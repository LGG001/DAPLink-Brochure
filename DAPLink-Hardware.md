## 官方DAPLink硬件  

官方DAPLink硬件是开源的，开源地址 :point_right: [Github](https://github.com/ARMmbed/mbed-HDK)

目前成熟的DAPLink硬件方案有三个，分别是位于mbed-HDK\Production Design Projects\ARM-mbed\DAPLink目录下的：
* DIPDAP
* STDAP
* SWDAP


### DIPDAP  

![here](http://uk.rs-online.com/largeimages/R9054100-01.jpg "DIPDAP-mbed")

DIPDAP是基于NXP LPC11U35为核心，支持CMSIS-DAP接口、拖拽式下载、虚拟串口等功能，DIAPDAP硬件包括以下内容：
* Eagle原理图和板子文件*（注：Eagle是PCB Layout软件）*
* PDF版原理图和板子副本文件
* Gerber生产文件
* BOM（材料清单）
* eBOM（一份网上购物清单，方便购买！）

通过DIPDAP提供的硬件材料，用户可以轻松的制作一个，如果嫌麻烦可以在网上购买成品， :point_right: [购买地址](http://uk.rs-online.com/web/p/processor-microcontroller-development-kits/9054100/)


### STDAP

STDAP是基于ST STM32F103CBT6为核心，支持CMSIS-DAP接口、拖拽式下载、虚拟串口等功能，DIAPDAP硬件包括以下内容：
* Eagle原理图和板子文件*（注：Eagle是PCB Layout软件）*
* PDF版原理图和板子副本文件
* Gerber生产文件
* BOM（材料清单）
* eBOM（一份网上购物清单，方便购买！）

***需要注意的是，目前官方的DAPLink固件中并没有支持STDAP的固件***


### SWDAP

![here](http://uk.rs-online.com/largeimages/R9054104-01.jpg "SWDAP-mbed")

DIPDAP是基于NXP LPC11U35为核心，支持CMSIS-DAP接口、拖拽式下载等功能，DIAPDAP硬件包括以下内容：
* Eagle原理图和板子文件*（注：Eagle是PCB Layout软件）*
* PDF版原理图和板子副本文件
* Gerber生产文件
* BOM（材料清单）
* eBOM（一份网上购物清单，方便购买！）

通过DIPDAP提供的硬件材料，用户可以轻松的制作一个，如果嫌麻烦可以在网上购买成品， :point_right: [购买地址](http://uk.rs-online.com/web/p/processor-microcontroller-development-kits/9054104/)


## 技新DAPLink硬件  

![技新DAPLink](/Images/DAPLink-JX01.jpg)

技新DAPLink参考官方DIPDAP硬件设计，以NXP LPC11U35为核心，支持CMSIS-DAP接口、拖拽式下载、虚拟串口等功能。技新DAPLink设计采用[**LCEDA**](https://lceda.cn/)，元器件在[**立创商城**](https://www.szlcsc.com/)平台采购，PCB在[**嘉立创**](https://www.sz-jlc.com/home/index.html#)平台生产。技新DAPLink也是开源的，包括：
* Gerber文件，可直接打样生产
* PCB文件、原理图文件
* BOM（元器件采购清单）

![技新DAPLink-BOM](/Images/DAPLink-BOM.png)

技新DAPLink的设计主要是为了解决以下问题：
* 官方DAPLink硬件在国内购买比较麻烦
* 官方DAPLink硬件的BOM中的元器件国内购买比较麻烦
* 提供一个官方DAPLink设计参考
* 提供一个官方DAPLink方案验证
* 作为小册的硬件实验使用

*技新DAPLink硬件地址 :point_right: [DAPLink_JX](https://lceda.cn/jixin002/daplink_jx)*   
*技新DAPLink购买地址 :point_right: [淘宝](https://item.taobao.com/item.htm?spm=a1z38n.10677092.0.0.53701debuPoaU9&id=575455906543)*  
*技新DAPLink开源地址 :point_right: [码云](https://gitee.com/jixiaoxin/DAPLink-Brochures)*


## 本章小结  

本章内容主要介绍了官方的DAPLink硬件以及技新DAPLink硬件，并且都是开源的，用户可以根据提供的资料自己制作或者到相应的网站上购买，同时DAPLink硬件也是作为DAPLink固件的载体，为下一章验证测试DAPLink固件做准备


