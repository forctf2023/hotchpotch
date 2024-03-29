### CRT MFC ATL

#### vs 报error LNK2005 XXX defined in XXX  
当是关于nafxcw.lib libcpmt.lib 等这些库的时候  大概率是因为LIBCMT.lib nafxcw.lib两个库重定义了同样的函数（跟上面crt atl mfc有关），和可以用在工程配置Linker的input手动设置link顺序（并且在ignore中添加两个库解决）；而更简便的方式是在linker->Command Line->Additional Options中添加/FORCE:MULTIPLE解决
In simple terms, you need to use /FORCE:MULTIPLE linker option to make VC++ generate a valid exe or dll file, even if there are multiple definitions. You need to add this to:   
Properties->Linker->Command Line->Additional Options   

#### 我的理解 CRT是最底层的，连windows API都是基于CRT编写的；ATL基于CRT，是静态链接了CRT代码；

https://blog.csdn.net/memeai/article/details/20037773 本文参考   

https://docs.microsoft.com/en-us/cpp/mfc/mfc-and-atl?view=msvc-160 （代查看）   

CRT原先是指Microsoft开发的C Runtime Library，用于操作系统的开发及运行。后来在此基础上开发了C++ Runtime Library，所以现在CRT是指Microsoft开发的C/C++ Runtime Library。在VC的CRT/SRC目录下，可以看到CRT的源码，不仅有C的，也有C++的。

     CRT原先的目的就是支持操作系统的运行。因为Windows操作系统除汇编部分外，都是用C/C++编写的，所以内核及许多关键服务都在CRT上运行（它们都采用dll技术动态链接）。此外，用 VC编写的C/C++程序也用到它们（可以动态链接，也可以静态链接，前者运行时需要系统中已安装CRT的dll，后者不需要）。可以说，CRT就是 Microsoft编写Windows时使用的低层类库。然后，它又被当作C++标准库的一个实现包含在了VC系列中；我们在VC中使用的C++标准库，其实就是CRT的一个真子集（少了C++标准所不包含的代码，特别是大量的低层C代码）

      至于CRT与WINDOWS API的关系，与许多人理解的相反，WINDOWS API作为Windows的一部份，是在CRT的基础上开发的。你可以将Windows（及其API）看作一个项目，而这个项目使用的语言是汇编/C/C ++，使用的类库就是CRT。所以，离开CRT，Windows API也无法使用的。

       C++标准，是C++的通用语言规范，指导所有C ++使用者。而CRT的其中一部分可以看作是Microsoft开发的一个C++标准库实现（其实也确实如此，Microsoft在开发CRT时，参考了正在标准化过程中的C++语言规范）。它与C++标准有一定的差距，部分原因是，在C++没有完成标准化之前，CRT已经开发并投入使用了。为了向下兼容以前的Windows代码，早期的CRT与C++标准总有一定的差距。但是CRT确实在不断的改进中。VC6带的CRT与C++标准还有比较大的差距，而 VC8的几乎完全符合C++标准了。
综上，CRT（Microsoft's C/C++ Runtime Library）的一个真子集（主要是C++ Runtime Library）是一个符合（或至少是企图符合）C++标准的C++库。而Windows API（以及Windows的其他许多部分）都是在CRT的基础上开发的。
   
      除了以上介绍的，在使用CRT的过程中，还需要了解的是：
     
      1、CRT的一些组成部分也调用了Windows API。这可能就是有人认为CRT是建立的Windows API基础上的原因。但是实际上，这一部分剥离CRT没有任何的问题。只不过Microsoft将在Windows平台上可以使用的C/C++低层库都加入到CRT中。因此，CRT中很大一部分是操作系统平台无关的（原始的CRT），是开发Windows本身及其上一切的基础。它们也可以作为一个C/C+ +库在其他操作系统平台上使用。还有一部分，则是和Windows紧密绑定的，调用Windows API来实现的，可以看作扩展的CRT。之所以将这两部分放在一起，是因为它们都是开发Windows操作系统所需要的，也因为它们也都是Windows 平台上的C/C++程序员所需要的。这种复杂关系是Microsoft的人为因素造成的，不能因此认为CRT是建立在Windows或Windows API基础上的。
     
      2、CRT的大部分内容是跨硬件平台的，但是也有一些部分，是直接用汇编写成、基于硬件平台、并根据特定硬件平台做的优化（而不是将生成机器码的责任完全交给编译器）。如早期对Indel的x32做了优化，现在由加入对AMD64的优化，这部分则是不跨硬件平台的。
