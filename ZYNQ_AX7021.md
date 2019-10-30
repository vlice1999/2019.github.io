# ZYNQ7000开发平台AX7021开发板学习

## 一、AC7021核心板
### （一）简介
核心板主要由ZYNQ7020 + 2个DDR3 + eMMc + QSPI Flash的最小系统构成，承担ZYNQ系统的高速数据处理和存储功能，ZYNQ7020和
两片DDR3之间的数据位宽为32位，两片DDR3容量高达1GB。32GB的eMMC FLASH存储芯片和256Mb的QSPI FLASH
用来静态存储 ZYNQ 的操作系统、文件系统及用户数据，用户可以通过核心板上的拨码开关
来选择不同的启动方式。ZYNQ7020 芯片可分成处理器系统部分 Processor System（PS）和
可编程逻辑部分 Programmable Logic（PL）。
### （二）ZYNQ芯片
芯片的 PS 系统集成了两个 ARM Cortex™-A9 处理器，AMBA®互连，内部存储器，外部存储
器接口和外设。这些外设主要包括 USB 总线接口，以太网接口，SD/SDIO 接口，I2C 总线接
口，CAN 总线接口，UART 接口，GPIO 等。PS 可以独立运行并在上电或复位下启动。


其中 PS 系统部分的主要参数如下：


- 基于 ARM 双核 CortexA9 的应用处理器，ARM-v7 架构 高达 1GHz


- 每个 CPU 32KB 1 级指令和数据缓存，512KB 2 级缓存 2 个 CPU 共享


- 片上 boot ROM 和 256KB 片内 RAM


- 外部存储接口，支持 16/32 bit DDR2、DDR3 接口


- 两个千兆网卡支持：发散-聚集 DMA ，GMII，RGMII，SGMII 接口


- 两个 USB2.0 OTG 接口，每个最多支持 12 节点


- 两个 CAN2.0B 总线接口


- 两个 SD 卡、SDIO、MMC 兼容控制器


- 2 个 SPI，2 个 UARTs，2 个 I2C 接口


- 4 组 32bit GPIO，54（32+22）作为 PS 系统 IO，64 连接到 PL


- PS 内和 PS 到 PL 的高带宽连接


其中 PL 逻辑部分的主要参数如下：


- 逻辑单元 Logic Cells：85K； - 查找表 LUTs: 53,200


- 触发器(flip-flops):106,400


- 乘法器 18x25MACCs：220; - Block RAM：4.9Mb； 


- 两个 AD 转换器,可以测量片上电压、温度感应和高达 17 外部差分输入通道，1MBPS

## DDR3 DRAM 
