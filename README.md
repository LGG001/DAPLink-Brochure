## 小册介绍

ARM Cortex内核的MCU在市场上的产品随处可见，如Cortex M系列内核的有：ST公司的STM32系列MCU产品、NXP公司的LPC系列MCU产品、国产的MM32系列MCU产品、GD32系列MCU产品等等，目前它们的年出货量是以亿为单位。不管是在校的电子专业相关的学生或是在职工程师，掌握一款Cortex内核的MCU是非常有必要的。

Cortex 内核中带有特定的下载调试单元（如Cortex M中的CMSIS接口），可以通过JTAG或SWD接口进行程序调试下载，也就需要带一个JTAG或SWD接口的下载器。目前市场上比较好用的下载器有两种：J-LINK、ST-LINK，但是它们的价格昂贵而且带有版权。DAPLink是ARM官方开源的下试器，具备JTAG和SWD两种接口，同时还带虚拟串口，拖拽式下载等功能。**本小册讲述如何制作一个官方的DAPLink下载器**

### 本小册能学到哪些知识

* 认识DAPlink
* 从零制作一个官方DAPLink
* DAPLink的使用

### 适宜人群

* 对DAPLink感兴趣的开发者
* 想制作一个DAPLink下载器的电子工程师
* 具备一定动手能力的电子工程师
* 有一台Windows电脑的电子工程师
* 有一点单片机编程基础的电子工程师


## 章节介绍

* **[第一章 DAPLink简介](第一章 DAPLink简介.md)**
>DAPLink简介  
>DAPLink功能介绍  
>DAPLink官方介绍  
>本章小结  

* **[第二章 DAPLink开发环境搭建](第二章 DAPLink开发环境搭建.md)**
>Windows工具安装  
>获取源码&生成MDK工程  
>编译源码  
>其他问题&解决方法  
>本章小结  

* **[第三章 DAPLink硬件设计](第三章 DAPLink硬件设计.md)**
>官方DAPLink硬件  
>技新DAPlink硬件  
>本章小结  

* **[第四章 DAPLink配置与应用](第四章 DAPLink配置与应用.md)**
>DAPLink固件更新  
>DAPLink在ARM-MDK中的使用  
>DAPLink的MSD命令使用  
>DAPLink其他功能介绍  
>本章小结  

### 章节预览
![技新DAPLink](/Images/DAPLink-design.png)



