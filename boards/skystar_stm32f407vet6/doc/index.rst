.. zephyr:board:: skystar_stm32f407vet6

概述
********

LCKFB 天空星 STM32F407VET6 核心板，主控为 STM32F407VET6
（ARM Cortex-M4，LQFP100，最高 168 MHz，512 kB Flash，192+4 kB SRAM）。
核心板通过 P1/P2 排针引出可用 IO。

核心板专用资源
==============

.. list-table::
   :header-rows: 1

   * - 资源
     - 引脚
     - 说明
   * - 用户 LED
     - PB2
     - 低电平点亮
   * - 调试串口 USART1
     - PA9 / PA10
     - TX / RX，默认 115200
   * - USB FS
     - PA11 / PA12
     - USB_DM / USB_DP
   * - SWD
     - PA13 / PA14
     - SWDIO / SWCLK
   * - SWO
     - PB3
     - TRACESWO
   * - HSE
     - PH0 / PH1
     - 8 MHz 晶振
   * - LSE
     - PC14 / PC15
     - 32.768 kHz RTC 晶振

P1/P2 排针
==========

.. list-table::
   :header-rows: 1
   :widths: 12 18 12 18

   * - P1 针
     - MCU 引脚
     - P2 针
     - MCU 引脚
   * - 1
     - PA2
     - 1
     - PD3
   * - 2
     - REF
     - 2
     - PC9
   * - 3
     - PA0
     - 3
     - PC8
   * - 4
     - PA1
     - 4
     - PC12
   * - 5
     - PA4
     - 5
     - PD2
   * - 6
     - PA3
     - 6
     - PC11
   * - 7
     - PA6
     - 7
     - PC10
   * - 8
     - PA5
     - 8
     - PC13
   * - 9
     - PC4
     - 9
     - PE6
   * - 10
     - PA7
     - 10
     - PE5
   * - 11
     - PB0
     - 11
     - PE4
   * - 12
     - PC5
     - 12
     - PE3
   * - 13
     - PE7
     - 13
     - PE2
   * - 14
     - PB1
     - 14
     - PC0
   * - 15
     - PE9
     - 15
     - PC1
   * - 16
     - PE8
     - 16
     - PC2
   * - 17
     - PE11
     - 17
     - PC3
   * - 18
     - PE10
     - 18
     - PE1
   * - 19
     - PE13
     - 19
     - PE0
   * - 20
     - PE12
     - 20
     - PB9
   * - 21
     - PE15
     - 21
     - PB8
   * - 22
     - PE14
     - 22
     - PB7
   * - 23
     - PB10
     - 23
     - PB6
   * - 24
     - PB11
     - 24
     - PB5
   * - 25
     - PB13
     - 25
     - PB4
   * - 26
     - PB12
     - 26
     - BAT
   * - 27
     - PB15
     - 27
     - PD7
   * - 28
     - PB14
     - 28
     - PD6
   * - 29
     - PD9
     - 29
     - PD5
   * - 30
     - PD8
     - 30
     - PD4
   * - 31
     - PD11
     - 31
     - PD1
   * - 32
     - PD10
     - 32
     - PD0
   * - 33
     - PD13
     - 33
     - PA15
   * - 34
     - PD12
     - 34
     - PA8
   * - 35
     - PD15
     - 35
     - PC6
   * - 36
     - PD14
     - 36
     - PC7
   * - 37
     - AGND
     - 37
     - GND
   * - 38
     - 3V3
     - 38
     - 3V3
   * - 39
     - GND
     - 39
     - GND
   * - 40
     - 5V0
     - 40
     - 5V0

.. note::

   P1/P2 的针脚编号按立创官方速查表整理，只保留 MCU 引脚定义。
   实际使用前请以核心板原理图和丝印为准。

系统时钟
========

系统时钟由 8 MHz HSE 经 PLL 倍频到 168 MHz；RTC 使用 32.768 kHz LSE。

编程与调试
**********

.. zephyr:board-supported-runners::

烧录
====

.. code-block:: console

   west build -p always -b skystar_stm32f407vet6 samples/basic/blinky
   west flash

默认使用 OpenOCD + CMSIS-DAP，也支持：

.. code-block:: console

   west flash -r openocd
   west flash -r pyocd
   west flash -r jlink
   west flash -r dfu-util
