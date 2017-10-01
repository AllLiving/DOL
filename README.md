

<center>嵌入式系统导论实验报告

---

   姓名 	   学号   	 班级 	    电话     	       邮箱        
  曹广杰 	15352015	1501	13727022190	1553118845@qq.com

---

1.实验题目

<center><font size=5>lab2 DOL开发环境配置</font></center >

2.配置过程

1)首先是安装相关的环境

这里涉及到几个命令行，笔者对其分别进行解释：

<center>sudo apt-get update</center >

该命令需要管理员权限，目的是检查已有的软件是否需要升级，如果需要升级，则系统需要下载并安装软件，而这样更改计算机系统配置的操作是需要管理员权限的。

<center>sudo apt-install ant</center >

继而安装ant编译环境，用于之后的编译，该操作与之后的几个环境的安装操作如出一辙，就不予赘述了。（同样的有openjdk-8-jdk[Java编译环境]，unzip解压软件）

2)下载dol的配置文件

上回书说已经安装了需要的编译环境，这里就下载配置文件。配置文件是dol环境的压缩包，压缩的信息就是dol文件本身。而编译环境则是将压缩信息转化为dol文件的主要手段。

这里的配置文件从网上下载，所以使用wget，下载的信息也不是如同apt-get一样直接就在terminal中安装，而是有一个实实在在的压缩包出现在目录中。

两条语句：

sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz

sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

3)解压文件并实现安装

将两个下载的压缩文件解压到新创建的dol文件夹中（dol文件由自己创建）。接下来进行编译以便安装dol软件——但是安装命令只有在特定的文件夹中才能够起效。所以需要我们进入文件夹：~/dol/systemc-2.3.1/objdir中（有就cd进入，没有就创建一个进入）。继而使用命令：

sudo ../configure --disable-async-updates

由于笔者之前安装过了cpp库，这里就非常顺利了，如果各位看官有什么不顺，可能是缺少了什么库，那就恐怕得自己安装了。

这条语句中的configure的意思就是“安装”，这里的安装对象就是后面的信息：“--disable-async-updates”

3)编译systemc

编译，已经安装了一个环境信息，如果不运行，那么这个环境的信息就会存在在你的计算机里，这本身没有什么，但是如果希望它运行，我们就需要编译。编译使得已经存在的文件转换为计算机可以获知的二进制文件，计算机只有在应对二进制文件时，才能够正常运作并输出结果。

cd ~/systemc - 2.3.1 & make install



make，何谓make，make就是编译，就是将已有的信息转化为二进制信息。install则是安装，将软件安装到当前的计算机上。



4)为编译dol准备

修改build_zip.xml文件 找到下面这段话，就是说上面编译的systemc位置在哪里，

<property name="systemc.inc" value="YYY/include"/> 

<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>

YYY表示之前systemc的路径，这里修改文件关联信息，是为了使得编译的时候，关联文件可以互相查询到，事实上，Linux很多的编译过程都是不使用C语言的头文件包含机制的，某些文件中的函数会被默认地编译，这里就是使用了文件关联的机制。

5)编译dol

有过之前的那么多准备，这里我们终于要编译dol的信息了，编译成功之后，就可以正常运行输出需要的信息。

按照我们之前强调过的，命令都是在特定的文件夹内才可以生效，所以在我们编译之前，一定要知道编译的路径：

cd ~/dol/dol_ethz/build/bin/main

之后使用我们之前配置过的编译环境ant，就是那个编译工具，对已有的信息进行编译：

sudo ant -f build_zip.xml all

这时候，看到编译成功的字样就可以进行第一个样例测试了。

2.实验结果

sudo ant -f runexample.xml -Dnumber=1





3.实验心得

<font size = 3>

本次实验主要任务是对dol的环境进行安装处置，并没有什么困难，安装中安装的Java.jdk包不能使用openjdk-7-jdk，第7版中的编译语言有不能编译的地方，笔者采用第8版Java编译库，可以顺利编译。</font>
