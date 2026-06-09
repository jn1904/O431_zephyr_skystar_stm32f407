.. zephyr:board:: skystar_stm32f407

概述
********

SKYSTAR_STM32F407 开发板搭载基于 ARM Cortex-M4 架构的 STM32F407VET6 MCU，
具备丰富的连接支持与灵活的配置选项。

硬件资源
********

SKYSTAR_STM32F407 开发板提供以下硬件组件：

- STM32F407VET6，LQFP100 封装
- ARM 32 位 Cortex-M4 CPU，带 FPU
- 最高主频 168 MHz
- 8 MHz 系统晶振
- 32.768 kHz RTC 晶振
- JTAG/SWD 调试接口
- 512 kB Flash
- 192+4 kB SRAM，含 64 kB CCM
- 3 路 12 位 ADC，共 24 个通道
- 2 路 12 位 D/A 转换器
- USB 2.0 OTG FS，内置片上 PHY
- 10/100 以太网 MAC，带专用 DMA
- SPI、I2C、UART、CAN、SDIO

有关 STM32F407VE SOC 的更多信息，请参阅：
- `STM32F407VE on www.st.com`_

支持的功能
==================

.. zephyr:board-supported-hw::

默认 Zephyr 外设引脚映射：
------------------------------

- UART_1_TX : PA9
- UART_1_RX : PA10
- UART_2_TX : PA2
- UART_2_RX : PA3
- USER_PB : PA0
- LD1 : PB2
- LD2 : PB8
- USB DM : PA11
- USB DP : PA12

系统时钟
============

系统时钟由 PLL 驱动，频率为 168 MHz，使用 8 MHz HSE 外部振荡器。

编程与调试
*************************

.. zephyr:board-supported-runners::

烧录
========

本开发板通过 SWD 接口使用 DAPLink (CMSIS-DAP) 进行编程和调试，
支持 PyOCD 和 OpenOCD 烧录工具。

构建并烧录应用程序：

.. code-block:: console

   west build -p always -b skystar_stm32f407 samples/basic/blinky
   west flash / ./openocd.sh

或显式指定烧录工具：

.. code-block:: console

   west flash -r pyocd
   west flash -r openocd

.. _STM32F407VE on www.st.com:
   https://www.st.com/en/microcontrollers/stm32f407ve.html
