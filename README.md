# hotchpotch
Hotchpotch of some knowledge.

### nice 技术学习网站： https://huntingday.github.io/    


- CSRF(Cross-site Request Forgery)跨站请求伪造
[参考链接](https://www.cnblogs.com/liuqingzheng/p/9505044.html)

- msf set rhosts 从文件读取：
msf auxiliary(smb_ms17_010) > set rhosts file:/root/pentest/10-all.txt


- linux 各个文件夹作用
1. /opt   主机额外安装软件所摆放的目录。默认是空的。 一般安装软件的时候，可以自己指定安装到这个目录下，便于查找和管理    
        opt (optional)，可选择目录，就像我们平时在安装windows软件的默认program files 的一样。
        
        
- windows  C:\Program Files和C:\Windows\System32 与  C:\Program Files (86)和C:\Windows\SysWoW64
64位Windows中提供了一种技术，Windows on Windows 64(即WoW64)。它可以使32位的应用程序正常地运行在64位的Windows中，这样用户在从32位到64位过渡的过程中，不会感受到很大的不便。为了能让32位的程序正常运行，64位的Windows中自带了一大部分的32位的系统文件，当32位程序运行的时候，系统会给它虚拟出一个32位的环境，这样32位程序会以为自己运行在32位Windows中。Windows的系统文件主要是存放在%SystemDrive%\Program Files和%Windir%\System32中（即通常的C:\Program Files和C:\Windows\System32)。64位系统中，这两个文件夹存放的是64位的系统文件，为了存放32位的同名系统文件，64位系统中有另外两个文件夹与之对应，%SystemDrive%\Program Files (86)和%Windir%\SysWoW64（即通常的C:\Program Files (86)和C:\Windows\SysWoW64)。

当32位程序需要访问Program Files或者System32中的文件时，系统会自动转向到Program Files (x86)或者SysWoW64中，这样32位的程序就可以正常的在64位Windows中运行了。类似的情况也发生在应用程序安装的时候，64位的程序一般都会被安装到Program Files中，而32位的程序则是装在Program Files (x86)中。

###  Compile C, C++, Objective-C, Ada, Fortran, Java, or treelang   
参考：http://gcc.gnu.org/onlinedocs/gcc-3.3.5/gcc/G_002b_002b-and-GCC.html   
Several versions of the compiler (C, C++, Objective-C, Ada, Fortran, Java and treelang) are integrated; this is why we use the name “GNU Compiler Collection”. GCC can compile programs written in any of these languages. The Ada, Fortran, Java and treelang compilers are described in separate manuals.

“GCC” is a common shorthand term for the GNU Compiler Collection. This is both the most general name for the compiler, and the name used when the emphasis is on compiling C programs (as the abbreviation formerly stood for “GNU C Compiler”).

When referring to C++ compilation, it is usual to call the compiler “G++”. Since there is only one compiler, it is also accurate to call it “GCC” no matter what the language context; however, the term “G++” is more useful when the emphasis is on compiling C++ programs.

Similarly, when we talk about Ada compilation, we usually call the compiler “GNAT”, for the same reasons.

We use the name “GCC” to refer to the compilation system as a whole, and more specifically to the language-independent part of the compiler. For example, we refer to the optimization options as affecting the behavior of “GCC” or sometimes just “the compiler”.

Front ends for other languages, such as Mercury and Pascal exist but have not yet been integrated into GCC. These front ends, like that for C++, are built in subdirectories of GCC and link to it. The result is an integrated compiler that can compile programs written in C, C++, Objective-C, or any of the languages for which you have installed front ends.

In this manual, we only discuss the options for the C, Objective-C, and C++ compilers and those of the GCC core. Consult the documentation of the other front ends for the options to use when compiling programs written in other languages.

G++ is a compiler, not merely a preprocessor. G++ builds object code directly from your C++ program source. There is no intermediate C version of the program. (By contrast, for example, some other implementations use a program that generates a C program from your C++ source.) Avoiding an intermediate C representation of the program means that you get better object code, and better debugging information. The GNU debugger, GDB, works with this information in the object code to give you comprehensive C++ source-level editing capabilities (see C and C++ (Debugging with GDB)).
