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
