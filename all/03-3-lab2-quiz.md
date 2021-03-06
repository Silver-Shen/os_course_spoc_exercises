# lab2在线练习


## 选择题

---
####7.1 了解x86保护模式中的特权级

80386 CPU保护模式下的特权级个数是()  s1

- [ ] 1
- [ ] 2
- [ ] 3
- [x] 4

> ring0-ring3


ucore OS中使用了的80386 CPU保护模式下的特权级的级别包括()  s1
- [x] 0
- [ ] 1
- [ ] 2
- [x] 3

> ring 0 for OS， ring3 for application


在ucore OS的管理下，如果CPU在ring3特权级执行访存指令，读属于ring0特权级的数据段中的内存单元，将出现的情况是（） s1
- [ ] 产生外设中断
- [x] 产生访存异常
- [ ] CPU继续正常执行
- [ ] 系统重启

> 将产生`General Protection Fault异常`


段描述符中与特权级相关的一个组成部分的名称是（） s1
- [x] DPL
- [ ] AVL
- [ ] Base
- [ ] Limit

> 是DPL


CS段寄存器中的最低两位保存的是（） s1
- [ ] DPL
- [x] CPL
- [ ] RPL
- [ ] NPL

> 是CPL


DS段寄存器中的最低两位保存的是（） s1
- [ ] DPL
- [ ] CPL
- [x] RPL
- [ ] NPL

> 是RPL


CPU执行一条指令访问数据段时，硬件要做的特权级检查是（） s1
- [x] MAX(CPL, RPL) <= DPL[数据段]
- [ ] MIN(CPL, RPL) <= DPL[数据段]
- [ ] MAX(CPL, DPL) <= RPL[数据段]
- [ ] MIN(CPL, DPL) <= RPL[数据段]

> 是MAX(CPL, RPL) <= DPL[数据段]

---
####7.2了解特权级切换过程

对于Task State Segment（TSS）而言，uCore OS可以利用它做（） s2
- [x] 保存ring 0的SS
- [x] 保存ring 0的ESP
- [ ] 保存中断描述符表的基址
- [ ] 保存全局描述符表的基址

> 是保存ring 0的SS和ESP

---
####7.3了解段/页表
页目录表的基址是保存在寄存器（） s3
- [ ] CR0
- [ ] CR1
- [ ] CR2
- [x] CR3

> CR3

在启动页机制后，不可能进行的操作包括（） s3
- [x] 取消段机制，只保留页机制
- [ ] 取消页机制，只保留段机制
- [ ] 取消页机制，也取消段机制
- [ ] 保留页机制，也保留段机制

> 不可能取消段机制，只保留页机制

---
####7.4了解UCORE建立段/页表
给定一个虚页地址和物理页地址，在建立二级页表并建立正确虚实映射关系的过程中，需要完成的事务包括() s4
- [x] 给页目录表动态分配空间，给页表分配空间
- [x] 让页基址寄存器的高20位内容为页目录表的高20位物理地址
- [x] 在虚地址高10位的值为index的页目录项中的高20位填写页表的高20位物理地址，设置有效位
- [x] 在虚地址中10位的值为index的页表项中中的高20位填写物理页地址的高20位物理地址，设置有效位

> 都对，还要设置更多的一些属性。


---
