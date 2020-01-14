# LINUX 0.11
## 开机到main()
### 实现从启动盘加载操作系统程序
1. 启动BIOS，准备实模式下的中断向量表和中断服务程序
2. 从启动盘加载操作系统到内存（利用中断服务程序）
3. 为执行32位main函数做过渡工作

## 术语
**实模式** Intel 80286和之后的80x86兼容CPU的操作模式<br/>
**RAM** Random Access Memory 随机存取存储器。 <br/>
**IP/EIP** Instruction Pointer 指令指针寄存器，存在于CPU中，记录将要执行的指令在代码段内的偏移地址，它与CS组合即为将要执行的指令的内存地址。<br/>
**CS** Code Segment Register 代码段寄存器，存在于CPU中，指向CPU当前执行代码在内存中所在的区域。<br/>
**ROM** Read Only Memory 只读存储器。<br/>