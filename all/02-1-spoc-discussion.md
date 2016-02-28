#lec 3 SPOC Discussion
##**提前准备**
（请在周一上课前完成）

 - 完成lec3的视频学习和提交对应的在线练习
 - git pull ucore_os_lab, v9_cpu, os_course_spoc_exercises  　in github repos。这样可以在本机上完成课堂练习。
 - 仔细观察自己使用的计算机的启动过程和linux/ucore操作系统运行后的情况。
 - 了解控制流，异常控制流，函数调用,中断，异常(故障)，系统调用（陷阱）,切换，用户态（用户模式），内核态（内核模式）等基本概念。思考一下这些基本概念在linux, ucore, v9-cpu中的os*.c中是如何具体体现的。
 - 思考为什么操作系统需要处理中断，异常，系统调用。这些是必须要有的吗？有哪些好处？有哪些不好的地方？
 - 了解在PC机上有啥中断和异常。搜索“80386　开机　启动”
 - 安装好ucore实验环境，能够编译运行lab8的answer
 - 了解Linux和ucore有哪些系统调用。搜索“linux 系统调用", 搜索lab8中的syscall关键字相关内容。
 - 会使用linux中的命令:objdump，nm，file, strace，了解这些命令的用途。
 - 了解如何OS是如何实现中断，异常，或系统调用的。会使用v9-cpu的dis,xc, xem命令（包括启动参数），分析v9-cpu中的os0.c, os2.c，了解与异常，中断，系统调用相关的os设计实现。阅读v9-cpu中的cpu.md文档，了解汇编指令的类型和含义等，了解v9-cpu的细节。
 - 在piazza上就lec3学习中不理解问题进行提问。
 
## 第三讲 启动、中断、异常和系统调用-思考题

