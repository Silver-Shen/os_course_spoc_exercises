#lec9 在线练习
## 选择题

---

物理页帧数量为3，且初始时没有对应的虚拟页。虚拟页访问序列为 0,1,2,0,1,3,0,3,1,0,3，请问采用最优置换算法的缺页次数为（）  s2

- [ ] 1
- [ ] 2
- [ ] 3
- [x] 4

> 4


物理页帧数量为3，且初始时没有对应的虚拟页。虚拟页访问序列为 0,1,2,0,1,3,0,3,1,0,3，请问采用LRU置换算法的缺页次数为（） s2
- [ ] 1
- [ ] 2
- [ ] 3
- [x] 4

> 4


物理页帧数量为3，且初始时没有对应的虚拟页。虚拟页访问序列为 0,1,2,0,1,3,0,3,1,0,3，请问采用FIFO置换算法的缺页次数为（） s2
- [ ] 1
- [ ] 2
- [ ] 4
- [x] 6

> 6


物理页帧数量为4，且初始时没有对应的虚拟页。虚拟页访问序列为 0,3,2,0,1,3,4,3,1,0,3,2,1,3,4 ，请问采用CLOCK置换算法（用1个bit表示存在时间）的缺页次数为（） s3

- [ ] 8
- [x] 9
- [ ] 10
- [ ] 11

> 9

物理页帧数量为4，且初始时没有对应的虚拟页。虚拟页访问序列为 0,3,2,0,1,3,4,3,1,0,3,2,1,3,4 ，请问采用CLOCK置换算法（用2个关联，bit表示存在时间,可以表示4,）的缺页次数为（） s3
- [x] 7
- [ ] 8
- [ ] 9
- [ ] 10

> 7

```
物理页帧数量为4
0,3,2,0,1,3,4,3,1,0,3,2,1,3,4

1 0
0
f 1
0 01 0 
1 00    <--
2 00
3 00

2 3
3,0
f 2
0 01 0
0 01 0 
1 01 3 
2 00    <--
3 00

3 2
2,3,0
f 3
0 01 0 
1 01 3 
2 01 2  
3 00   <--

4 0
2,3,0
f 3
0 10 0 
1 01 3 
2 00 2  
3 00   <--


5 1 
1,2,3,0
f 4

0 10 0 <--
1 01 3 
2 01 2  
3 01 1  


6 3
1,2,3,0

0 10 0 <--
1 10 3 
2 01 2  
3 01 1  


7 4
f 5

round 1
0 01 0 <--
1 01 3 
2 00 2  
3 00 1  

round 2

0 00 0
1 00 3
2 01 4  
3 00 1  <--

8 3
f 
0 00 0
1 01 3
2 01 4  
3 00 1  <--


9 1
f 
0 00 0
1 01 3
2 01 4  
3 01 1  <--


10 0
f 
0 01 0
1 01 3
2 01 4  
3 01 1  <--

11 3
f 
0 01 0
1 10 3
2 01 4  
3 01 1  <--

12 2
f 6
0 01 0
1 10 3
2 01 4  
3 01 1  <--

round 1
0 00 0
1 01 3
2 00 4  
3 00 1  <--

round 2
0 00 0 <--
1 01 3
2 00 4  
3 01 2  

13 1 
f 7
0 01 1 
1 01 3 <--
2 00 4  
3 01 2 

14 3
f
0 01 1 
1 10 3 <--
2 00 4 
3 01 2 

15 4
f 7
0 01 1
1 10 3  <--
2 01 4  
3 01 2  
```

虚拟页访问序列为 1,2,3,4,1,2,5,1,2,3,4,5，物理页帧数量为3和4，采用FIFO置换算法，请问是否会出现bealdy现象() s4

- [x] 会
- [ ] 不会

> 3页时9次缺页，4页时10次缺页。



下面哪些页面淘汰算法不会产生Belady异常现象 s4
- [ ] 先进先出页面置换算法（FIFO)
- [ ] 时钟页面置换算法（CLOCK)
- [x] 最佳页面置换算法（OPT）
- [x] 最近最少使用页面置换算法（LRU）

> LRU和OPT属于一种栈算法

物理页帧数量为5，且初始时没有对应的虚拟页，虚拟页访问序列为 4,3,0,2,2,3,1,2,4,2,4,0,3，请问采用工作集置换算法（工作集窗口T=4）的缺页次数为（） s5
- [ ] 6
- [ ] 7
- [x] 8
- [ ] 9

> 8

```
 T:1.2.3.4.5.6.7.8.9.a,b,c,d
 P:4,3,0,2,2,3,1,2,4,2,4,0,3

 1 4
 f 1
 
 2 3
 3,4
 f 2
 
 3 0
 0,3,4
 f 3
 
 4 2
 2,0,3,4
 f 4
 
 5 2
 2,0,3
 f 4
 
 6 3
 3,2,0
 f 4
 
 7 1
 1,3,2
 f 5
 
 8 2 
 2,1,3
 f 5
 
 9 4
 4,2,1,3
 f 6

 10 2
 2,4,1

 11 4
 4,2

 12 0
 0,4,2
 f 7

 13 3
 3,0,4,2
 f 8

```

物理页帧数量为5，且初始时没有对应的虚拟页，虚拟页访问序列为 4,3,0,2,2,3,1,2,4,2,4,0,3，请问采用缺页率置换算法（窗口T=2）的缺页次数为（） s6
- [ ] 6
- [ ] 7
- [x] 8
- [ ] 9

> 8

```
 4,3,0,2,2,3,1,2,4,2,4,0,3
 1 4
 f 1
 
 2 3,4
 f 2
 
 3 0,3,4
 f 3

 4 2
  2,0,3,4
 f 4
 
 5 2
  2,0,3,4
 n f
 
 6 3
  3,2,0,4
 n f
 
 7 1
 f 5 t=3 >2 
[4,7] 1,3,2  ^0,4

 8 2
 2,1,3
 
 
 9 4
 f 6 t=9-7<=2
 4,2,1,3
 
 10 2 
 2,4,1,3
 
 11 4
 4,2,1,3
 
 12 0
 f 7  12-7=5>2
 0,4,2,1   ^3
 
 13 3
 f 8 13-12=1<=2
 3,0,4,2,1 
```   
 















