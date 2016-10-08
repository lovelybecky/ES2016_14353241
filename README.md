#1.Distributed Operation Layer : 
**The distributed operation layer (DOL) **is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.

The distributed operation layer (DOL) is a framework that enables the (semi-) automatic mapping of applications onto the multiprocessor SHAPES architecture platform. The DOL consists of basically three parts:

* **DOL Application Programming Interface:** The DOL defines a set of computation and communication routines that enable the programming of distributed, parallel applications for the SHAPES platform. Using these routines, application programmers can write programs without having detailed knowledge about the underlying architecture. In fact, these routines are subject to further refinement in the hardware dependent software (HdS) layer.
* **DOL Functional Simulation:** To provide programmers a possibility to test their applications, a functional simulation framework has been developed. Besides functional verification of applications, this framework is used to obtain performance parameters at the application level.
* **DOL Mapping Optimization:** The goal of the DOL mapping optimization is to compute a set of optimal mappings of an application onto the SHAPES architecture platform. In a first step, XML based specification formats have been defined that allow to describe the application and the architecture at an abstract level. Still, all the information necessary to obtain accurate performance estimates is contained.

#2.Insatll DOL
####1.安装一些必要的环境(ubuntu为例)：
`$	sudo apt-get update
 $	sudo apt-get install ant
 $ 	sudo apt-get install openjdk-7-jdk
 $	sudo apt-get install unzip`
####2.下载解压DOL和systemc文件到虚拟机中
sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

* 新建dol的文件夹 
`$	mkdir dol`
* 将dolethz.zip解压到 dol文件夹中
`$	unzip dol_ethz.zip -d dol`
* 解压systemc
`$	tar -zxvf systemc-2.3.1.tgz`

####3.编译systemc
* 解压后进入systemc-2.3.1的目录下
`$	cd systemc-2.3.1`
* 新建一个临时文件夹objdir
`$	mkdir objdir`
* 进入该文件夹objdir
`$	cd objdir`
* 运行configure(能根据系统的环境设置一下参数，用于编译)
`$	../configure CXX=g++ --disable-async-updates`
下图为运行configure之后的截图：
![](http://upload-images.jianshu.io/upload_images/3234380-73057a993f0b2abb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 编译
`$	sudo make install`
编译完后文件目录如下($ cd ..   $ ls)，能看到include, lib-linux(对于64位系统，这里是lib-linux64)
![](http://upload-images.jianshu.io/upload_images/3234380-af144599dc93ad95.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 记录当前的工作路径(会输出当前所在路径，记下来，待会有用)
`$	pwd`
![](http://upload-images.jianshu.io/upload_images/3234380-12740dbc7f25cc7b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
####4.编译DOL
* 进入刚刚dol的文件夹
`$	cd ../dol`
* 修改build_zip.xml文件
找到下面这段话，就是说上面编译的systemc位置在哪里，
><property name="systemc.inc" value="YYY/include"/>
<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>

 把YYY改成上页pwd的结果
* 然后进行编译
`$	ant -f build_zip.xml all`
若成功会显示build successful
* 接着试运行第一个例子，进入build/bin/mian路径下
`$	cd build/bin/main`
* 然后运行第一个例子
`$	ant -f runexample.xml -Dnumber=1`
成功结果如图
![](http://upload-images.jianshu.io/upload_images/3234380-c7dc79cf1ab7d21d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**若最后显示成功结果，则完成了DOL的配置安装。**

#3.实验感想
   本次试验初次了解了DOL的基本含义和框架。并在虚拟机上安装配置了DOL。安装配置过程中，需要注意安装环境一定要配置安装正确才能保证后面DOL的安装不会出错。还有输入的每一条命令要仔细认真检查好，不要出现拼写和字符等错误导致安装失败。本次试验较容易，只要按照正确的步骤就可以成功的完成。期待下一次试验对DOL有更进一步的了解。
