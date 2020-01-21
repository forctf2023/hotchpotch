## PWD  
#### PWN工具： binutils/nasm/ncat/gdb/pwntools/ropgadget/peda   
#### pwn入门 https://www.jianshu.com/p/187b810e78d2    
- 栈(stack)和堆(heap)的区别：    
  全局、静态、局部变量存于栈中，用户自定义内存段（malloc 的变量置于堆中）  堆栈都是内存部分。   
gdb使用的wiki 很基础且有用 http://wiki.ubuntu.org.cn/%E7%94%A8GDB%E8%B0%83%E8%AF%95%E7%A8%8B%E5%BA%8F    

- gcc编译时，-fno-stack-protector参数   
意思是禁用canary保护. canary是一种用来防护栈溢出的保护机制。其原理是在一个函数的入口处，先从fs/gs寄存器中取出一个4字节(eax)或者8字节(rax)的值存到栈上，当函数结束时会检查这个栈上的值是否和存进去的值一致，若一致则正常退出，如果是栈溢出或者其他原因导致canary的值发生变化，那么程序将执行___stack_chk_fail函数，继而终止程序 详见 https://www.anquanke.com/post/id/177832

