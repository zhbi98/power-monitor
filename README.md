# Elecal 迷你 USB 电源功率计

## 1. 项目简介

Elecal 是我设计的一个 Mini-USB 电源功率计，设计包含外观结构，电路 PCB，程序固件。

Elecal 在硬件设计上支持同时采样被测电源的电压，电流及功率等参数，同时通过软件的形式实现了电能实时监测功能。

电能实时监测功能可以方便的知道被监测电源所输出的电能。 比如通过 Elecal 可以知道充电宝为手机充电时，充电宝流入手机的电能为多少 mAh。

而其中 mAh 表明的是电能单位，例如以 $x$ mA 电流持续输出 $1$ h 时间，则输出的电能为 $x$ mAh。

## 2. 硬件介绍

**(1)** 微控制器：采用国产兆易 GD32F103RCT6，芯片主频 96MHz 最高可达 108MHz，64P 引脚，RAM 空间 64KB，ROM 空间 256KB，支持 USB 通信。

**(2)** 屏幕：驱动芯片 ST7789V3，材质 IPS，采用 8 位并行 8080 通信接口，分辨率 320x170。

**(3)** Flash 芯片：GD25Q64 64MBit 即 8MByte。

**(4)** 电压电流采样芯片：采用德州仪器 TI 的 INA226AIDGSR 芯片。 

**(5)** 外壳模型：3D 打印，材料使用尼龙或工程塑料 。

## 3. 目录说明

### 3.1 firmware 目录

该目录包含 Elecal 的所有功能源码实现，芯片驱动库，以及 Keil 编译工程所在目录，现在来简单介绍一下。
mdk5/ 目录即为 MDK-ARM（即 Keil5 集成开发环境） 的工程文件。

test/ 目录包含所有功能实现源码，以及需要用到的芯片驱动库，图形界面库 LVGL。

程序主要包含以下内容：

**(1)** GD32f103 的 USB Device 设备驱动，USB 驱动使用的设备描述符是 CDC 虚拟串口，使用 USB 接口可以用于和上位机进行数据通讯。

**(2)** ST7789V3 屏幕芯片驱动。

**(3)** 电压电流采样芯片驱动。

**(4)** 移植好的 LVGL8.2.0 的 UI 绘图库，这个 UI 库可以实现美观的图形界面，使用 LVGL 后就不需要我们自己控制屏幕逐像素的绘制图形来实现 UI 了。

注意：如果需要编译此工程需要安装 keil5 集成开发环境，以及在 keil5 中安装 GD32F10 系列的芯片描述包, 安装好后点击本项目工程文件夹下的工程文件启动 keil 直接编译即可**。

GD32F10 芯片描述包可以到兆易官方网站下载，找到 **GD32F1x0 AddOn** 压缩包，芯片描述包就在该压缩包下，下载地址：[点击这里](https://www.gd32mcu.com/cn/download/7?kw=GD32F1)。

---

Firmware.hex：Elecal 的编译固件，如果使用编译固件，需要使芯片进入 BOOT 模式，并使用预留的串口来写入该固件。

### 3.2 hardware 目录

Elecal 的 PCB 工程源文件，该文件夹下包含电路原理图，以及 PCB 制造文件（即 Gerber 文件），器件 BOM 单（用于 SMT 贴片），器件位置文件（用于 SMT 贴片）。

将 Gerber 文件压缩后到嘉立创网站下单即可将 PCB 打样出来，BOM 单和器件位置文件是嘉立创格式，PCB 打样后可以自行按照 BOM 单购买元器件手工焊接，或利用我提供的 BOM 单和器件坐标文件运用嘉立创的 SMT 贴片服务来贴片。

硬件 PCB 已经打样验证通过，想制作的小伙伴可以放心打样使用。

---

PCB 设计时原本的设想是使用 **STM32F103RCT6** 这颗芯片作为微控制器使用的，但是奈何 **STM32F103RCT6** 价格较高，所以最终芯片使用的是国产兆易的 **GD32F103RCT6**。

但是这对电路并不影响，因为 **GD32F103RCT6** 可以不需要任何改动而实现 PIN 对 PIN 的引脚以及外设兼容 **STM32F103RCT6** 芯片。

### 3.3 image 目录

该目录是功率计制作实物效果图片展示，观看制作效果可以查看该目录下的实物照片。

### 3.4 structure 目录

该目录存放功率计外壳模型文件 `.step` 格式，外壳模型包含壳体，按键帽，屏幕支架，上盖板，直接下载用于 3D 打印即可。

为了美观考虑盖板最好使用透明亚克力板进行制作，普通 3D 打印无法实现透明。

**(1)** 壳体  elecal_button1_v2.0.step 建议采用黑色尼龙材材料 3D 打印。

**(2)** 屏幕支架 elecal_bracket_V2.0.step 建议采用透明树脂材料 3D 打印。

**(3)** 上盖板 elecal_panel_V2.0.step 建议采用亚克力或聚碳酸酯材料 CNC 加工。

**(4)** 按键帽 elecal_button1_v2.0.step ，elecal_button2_v2.0.step
elecal_button3_v2.0.step，elecal_button4_v2.0.step 建议采用尼龙材料 3D 打印。

## 4. 外观设计

**最初的 V1.0 版本模型效果**

![Elecal_v1.0](./image/Elecal_v1.0.png)

**改进后 V2.0 版本模型效果**

![Elecal_v2.0](./image/Elecal.png)

## 5. 实物展示

![Elecal_v2.0](./image/Elecal_Model.jpg)
