# lec5 SPOC思考题

## 提前准备

- 完成lec５的视频学习和提交对应的在线练习
- git pull ucore_os_lab, v9_cpu, os_course_spoc_exercises 　in github repos。这样可以在本机上完成课堂练习。
- 理解连续内存动态分配算法的实现（主要自学和网上查找）

NOTICE
- 有"w3l1"标记的题是助教要提交到学堂在线上的。
- 有"w3l1"和"spoc"标记的题是要求拿清华学分的同学要在实体课上完成，并按时提交到学生对应的git repo上。
- 有"hard"标记的题有一定难度，鼓励实现。
- 有"easy"标记的题很容易实现，鼓励实现。
- 有"midd"标记的题是一般水平，鼓励实现。


## 个人思考题
---

请简要分析最优匹配，最差匹配，最先匹配，buddy systemm分配算法的优势和劣势，并尝试提出一种更有效的连续内存分配算法 (w3l1)

```
  + 采分点：说明四种算法的优点和缺点
  - 答案没有涉及如下3点；（0分）
  - 正确描述了二种分配算法的优势和劣势（1分）
  - 正确描述了四种分配算法的优势和劣势（2分）
  - 除上述两点外，进一步描述了一种更有效的分配算法（3分）
 ```
- [x]  

>  1. 最先匹配：优点是实现比较简单，可以在高地址有大块空间使用；缺点是会在低地址产生很多的外部碎片，如果要分配大块内存需要搜索很久；
>  2. 最佳匹配：优点是可以减少外部碎片的大小，避免大块区域被拆分；缺点是预留的外部碎片很难利用
>  3. 最差匹配：优点是适合中等大小的内存分配，余下的部分经常可以利用；缺点是破坏了大分区
>  4. 伙伴系统：优点是有效减少了外部碎片，且实现效率较高（二叉树实现）；缺点是会产生比较大的内部碎片
>  
>  可以对最先匹配做一些改进，搜索位置从上一次分配的空闲块开始，而不是从0地址开始，这样可以有效减少在低地址有大量外部碎片的情况

## 小组思考题

请参考ucore lab2代码，采用`struct pmm_manager` 根据你的`学号 mod 4`的结果值，选择四种（0:最优匹配，1:最差匹配，2:最先匹配，3:buddy systemm）分配算法中的一种或多种，在应用程序层面(可以 用python,ruby,C++，C，LISP等高语言)来实现，给出你的设思路，并给出测试用例。 (spoc)
>伙伴系统的实现<br>
[buddy_system](https://github.com/Silver-Shen/Buddy_System/blob/master/pmm_manager.cpp)<br>
[文档](https://github.com/Silver-Shen/Buddy_System/blob/master/README.md)


请参考xv6（umalloc.c），ucore lab2代码，选择四种（0:最优匹配，1:最差匹配，2:最先匹配，3:buddy systemm）分配算法中的一种或多种，在Linux应用程序/库层面，用C、C++或python来实现malloc/free，给出你的设计思路，并给出可以在Linux上运行的malloc/free实现和测试用例。 (spoc)

- [基于malloc与free函数的实现代码及分析](http://www.jb51.net/article/36391.htm)


```
如何表示空闲块？ 如何表示空闲块列表？ 
[(start0, size0),(start1,size1)...]
在一次malloc后，如果根据某种顺序查找符合malloc要求的空闲块？如何把一个空闲块改变成另外一个空闲块，或消除这个空闲块？如何更新空闲块列表？
在一次free后，如何把已使用块转变成空闲块，并按照某种顺序（起始地址，块大小）插入到空闲块列表中？考虑需要合并相邻空闲块，形成更大的空闲块？
如果考虑地址对齐（比如按照4字节对齐），应该如何设计？
如果考虑空闲/使用块列表组织中有部分元数据，比如表示链接信息，如何给malloc返回有效可用的空闲块地址而不破坏
元数据信息？
伙伴分配器的一个极简实现
http://coolshell.cn/tag/buddy
```

--- 

## 扩展思考题

阅读[slab分配算法](http://en.wikipedia.org/wiki/Slab_allocation)，尝试在应用程序中实现slab分配算法，给出设计方案和测试用例。

## “连续内存分配”与视频相关的课堂练习

### 5.1 计算机体系结构和内存层次
MMU的工作机理？

- [x]  

>  http://en.wikipedia.org/wiki/Memory_management_unit

L1和L2高速缓存有什么区别？

- [x]  

>  http://superuser.com/questions/196143/where-exactly-l1-l2-and-l3-caches-located-in-computer
>  Where exactly L1, L2 and L3 Caches located in computer?

>  http://en.wikipedia.org/wiki/CPU_cache
>  CPU cache

### 5.2 地址空间和地址生成
编译、链接和加载的过程了解？

- [x]  

>  

动态链接如何使用？

- [x]  

>  


### 5.3 连续内存分配
什么是内碎片、外碎片？

- [x]  

>  

为什么最先匹配会越用越慢？

- [x]  

>  

为什么最差匹配会的外碎片少？

- [x]  

>  

在几种算法中分区释放后的合并处理如何做？

- [x]  

>  

### 5.4 碎片整理
一个处于等待状态的进程被对换到外存（对换等待状态）后，等待事件出现了。操作系统需要如何响应？

- [x]  

>  

### 5.5 伙伴系统
伙伴系统的空闲块如何组织？

- [x]  

>  

伙伴系统的内存分配流程？

- [x]  

>  

伙伴系统的内存回收流程？

- [x]  

>  

struct list_entry是如何把数据元素组织成链表的？

- [x]  

>  



## v9-cpu相关

[challenge]在v9-cpu上完成基于method-0/1/2/buddy system（选一个方法）with first/best/worst-fit(选一个fit)用户态动态内存分配函数malloc/free，要求在内核态实现sbrk系统调用以支持用户态动态内存分配方法。基于os4.c实现，可参考v9-cpu git repo的testing分支中的os.c和mem.h

- [x]  

> 

[challenge]在v9-cpu上完成基GC算法，要求在内核态实现sbrk系统调用以支持用户态动态内存分配方法。基于os4.c实现，可参考v9-cpu git repo的testing分支中的os.c和mem.h

- [x]  

>

## 其它
- 静态分配内存与动态分配内存的区别是啥？
- 在隐式链表结构中，如何实现向前的合并操作？
- 如何判断一个函数是库函数还是一个系统调用？
- 为何要在OS内部和用户态中实现两层动态内存分配？
- 为何在OS内部没有采用GC分配方式？
