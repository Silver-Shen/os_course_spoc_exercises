# lab3 SPOC思考题

=======
# lab3 SPOC思考题

NOTICE
- 有"w5l2"标记的题是助教要提交到学堂在线上的。
- 有"w5l2"和"spoc"标记的题是要求拿清华学分的同学要在实体课上完成，并按时提交到学生对应的git repo上。
- 有"hard"标记的题有一定难度，鼓励实现。
- 有"easy"标记的题很容易实现，鼓励实现。
- 有"midd"标记的题是一般水平，鼓励实现。

## 个人思考题
---

### 10.1 实验目标：虚存管理
---

(1)缺页异常的处理流程？

(2)从外存的页面的存储和访问代码？

(3)缺页和页访问非法的返回地址有什么不同？

> 硬件设置、软件可修改； 中断号是

(4)虚拟内存管理中是否用到了段机制

(5)ucore如何知道页访问异常的地址？

### 10.2 回顾历史和了解当下
---

(6)中断处理例程的段表在GDT还是LDT？

(7)物理内存管理的数据结构在哪？

(8)页表项的结构？

(9)页表项的修改代码？

(10)如何设置一个虚拟地址到物理地址的映射关系？

(11)为了建立虚拟内存管理，需要在哪个数据结构中表示“合法”虚拟内存

### 10.3 处理流程、关键数据结构和功能
---

(12)swap_init()做了些什么？

(13)vmm_init()做了些什么？

(14)vma_struct数据结构的功能？

(15)mmap_list是什么列表？

(16)外存中的页面后备如何找到？

(17)vma_struct和mm_struct的关系是什么？

> 合法的连续虚拟地址区域、整个进程的地址空间

(18)画数据结构图，描述进程的虚拟地址空间、页表项、物理页面和后备页面的关系；

### 10.4 页访问异常
---

(19)页面不在内存和页面访问非法的处理中有什么区别？对应的代码区别在哪？

(20)find_vma()做了些什么？

(21)swapfs_read()做了些什么？

(22)缺页时的页面创建代码在哪？

(23)struct rb_tree数据结构的原理是什么？在虚拟管理中如何用它的？


(24)页目录项和页表项的dirty bit是何时，由谁置1的？


(25)页目录项和页表项的access bit是何时，由谁置1的？


### 10.5 页换入换出机制
---

(26)虚拟页与磁盘后备页面的对应有关系？

(27)如果在开始加载可执行文件时，如何改？

(28)check_swap()做了些什么检查？

(29)swap_entry_t数据结构做什么用的？放在什么地方？

(30)空闲物理页面的组织数据结构是什么？

(21)置换算法的接口数据结构？

> swap_manager

================


## 小组思考题
---
(1)(spoc) 请参考lab3_result的代码，思考如何在lab3_results中实现clock算法，给出你的概要设计方案。可4人一个小组。要求说明你的方案中clock算法与LRU算法上相比，潜在的性能差异性。进而说明在lab3的LRU算法实现的可能性评价（给出理由）。
>
可以重用一部分FIFO的框架，主要修改的部分为swap_manager这个数据结构
修改的函数为

```
int (*map_swappable)   (struct mm_struct *mm, uintptr_t addr, struct Page *page, int swap_in);
int (*swap_out_victim) (struct mm_struct *mm, struct Page **ptr_page, int in_tick);
```
>（1）FIFO在维护可交换页面的时候采用了单向的链表，在map_swappable里维护了这个链表<br>
CLOCK算法需要维护一个循环链表，故需要把头结点和尾结点连在一起，可以调用list_entry提供的宏<br>
（2）页面换出的算法，即swap_out_victim需要修改
原先的数据结构修改了Page结构

```
struct Page {
    int ref;                        // page frame's reference counter
    uint32_t flags;                 // array of flags that describe the status of the page frame
    unsigned int property;          // the num of free block, used in first fit pm manager
    list_entry_t page_link;         // free list link
    list_entry_t pra_page_link;     // used for pra (page replace algorithm)
    uintptr_t pra_vaddr;            // used for pra (page replace algorithm)
};
```

我认为这里Page还需要加一个域来表示访问位，这个位可以由硬件来记录（在页表上记录）
然后Page里加入一个宏来映射这个访问位，在swap_out_victim中遍历链表，查看访问位，并决定是否换出
>性能分析：FIFO在某些情况下性能非常差，因为可能和访问时候的特征相悖。LRU的时间开销非常大，实现也比较复杂。而clock算法实现较为简单，性能也比较好，因为每次读操作只需要修改标志位（由硬件完成），多次写操作才回写回一次，每次缺页不会转太多（因为每次访问最多+1，每转一格-1，这样转的格数不会超过访问次数）。LRU的性能较差，但是可能缺页率会比Clock更好。因为每次访问需要修改链表的结构。

(2)(spoc) 理解内存访问的异常。在x86中内存访问会受到段机制和页机制的两层保护，请基于lab3_results的代码（包括lab1的challenge练习实现），请实践并分析出段机制和页机制各种内存非法访问的后果。，可4人一个小组，，找出尽可能多的各种内存访问异常，并在代码中给出实现和测试用例，在执行了测试用例后，ucore能够显示出是出现了哪种异常和尽量详细的错误信息。请在说明文档中指出：某种内存访问异常的原因，硬件的处理过程，以及OS如何处理，是否可以利用做其他有用的事情（比如提供比物理空间更大的虚拟空间）？哪些段异常是否可取消，并用页异常取代？

## v9-cpu相关
---
(1)分析并编译运行v9-cpu git repo的testing branch中的,root/etc/os_lab2.c os_lab3.c os_lab3_1.c,理解虚存机制是如何在v9-cpu上实现的，思考如何实现clock页替换算法，并给出你的概要设计方案。

(2)分析并编译运行v9-cpu git repo的testing branch中的,root/etc/os_lab2.c os_lab3.c os_lab3_1.c，理解内存访问异常的各种情况，并给出你的分析结果。