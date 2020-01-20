# LINUX 0.11
## 开机到main()
### 实现从启动盘加载操作系统程序
1. 启动BIOS，准备实模式下的中断向量表和中断服务程序
2. 从启动盘加载操作系统到内存（利用中断服务程序）
  * 由BIOS中断int 0x19h把第一扇区bootsect的内容加载到内存中
  * 在bootsect的指挥下，把其后的四个扇区加载到内存
  * 在bootsect的指挥下，把上一步随后的240个扇区加载到内存
3. 为执行32位main函数做过渡工作

## 术语
**实模式** Intel 80286和之后的80x86兼容CPU的操作模式<br/>
**RAM** Random Access Memory 随机存取存储器。 <br/>
**IP/EIP** Instruction Pointer 指令指针寄存器，存在于CPU中，记录将要执行的指令在代码段内的偏移地址，它与CS组合即为将要执行的指令的内存地址。<br/>
**CS** Code Segment Register 代码段寄存器，存在于CPU中，指向CPU当前执行代码在内存中所在的区域。<br/>
**ROM** Read Only Memory 只读存储器。<br/>
**中断INT** INTerrupt 原指外在事件打断正在执行的程序，处理外在事件后，回到被打断的程序继续执行。现在，可先理解为一种技术手段，与c语言函数调用类似。<br/>
**中断向量表** Interrupt Vector Table 实模式中断机制的重要组成部分，表中记录所有中断号对应的中断服务程序的内存地址。<br/>
**中断服务程序** Interrupt Services 通过中断向量表的索引对中断进行响应服务，是一些具有特定功能的程序。<br/>