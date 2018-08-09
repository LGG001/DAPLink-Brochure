## DAPLink简介

DAPLink是ARM官方的一款开源的调试仿真器，之前叫CMSIS-DAP。DAPLink的软件和硬件都在Github上开源：
* DAPLink软件地址 :point_right: [Github](https://github.com/ARMmbed/DAPLink)
* DAPLink硬件地址 :point_right: [Github](https://github.com/ARMmbed/mbed-HDK)

DAPLink目前源码固件主要使用在LPC11U35以及MK20DX128VFM5的硬件上，并在Github上开源，成熟的DAPLink硬件方案有三个：
* DIPDAP（主芯片：LCP11U35FHI33/501）
* STDAP（主芯片：STM32F103CBT6）
* SWDAP（主芯片：LCP11U35FHI33/501）

DAPLink可以对ARM Cortex内核（*如 Cortex M3*）进行仿真调试，并且提供源码和硬件，这样可以使用户可以轻松的集成一个仿真调试器到自己的项目上而无需担心版权问题。DAPLink不仅拥有仿真调试功能，同时它还具备虚拟串口和拖拽式下载功能（*拖拽式下载只支持固件上对应的MCU*）


## DAPLink功能介绍

* MSC-拖拽式下载
* CDC-日志打印、追踪和终端仿真的虚拟串口
* HID-CMSIS-DAP兼容式调试接口
* WEBUSB HID-CMSIS-DAP兼容式调试接口

### MSC拖拽式下载

通过复制或保存一个DAPLink支持的格式文件DAPLink的虚拟U盘中，完成后DAPLink设备就会重启。如果发生错误，错误的信息就会存放在FAIL.TXT中

DAPLink的MSC功能支持的文件格式如下：
* .bin
* .hex


### CDC-日志打印、追踪和终端仿真的虚拟串口

CDC虚拟串口功能具备普通的串口IC功能，串行端口直接连接到目标MCU，允许双向通信。它还允许通过在串行端口上发送中断命令来重置目标。

串口通讯支持的波特率如下：
* 9600
* 14400
* 19200
* 28800
* 38400
* 56000
* 57600
* 115200
*注：大多数DAPLink还支持这里列出来之外的串口通讯波特率*


### HID-CMSIS-DAP兼容式调试接口

CMSIS-DAP接口可以在任何支持CMSISI-DAP协议的IDE中进行调试，其中包括：
* [pyOCD](https://github.com/mbedmicro/pyOCD)
* [uVision](http://www.keil.com/)
* [IAR](https://www.iar.com/)


### WEBUSB HID-CMSIS-DAP兼容式调试接口

WEBUSB HID-CMSIS-DAP是用于网页上进行调试的接口。



## DAPLink官方介绍

[![DAPLink](/Images/DAPLink.png)](https://armmbed.github.io/DAPLink/)

Arm Mbed DAPLink是一个开源软件项目，它能够在Arm Cortex架构上的CPU运行编程和调试应用程序。DAPLink是作为应用MCU的SWD或JTAG接口的辅助型MCU，通常称之为接口固件。这种配置几乎在所有的开发板上都可以看到，DAPLink枚举为一个USB复合设备，为开发者的计算机和CPU调试访问端口之间建立了一个桥梁。DAPLink能让开发者具有：

* MSC-拖拽式编程FLASH闪存
* CDC-日志打印、追踪和终端仿真的虚拟串口
* HID-CMSIS-DAP兼容式调试接口
* WEBUSB HID-CMSIS-DAP兼容式调试接口

更多的功能正在规划兵渐渐展现出来。DAPLink项目不断地在Arm、它的合作伙伴、众多的硬件供应商和世界各地的开源社区的大力开发之下，取代了CMSIS-DAP接口固件项目，你可以尽情使用和贡献。Enjoy!

更多可用的细节信息可查看DAPLink用户指南[DAPLink用户指南](https://github.com/ARMmbed/DAPLink/blob/master/docs/USERS-GUIDE.md)


### 兼容性

DAPLink接口固件已经运行在许多基于ARM微控制器的硬件接口电路（HICs），它们可用作独立的（调试器）板子或作为开发工具的一部分。一些已知的IO兼容品牌的电路如下：
* [NXP OpenSDA based on K20, K22 and KL26](http://www.nxp.com/products/software-and-tools/run-time-software/kinetis-software-and-tools/ides-for-kinetis-mcus/opensda-serial-and-debug-adapter:OPENSDA)
* [NXP LPC-Link2 based on LPC11U35 or LPC4322](https://www.nxp.com/support/developer-resources/hardware-development-tools/lpcxpresso-boards:LPCXPRESSO-BOARDS)
* [Segger J-Link OB based on Atmel SAM3U](https://www.segger.com/products/debug-probes/j-link/models/j-link-ob/)
* Maxim Epsilon based on MAX32550 - coming soon


### 版本

DAPLink官方的Github仓库创建了许多板级构建（板 = HIC + 目标组合）。季度版本将包含新的特性和修复BUG，一旦根据报告、验证并修复BUG，就会发布独立的修复BUG后的版本无论是季度版本还是修复Bug版本，都会导致生成号递增。许多开发工具包和产品与DaPink接口固件一起运行，或者能够运行DaPink固件。当前发布版本和更新DaPink界面固件的指令是在[DaPink发布站点](https://armmbed.github.io/DAPLink/)上托管的。发行说明和以前发布版本可以在GITHUB发行版中找到


## 本章小结  

本章内容介绍了DAPLink的相关信息，包括它的特点、功能、软件、硬件等，在后续章节会通过官方的源码以及硬件来制作一个官方的DAPLink