## 3.1 BIOS
 1. 比较UEFI和BIOS的区别。
 >[UEFI](http://www.ihacksoft.com/uefi.html)([wiki](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface))作为传统BIOS的继任者，UEFI拥有前辈所不具备的诸多功能，比如图形化界面、多种多样的操作方式、允许植入硬件驱动等等。这些特性让UEFI相比于传统BIOS更加易用、更加多功能、更加方便。<br>
相比于BIOS，UEFI的优势有以下几点<br>

```
* Ability to boot from large disks (over 2 TB) with a GUID Partition Table (GPT)[13][b]
* CPU-independent architecture[b]
* CPU-independent drivers[b]
* Flexible pre-OS environment, including network capability
* Modular design
```
UEFI本身相当于一个微型操作系统，UEFI已具备文件系统的支持，它能够直接读取FAT分区中的文件。其次，可开发出直接在UEFI下运行的应用程序，这类程序文件通常以efi结尾。既然UEFI可以直接识别FAT分区中的文件，又有可直接在其中运行的应用程序。那么完全可以将Windows安装程序做成efi类型应用程序，然后把它放到任意fat分区中直接运行即可，也就是说UEFI不需要主引导记录，也不需要活动分区，就能完成系统的启动。

 2. 描述PXE的大致启动流程。
 [wiki](https://en.wikipedia.org/wiki/Preboot_Execution_Environment)<br>
 [一些解释](http://searchnetworking.techtarget.com/definition/Preboot-Execution-Environment)
 
## 3.2 系统启动流程
 1. 了解NTLDR的启动流程。[wiki](https://en.wikipedia.org/wiki/NTLDR)/[baike](http://baike.baidu.com/link?url=q1YAdPvA3EYyUUXsJFkXNnnI4zKxjvouDb5jScqaYbENKoJoE7cQAKOlAMnjQ5nsemP2-ufEygkn26FdruP5oK)
 1. 了解GRUB的启动流程。[baike](http://baike.baidu.com/link?url=1Ppn1pBFldWVUk1k4qkD6uHpHob6aK6cVMi3fS_ZmNMI7zCbndv_yNdekdQ-2t8IIQfctznJ25hc3LWHDLkTYa)/[wiki](https://zh.wikipedia.org/wiki/GNU_GRUB)
 1. 比较NTLDR和GRUB的功能差异。
 [网络](http://www.frozentechnology.com/2003/10/16/boot-loader-review-six-boot-loaders-compared/)/[本地](/Users/Silver_Bullet/Desktop/2015-2016Spring/Operating Systems/第三讲 系统启动、中断、异常和系统调用/grub_ntldr.html)
 1. 了解u-boot的功能。[csdn](http://blog.csdn.net/ghostyu/article/details/6953982)
 
## 3.3 中断、异常和系统调用比较
 1. 举例说明Linux中有哪些中断，哪些异常？
 1. Linux的系统调用有哪些？大致的功能分类有哪些？  (w2l1)

```
  + 采分点：说明了Linux的大致数量（上百个），说明了Linux系统调用的主要分类（文件操作，进程管理，内存管理等）
  - 答案没有涉及上述两个要点；（0分）
  - 答案对上述两个要点中的某一个要点进行了正确阐述（1分）
  - 答案对上述两个要点进行了正确阐述（2分）
  - 答案除了对上述两个要点都进行了正确阐述外，还进行了扩展和更丰富的说明（3分）
 ```
 
 1. 以ucore lab8的answer为例，uCore的系统调用有哪些？大致的功能分类有哪些？(w2l1)
 
 ```
  + 采分点：说明了ucore的大致数量（二十几个），说明了ucore系统调用的主要分类（文件操作，进程管理，内存管理等）
  - 答案没有涉及上述两个要点；（0分）
  - 答案对上述两个要点中的某一个要点进行了正确阐述（1分）
  - 答案对上述两个要点进行了正确阐述（2分）
  - 答案除了对上述两个要点都进行了正确阐述外，还进行了扩展和更丰富的说明（3分）
 ```
 
## 3.4 linux系统调用分析
 1. 通过分析[lab1_ex0](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex0.md)了解Linux应用的系统调用编写和含义。(w2l1)
 >工具大致用法<br>
 [objdump](http://blog.csdn.net/beyondioi/article/details/7796414)<br>
 [nm](http://blog.csdn.net/stpeace/article/details/47089585)<br>
 [file](http://www.cnblogs.com/kerrycode/p/3806618.html)<br>
 linux 的系统调用都有一个系统调用编号，在调用时把响应的编号存入eax寄存器，所需的参数依次存入ebx,ecx,edx寄存器，然后调用int 0x80完成系统调用；objdump主要完成可执行文件的反汇编、nm显示文件的符号信息、file显示文件类型

 ```
  + 采分点：说明了objdump，nm，file的大致用途，说明了系统调用的具体含义
  - 答案没有涉及上述两个要点；（0分）
  - 答案对上述两个要点中的某一个要点进行了正确阐述（1分）
  - 答案对上述两个要点进行了正确阐述（2分）
  - 答案除了对上述两个要点都进行了正确阐述外，还进行了扩展和更丰富的说明（3分）
 
 ```
 
 1. 通过调试[lab1_ex1](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex1.md)了解Linux应用的系统调用执行过程。(w2l1)
 >[strace](http://man.linuxde.net/strace)可以执行一个指定的命令，在命令执行的过程中，strace会记录和解析命令进程的所有系统调用以及这个进程所接收到的所有的信号值<br>
利用strace可以看到lab1-ex1.exe执行过程中的系统调用统计和过程<br>
[execve](http://blog.163.com/fan_yishan/blog/static/47692213201491251120755/)、[brk](http://blog.csdn.net/sgbfblog/article/details/7772153)、[access](http://blog.sina.com.cn/s/blog_6a1837e90100uh5d.html)、[mmap](http://blog.chinaunix.net/uid-26669729-id-3077015.html)、open、close、[fstat](http://blog.sina.com.cn/s/blog_803527e70100veqr.html)、[mprotect](http://blog.csdn.net/ustc_dylan/article/details/6941768)、munmap、write、[arch_prctl](http://man7.org/linux/man-pages/man2/arch_prctl.2.html)<br>
系统调用由应用程序发起，通过int 0x80进行软中断，之后系统跳转到一个预设的内核空间地址中的system_call系统调用处理函数，通过eax中的系统调用号查表计算出服务程序入口地址，并将参数压栈后跳转到服务程序进行处理

 ```
  + 采分点：说明了strace的大致用途，说明了系统调用的具体执行过程（包括应用，CPU硬件，操作系统的执行过程）
  - 答案没有涉及上述两个要点；（0分）
  - 答案对上述两个要点中的某一个要点进行了正确阐述（1分）
  - 答案对上述两个要点进行了正确阐述（2分）
  - 答案除了对上述两个要点都进行了正确阐述外，还进行了扩展和更丰富的说明（3分）
 ```
 
## 3.5 ucore系统调用分析
 1. ucore的系统调用中参数传递代码分析。
 1. ucore的系统调用中返回结果的传递代码分析。
 1. 以ucore lab8的answer为例，分析ucore 应用的系统调用编写和含义。
 1. 以ucore lab8的answer为例，尝试修改并运行ucore OS kernel代码，使其具有类似Linux应用工具`strace`的功能，即能够显示出应用程序发出的系统调用，从而可以分析ucore应用的系统调用执行过程。
 
## 3.6 请分析函数调用和系统调用的区别
 1. 请从代码编写和执行过程来说明。
   1. 说明`int`、`iret`、`call`和`ret`的指令准确功能
 
