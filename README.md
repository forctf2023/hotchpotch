# hotchpotch
Hotchpotch of some knowledge.

### nice 技术学习网站： https://huntingday.github.io/    


- CSRF(Cross-site Request Forgery)跨站请求伪造
[参考链接](https://www.cnblogs.com/liuqingzheng/p/9505044.html)

- msf set rhosts 从文件读取：
msf auxiliary(smb_ms17_010) > set rhosts file:/root/pentest/10-all.txt


- linux 各个文件夹作用
1. /usr：系统级的目录，可以理解为C:/Windows/，/usr/lib理解为C:/Windows/System32。
2. /usr/local：用户级的程序目录，可以理解为C:/Progrem Files/。用户自己编译的软件默认会安装到这个目录下。
3. /opt：用户级的程序目录，可以理解为D:/Software，opt有可选的意思，这里可以用于放置第三方大型软件（或游戏），当你不需要时，直接rm -rf掉即可。在硬盘容量不够时，也可将/opt单独挂载到其他磁盘上使用。
        源码放哪里？
        /usr/src：系统级的源码目录。
        /usr/local/src：用户级的源码目录。   
-----------------翻译-------------------
       
        /opt    
        Here’s where optional stuff is put. Trying out the latest Firefox beta? Install it to /opt where you can delete it without affecting other settings. Programs in here usually live inside a single folder whick contains all of their data, libraries, etc.
        这里主要存放那些可选的程序。你想尝试最新的firefox测试版吗?那就装到/opt目录下吧，这样，当你尝试完，想删掉firefox的时候，你就可 以直接删除它，而不影响系统其他任何设置。安装到/opt目录下的程序，它所有的数据、库文件等等都是放在同个目录下面。
        举个例子：刚才装的测试版firefox，就可以装到/opt/firefox_beta目录下，/opt/firefox_beta目录下面就包含了运 行firefox所需要的所有文件、库、数据等等。要删除firefox的时候，你只需删除/opt/firefox_beta目录即可，非常简单。   

        /usr/local

        This is where most manually installed(ie. outside of your package manager) software goes. It has the same structure as /usr. It is a good idea to leave /usr to your package manager and put any custom scripts and things into /usr/local, since nothing important normally lives in /usr/local.

        这里主要存放那些手动安装的软件，即不是通过“新立得”或apt-get安装的软件。它和/usr目录具有相类似的目录结构。让软件包管理器来管理/usr目录，而把自定义的脚本(scripts)放到/usr/local目录下面，我想这应该是个不错的主意。           
        
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


## Linux内核版本与系统版本信息查看以及x86与x86_64的区别
### 一、 x86与x86_64

x86、x86_64主要的区别就是32位和64位的问题。

x86 ======> 32位   
x86_64 和 x64 以及AMD64 ======> 都是64位

　　x86是指intel的开发的一种32位指令集，从386开始时代开始的，一直沿用至今，是一种cisc指令集，所有intel早期的cpu，amd早期的cpu都支持这种指令集，ntel官方文档里面称为“IA-32”

　　 x84_64是x86 CPU开始迈向64位的时候，有2选择：1、向下兼容x86。2、完全重新设计指令集，不兼容x86。AMD抢跑了，比Intel率先制造出了商用的兼容x86的CPU，AMD称之为AMD64。而Intel选择了设计一种不兼容x86的全新64为指令集，称之为IA-64，但是比amd晚了一步，因为是全新设计的CPU，没有编译器，也不支持windows、后来不得不在时机落后的情况下也开始支持AMD64的指令集，但是换了个名字，叫x86_64，表示是x86指令集的64扩展，。也就是说实际上，x86_64,x64,AMD64基本上是同一个东西。

### 二、查看Linux内核信息
```
[root@localhost ~]# cat /proc/version
Linux version 2.6.32-642.el6.x86_64 (mockbuild@worker1.bsys.centos.org) (gcc version 4.4.7 20120313 (Red Hat 4.4.7-17) (GCC) ) #1 SMP Tue May 10 17:27:01 UTC 2016
[root@localhost ~]# uname -r
2.6.32-642.el6.x86_64
[root@localhost ~]# uname -a
Linux localhost.localdomain 2.6.32-642.el6.x86_64 #1 SMP Tue May 10 17:27:01 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
uname -r 显示的结果是什么意思?
2.6.32-642.el6.x86_64
2： —->主版本号
6： —–>次版本号 6 表示稳定版本
32： —–>修订版本号，表示修订次数
```
### 三、查看Linux版本信息
```
[root@localhost ~]# cat /etc/issue
CentOS release 6.8 (Final)
Kernel \r on an \m
[root@localhost ~]# cat /etc/redhat-release
CentOS release 6.8 (Final)
[root@localhost ~]# file /bin/bash
/bin/bash: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.18, stripped
[root@localhost ~]# file /bin/cat
/bin/cat: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.18, stripped
```
### 四、查看当前系统的位数
上面已经可以看出来uname -r cat /proc/version uname -a 都可以查看内核的位数，file /bin/bash 以及 file /bin/cat 可以查看当前你系统的位数。对应的结果是 x86_64 也即是64位。

但是还有更简单粗暴的方法：
```
[root@localhost ~]# getconf LONG_BIT
64
```
显示的结果直接就是位数。
