## DAPLink固件更新

DAPLink固件由两个部分组成
* 以xxx_bl结尾的.bin文件（Bootloader）
* 以xxx_if结尾的.bin文件（应用程序）

NXP的LPC11U35是自带Bootloader，原装的LPC11U35芯片首次上电时就会自动进入Bootloader，虚拟出一个U盘设备，然后将以应用程序拖进去即可完成烧录，之后就会自动运行应用程序

### 技新DAPLink固件更新

1. 按住K1（或短接nRST和GND）插入电脑就会识别出一个`CRP DISABLD`U盘设备，里面有一个`firmware.bin`文件，将其删除
2. 把第二章的编译产生的DAPLink固件**`lpc11u35_lpc812xpresso_if_crc.bin`**（固件位于DAPLink\projectfiles\uvision\lpc11u35_lpc812xpresso_if\build目录下）拖（复制）到U盘中
3. 将DAPLink重新插拔一次（不需要按住K1或短接nRST和GND），就会看到一个`DAPLINK`U盘设备，固件更新完毕

固件更新后，`DAPLINK`内有DETALLS.TXT和MBED.HTM两个文件，MBED.HTM是一个网页，DETALLS.TXT是该DAPLink固件的相关信息：
```
# DAPLink Firmware - see https://mbed.com/daplink
Unique ID: 105000001781cdaa00000000000000000000000097969902
HIC ID: 97969902
Auto Reset: 0
Automation allowed: 0
Overflow detection: 0
Daplink Mode: Interface
Interface Version: 0247
Git SHA: 7574bed494828d1da9a170d4f2727bba28362eaf
Local Mods: 0
USB Interfaces: MSD, CDC, HID, WebUSB
Interface CRC: 0x7ba4edb8
Remount count: 0
URL: https://mbed.org/device/?code=105000001781cdaa00000000000000000000000097969902?version=0247?target_id=@T
```

