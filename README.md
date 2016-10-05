## Read Me ##

### Description ###

**The distributed operation layer (DOL)** is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.

### How To Install ###

* 安装必要环境
   ``` 
$ sudo apt-get update
$ sudo apt-get install ant
$ sudo apt-get install openjdk-7-jdk
$ sudo apt-get install unzip
   ```

* 下载文件
   ```
$ sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
$ sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
   ```

* 解压文件 
 - 新建dol的文件夹

    ` $ mkdir dol `
 - 将dolethz.zip解压到 dol文件夹中

    ` $ unzip dol_ethz.zip -d dol `
 - 解压systemc

    ` $ tar -zxvf systemc-2.3.1.tgz `

* 编译systemc
 - 解压后进入systemc-2.3.1的目录下

    ` $ cd systemc-2.3.1 `
 - 新建一个临时文件夹objdir

 	` $ mkdir objdir `
 - 进入该文件夹objdir

 	` $ cd objdir `
 - 运行configure(能根据系统的环境设置一下参数，用于编译)

 	` $ ../configure CXX=g++ --disable-async-updates `

   	下图为运行configure之后的截图

   	![](https://github.com/nickxiaowei/markdownpicture/raw/master/lab1_picture1.png)
 - 编译

 	` $ sudo make install `

   	编译完后文件目录如下(`$ cd ..`        `$ ls`)

   	![](https://github.com/nickxiaowei/markdownpicture/raw/master/lab1_picture2.jpg)

 - 记录当前的工作路径(会输出当前所在路径，记下来，待会有用)

 	` $ pwd `

   	![](https://github.com/nickxiaowei/markdownpicture/raw/master/lab1_picture3.png)

   	这里表示我当前的工作路径为**/home/liuxiaowei/systemc-2.3.1**

* 编译dol
 - 进入刚刚dol的文件夹
 
    ` $ cd ../dol `
 - 修改build_zip.xml文件
   找到下面这段话，就是说上面编译的systemc位置在哪里

   	> property name="systemc.inc" value="YYY/include"/
   	> property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/

   	把YYY改成上页pwd的结果（注意，**对于64位系统的机器，lib-linux要改成lib-linux64**）
 - 然后是编译
 
   ` $ ant -f build_zip.xml all `
若成功会显示**build successful**
 - 然后试着运行第一个例子
   
   ``` 
   $ cd build/bin/main
   $ ant -f runexample.xml -Dnumber=1
   ```
   成功结果如下图

   		![](https://github.com/nickxiaowei/markdownpicture/raw/master/lab1_picture4.png)

### Experimental experience ###
* **lab1**

 这次实验的话，虽然上个学期的操作系统课已经配置过一次Ubuntu了，也不是不可以直接用之前配置过的Ubuntu来完成这次的实验，但是为了之前配置的印象已经比较浅了，所以我选择了重新配置一次Ubuntu，还好，由于有过经验和印象，做的过程还是比较轻松愉快的，整个做的过程并没有出现什么大的问题，不过做到运行configure查看系统参数的时候，由于是新配置的虚拟机，还没有安装过gcc，所以C++编译器出现了问题，除此之外照着PPT做的过程都很顺利。