关于ATL
     
      ATL是建立在CRT上的，如果你看了ATL的源码就知道了。至于不用链接，是因为ATL库静态链接了CRT，所以它可以在CRT之外运行。类似这样的误解在于混淆了作为低层基本库的CRT和作为产品而附带在VC中的CRT。虽然这两者是同样的代码，但是概念是不一样的。
     
      在编写操作系统时，你需要一个合适的低层库，以便完成一些基本的、多次重复的工作。于是，就有了CRT。在最低层的时候，根本连dll这个概念都没有的，所以CRT的源代码只能做成lib，被静态链接。然后，随着Windows越做越复杂，Microsoft提出了API的概念，它提供Windows开发者一组接口，可以直接操作Windows，这就是Windows API了。当然，Windows API也是在CRT之上编写的。

       接着， Microsoft想给予C/C++程序员以足够的支持，除了原始CRT之外，还要增加在Windows平台上编程所特有的东西，如thread等等。这些东西都是和平台相关的，只能建立在Windows API上。而这些新增内容，也被放进了CRT中。此时，CRT不仅仅包含最低层平台无关的代码，还包括平台相关的部分。如你调用CRT的 _beginthread，其实内部调用了Windows API的CreateThread。加入这些东西后，CRT仍然被用作编写操作系统；但是显然，那些调用了Windows API的部分已经失去移值性了。

       然后，CRT被封装成产品，随编译器一起发布。此时CRT产品的LIB和DLL都是Windows格式的，你不能在Windows以外的平台上使用EXE或DLL吧，这就是CRT和CRT产品的区别。Windows API的产品，或是Windows的其他许多组成部分也是一些LIB/DLL文件，这些都是表面的东西，是与Windows绑定在一起的。但是，如果你认为是先有Windows或Windows API，才有CRT的，那你就本末倒置了。除非你对CRT的定义就是那些LIB/DLL产品，而不包括用来产生它们的代码。
     
       就象C++编译器用来编译用C++写的编译器自身一样，Windows（及其上的编译器）用来作为平台开发和编译CRT，并也用CRT来写Windows自身（当然第一个CRT和第一个用来编译Windows的编译器不是在Windows上开发的）。就象“我”也可以先写一个类库，然后在它基础上写一个操作系统，在这个操作系统上进一步扩充这个类库，然后将它配合编译器发布出去，发展一些我的操作系统的支持者，顺便再赚点收入。或者以另一种模式发布另一个库（只是我在原来那个库上开发的一个产品，由于我独立地发布这个新库，许多人会不知道这个新库与旧库的关系。这很好，因为编程本身就是尽量隐藏细节，尽量做到对使用者透明的），吸引不同风格的开发者。这样我的付出得到了最大的回报——由于我没有发布操作系统的源代码，所以许多用户认为我不仅做了系统，还做了编译器，还开发了一个类库。做了那么多事，回报是应该的。其实他们不知道，类库是编写操作系统所必须的，编译器也是必须的，这些必须的东西却可以在操作系统之外获得更多的回报，真是太完美了！这是什么？这就是商业精神！当然这些误解对我是有好处的，我就不必到处宣扬真相了。反正我把类库的源码都发布了，也没有骗过人吧。我不过是在那个原始类库中加进了一些与我的操作系统相关的东西，以方便在我的系统上编写程序的人们，这是我的好心吧；至于有人可能产生进一步的误解，就不是我需要考虑的了……

       所以还是看看CRT的源码吧——看看那些针对硬件平台的汇编；看看VC的标准C++库和CRT关系；再看看其他操作系统的源代码，想想CRT中的哪些部分可以支持用来写操作系统，而如果我自己写系统，又需要哪些东西；甚至你可以看看DOS的源代码，想想和CRT的相似性，以及历史渊源。可惜不能看到Windows的源代码，否则一切就清楚了。

       最后再说一句，C++当然不是Microsoft的专利。但是Microsoft选择了C++，并取得了成功，这是肯定的了：象CRT，象VC，象Windows，象Office，象 SQLServer......这一方面说明了C++的优势，一方面也是Microsoft自身的因素在起作用。然后，它当然要紧抓C++的大旗，大力宣扬它自己的C++，并排斥其他的C++。这就是帝国的“风范”了。所以对Microsoft，总是即恨且爱，总希望哪天它会良心发现——当然这只是幻想罢了。不过，肯定该肯定的，否定该否定的，总是应该的。但就产品而言，Microsoft不是最好的，但大多都是最成功的，在看到它的不足的同时，也要看到它的优点。存在的即使不是合理的，也一定有它的合理性。所以，不能简单用一两句话评价Microsoft及它的成功。惟有一点是可以肯定的，它决定选择C ++，真是太英明了！