DAPLink插入电脑后会识别出如下设备（如果有部分设备无法识别请检查系统驱动是否有问题）：
* MSD--USB大容量存储设备（拖拽式下载）
* CDC--mbed Serial Port（虚拟串口）
* HID--符合HID标准的供应商定义设备/USB输入设备（CMSIS-DAP接口）
* WebUSB：CMSIS-DAP或USB_DFU
*注：W7和W8系统的CDC驱动需要手动安装，:point_right: [驱动地址](http://os.mbed.com/media/downloads/drivers/mbedWinSerial_16466.exe)*


### 其他DAPLink固件更新

LPC11U35本身自带Bootloader，所以只需要Bootloader的MMSD接口把固件烧录进去即可，对于本身没有自带Bootloader功能的，需要先往里先烧录Bootloader。DAPLink的固件源码编译生成的工程，对于LPC11U35之外没有Bootloader功能的DAPLink硬件提供了Bootloader固件，如DAPLink\projectfiles\uvision目录下的`k20dx_bl`工程就是`k20dx`的Bootloader


## DAPLink在ARM-MDK中的使用

DAPLink的CMSIS-DAP接口是用于ARM Cortex内核MCU调试仿真的，只要IDE支持CMSIS-DAP协议接口即可使用DAPLink，这里以ARM-MDK为例，其他的IDE也类似使用，调试仿真使用的是DAPLink的CMSIS-DAP接口功能

1. DAPLink作为仿真器连接目标设备，如STM32F103C8T6最小系统板
2. 打开STM32F103C8T6的ARM-MDK例程
3. 打开Options for Target选项，在Debug栏下的Use选项选择CMSIS-DAP Debugger
4. 点击Settings，Debug栏设置如下图，点击OK完成配置，之后即可编译下载/调试

![技新DAPLink](/Images/DAPLink-MDK1.png)


## DAPLink的MSD命令使用

DAPLink允许通过MSD接口来给它一些简单的命令。复制一个指定命名的文件通过MSD接口到DAPLink，可以使DAPLink执行一个动作或一个永久有效配置，文件的内容可以被忽略（可以发送一个空文件）

MSD的命令只有在下面状态下才有效
* 插入DAPLink，再按住K1，然后把相应的.act或.cfg文件复制到MSD接口
* 在打automation-allowed模式下，把相应的.act或.cfg文件复制到MSD接口

MSD命令有两种
* .act文件，触发DAPLink一个Action（动作）
* .cfg文件，配置DAPLink一个Configuration（设置）


### Action命令

`start_bl.act` 该文件将强制进入Bootloader，相当于拔下DAPLink，按住K1再插上。如果DAPlink已经处于Bootloader，则该命令无效

`start_if.act` 该文件将强制DAPLink重新进入DAPLink接口模式。它相当于拔下USB电缆，并将其插入。如果已经处于DAPLink接口模式，则此命令无效

`assert.act` 该文件可以用来测试DAPLink的assert实用程序。当您将该文件复制到DAPLink MSD驱动器时，DAPLink将生成对util_assert()方法的调用。assert调用导致DAPLink MSD驱动器重新加载一个附加文件ASSERT.TXT，出现在驱动器的根部。这个文件详细说明了断言失败发生的地方(源文件，行号)

`refresh.act` 该文件强制重新加载DAPLink MSD驱动器

`erase.act` 该文件触发对目标FLASH的擦除


### Configuration命令

`auto_rst.cfg` 该文件用于配置自动复位模式，默认情况下自动复位是禁止的

`hard_rst.cfg` 该文件用于关闭自动复位模式，默认情况下自动复位是禁止的

`auto_on.cfg`  该文件用于打开automation-allowed模式，再该模式下可以出发DAPLink的MSD命令，而不需要按住K1案件。此外，Bootloader更新只允许再该模式下运行

`auto_off.cfg` 该文件用于关闭automation-allowed模式，automation-allowed模式默认是关闭的

`ovfl_on.cfg` 该文件用于打开串口溢出报告。再串口通讯过程中，如果主机PC没有以足够快的速度从DAPLink读取数据，并且发生溢出，则文本<DAPLink: overflow >将出现在串行数据中。串行溢出报告默认关闭

`ovfl_off.cfg` 该文件用于关闭串口溢出报告


### MSD命令使用

1. 使能automation-allowed模式。新建文本文档并重命名为`auto_on.cfg`，插入DAPLink并按按K1，然后把auto_on.cfg文件拷贝进DAPLink的MSD接口（虚拟U盘），这时DAPLink的MSD会重启，在根目录的DETAILS.TXT文件中`Automation allowed: 1; Remount count: 1`
```
# DAPLink Firmware - see https://mbed.com/daplink
Unique ID: 105000001781cdaa00000000000000000000000097969902
HIC ID: 97969902
Auto Reset: 0
Automation allowed: 1
Overflow detection: 0
Daplink Mode: Interface
Interface Version: 0247
Git SHA: 7574bed494828d1da9a170d4f2727bba28362eaf
Local Mods: 0
USB Interfaces: MSD, CDC, HID, WebUSB
Interface CRC: 0x7ba4edb8
Remount count: 1
URL: https://mbed.org/device/?code=105000001781cdaa00000000000000000000000097969902?version=0247?target_id=@T
```

2. 触发一个Action。新建文本文档并重命名为`refresh.act`，将该文档拷贝进DAPLink的MSD接口（虚拟U盘），这时DAPLink的MSD会重启，在根目录的DETAILS.TXT文件中`Automation allowed: 1; Remount count: 2`
```
# DAPLink Firmware - see https://mbed.com/daplink
Unique ID: 105000001781cdaa00000000000000000000000097969902
HIC ID: 97969902
Auto Reset: 0
Automation allowed: 1
Overflow detection: 0
Daplink Mode: Interface
Interface Version: 0247
Git SHA: 7574bed494828d1da9a170d4f2727bba28362eaf
Local Mods: 0
USB Interfaces: MSD, CDC, HID, WebUSB
Interface CRC: 0x7ba4edb8
Remount count: 2
URL: https://mbed.org/device/?code=105000001781cdaa00000000000000000000000097969902?version=0247?target_id=@T
```

3. 配置一个Configuration。新建文本文档并重命名为`refresh.act`，将该文档拷贝进DAPLink的MSD接口（虚拟U盘），这时DAPLink的MSD会重启，在根目录的DETAILS.TXT文件中`Automation allowed: 1; Overflow detection: 1; Remount count: 3`
```
# DAPLink Firmware - see https://mbed.com/daplink
Unique ID: 105000001781cdaa00000000000000000000000097969902
HIC ID: 97969902
Auto Reset: 0
Automation allowed: 1
Overflow detection: 1
Daplink Mode: Interface
Interface Version: 0247
Git SHA: 7574bed494828d1da9a170d4f2727bba28362eaf
Local Mods: 0
USB Interfaces: MSD, CDC, HID, WebUSB
Interface CRC: 0x7ba4edb8
Remount count: 3
URL: https://mbed.org/device/?code=105000001781cdaa00000000000000000000000097969902?version=0247?target_id=@T
```
*注：其他MSD命令使用也如上配置*


## DAPLink其他功能介绍

### CDC虚拟串口

DAPLink带有虚拟串口功能，可用于与目标设备进行串口通讯，使用方法与其他UDB转TTL的模块一样，支持的比特率有：
```
9600
14400
19200
28800
38400
56000
57600
115200
```
*注：大多数DAPLink还支持这里列出来之外的串口通讯波特率*


### MSC拖拽式下载功能

DAPLink带有拖拽式下载功能，但是该功能通常只针对独立的目标设备，如固件`lpc11u35_lpc812xpresso_if_crc.bin`的拖拽式下载是针对lpc812xpresso目标的，如果想支持其他的目标就需要对DAPLink固件进行修改移植， :point_right: [参考文档](https://github.com/ARMmbed/DAPLink/blob/master/docs/PORT_BOARD.md)


### 其他功能

DAPLink还提供了非常多的功能和应用，如自动化测试、添加一个新板支持、添加一个新设备、移植到新的硬件电路等，其中的操作都有独立的文档讲解，本章介绍的固件更新和DAPLink的MSD命令使用也只是其中一部分功能，具体可参考  :point_right: [DAPLink官方文档](https://github.com/ARMmbed/DAPLink/tree/master/docs)

DAPLink的移植部分是一个比较重要也是比较复杂的功能，本小册是属于基础篇，所以就不介绍DAPLink一直部分内容，如果对DAPLink一直感兴趣的可以参考官方的文档说明，或者在后面会单独写一份关于DAPLInk移植的小册


## 本章小结

本章的内容介绍DAPLink如何更新固件、DAPLink在ARM-MDK上的使用、DAPLink的MSD命令使用等。通过本章内容可以了解到DAPLink是一个非常强大的开源仿真器，想详细了解DAPLink建议阅读官方DAPLink相关的文档

小册的内容到此也就结束了，小册比较详细地介绍了DAPLink的软硬件，同时也介绍DAPLink使用，用户可根据本小册的内容自己DIY一个DAPLink，也可以根据小册提供的连接购买一个DAPLink。说起DAPLink也是一种缘分，当初公司项目需求一个Cortex -M的仿真器，但是市场上上常用的J-LINK个ST-LINK都是有版权的，并且价格也是非常昂贵。后来遇见DAPLink（当时还叫CMSIS-DAP），然后再网上搜各种资料，资料比较少（可能因为CMSIS-DAP是国外开源项目，在国内很少人研究），但是也有不少牛人实现CMSIS-DAP的移植，其中网友*X839*在STM32上移植成功了，这也是在网上流行的CMSIS-DAP版本。后来官方把CMSIS-DAP改名为DAPLink，并丰富了很多的资料，使DAPLink逐渐完善起来，支持的设备越来越多，兼容的硬件平台也越来越多，同时提供各种参考资料


