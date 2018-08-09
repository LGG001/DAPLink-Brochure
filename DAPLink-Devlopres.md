
## Windows工具安装

本章介绍在Windows下的DAPLink开发环境搭建。安装的工具列表如下，如果有些工具已经安装好可以跳过（*注意：软件安装包尽量选择最新版，选择适合自己电脑的32/64位安装包*）

* **Python2**，版本2.7.9以上，并添加环境变量 :point_right:[下载地址](https://www.python.org/downloads/)
* **Git**，并添加环境变量 :point_right:[下载地址](https://git-scm.com/downloads)
* **Keil MDK-ARM** :point_right:[下载地址](https://www.keil.com/download/product/)  
*注意：软件安装时尽量使用默认路径*



## 获取源码&生成MDK工程

*将需要的的工具安装完成后，点击鼠标右键，选择**Git Bash Here**打开Git命令行界面，按以下步骤输入命令进行操作*  
<!-- ![Git Bash](/DAPLink-Brochure/Images/DAPLink3.png) -->


1. 下载DAPlink源码到本地
```
$ git clone https://github.com/mbedmicro/DAPLink
```

2. 切换到DAPLink目录下
```
$ cd DAPLink
```

3. 安装虚拟环境
```
$ pip install virtualenv
```

4. 进入拟环境
```
$ virtualenv venv
```

5. 启动虚拟环境下的脚本
```
$ venv/Scripts/activate
```

6. 安装requirements.txt表中的工具
```
$ pip install -r requirements.txt
```

7. 生成MDK工程
```
$ progen generate -t uvision
```
*关闭Git命令行界面，在DAPlink目录下有个projectfiles文件夹，里面就是生成的MDK工程，可使用MDK-ARM工具打开*


## 编译源码

1. 打开*DAPLink\projectfiles\uvision*目录下的工程，如*lpc11u35_lpc812xpresso_if*工程，如弹出**Using an MDK Version 4 Project**窗口，选择**Migrate to Device Pack**  
<!-- ![Using an MDK Version 4 Project](/DAPLink-Brochure/Images/DAPLink1.png) -->

2. 此时会打开**Pack Install**窗口并自动下载安装相应的固件包，等待安装完成并关闭  
<!-- ![Pack Install](/DAPLink-Brochure/Images/DAPLink4.png) -->

3. 编译工程，在lpc11u35_lpc812xpresso_if\build目录会生成.bin和.hex文件  
<!-- ![Compile](/DAPLink-Brochure/Images/DAPLink2.png) -->


## 其他问题&解决方法

* **编译源码**的第1步中提示的问题是因为MDK-ARM版本问题引起，可安装对应MDK-ARM的MDK4兼容包解决 :point_right:[下载地址](http://www2.keil.com/mdk5/legacy)
* **编译源码**的第2步中如果提示找不到LPC11U35型号，可在**Pack Install**窗口搜索`LPC1100`并安装LPC1100 Series固件包；或者在KEIL官网下载安装LPC1100 Series固件包 :point_right:[下载地址](http://www.keil.com/dd2/Pack/)
* 工程目录*projectfiles\uvision\*下的文件，以`_if`结尾的工程是对应工程的应用程序；`_bl`结尾的是对应工程的Bootloader应用程序，LPC11U35自带Bootloader程序


## 本章小结

本章内容介绍DAPLink开发环境的搭建，并在搭建好的环境中下载并生成MDK工程，然后使用MDK编译官方的源码生成.bin和.hex文件。通过本章内容可以了解官方源码开发的环境以及使用，后面会介绍DAPLink官方提供的硬件版本，并在其上面烧录本章编译生成的固件

