.. zephyr:board:: skystar_stm32f407

概述
********

SKYSTAR_STM32F407 是立创开发板的“天空星筑基学习板”，核心 MCU 为
STM32F407VET6（ARM Cortex-M4，LQFP100，最高 168 MHz）。
本文档的引脚分配只以筑基学习板为准。

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
- 以太网 LAN8720A、隔离 CAN、隔离 RS485
- I2C1 六设备总线、I2C2 触摸/外扩总线
- LCD SPI 屏幕 + FT6336 触摸
- WS2812 RGB、蜂鸣器、继电器、电位器
- TF / SDIO、外部 SPI 扩展
- 直流电机、舵机、TMC2209 步进电机
- HX711、单总线、HX711 外扩 ADC

有关 STM32F407VE SOC 的更多信息，请参阅：
- `STM32F407VE on www.st.com`_

支持的功能
==================

.. zephyr:board-supported-hw::

默认 Zephyr 外设引脚映射（按天空星筑基学习板）：
----------------------------------------------------

.. list-table::
   :widths: 22 38 24
   :header-rows: 1

   * - 模块
     - 信号
     - 引脚
   * - 调试串口
     - USART1_TX / USART1_RX
     - PA9 / PA10
   * - 核心板 USB
     - USB_DM / USB_DP
     - PA11 / PA12
   * - 独立串口 2
     - USART2_TX / USART2_RX
     - PD5 / PD6
   * - RS485
     - USART3_TX / USART3_RX / RE_DE
     - PD8 / PD9 / PD15
   * - I2C1（6 个设备）
     - I2C1_SCL / I2C1_SDA
     - PB6 / PB7
   * - I2C2（触摸/外扩）
     - I2C2_SCL / I2C2_SDA
     - PD10 / PE13
   * - SPI2
     - SPI2_SCK / MISO / MOSI
     - PB10 / PC2 / PC3
   * - SPI2 片选
     - Flash CS / IMU CS / 外扩 CS0~2
     - PE4 / PE7 / PD11, PE0, PE15
   * - LCD 屏幕
     - SPI1_SCK / MOSI
     - PA5 / PB5
   * - LCD 控制
     - BL_PWM / CS / DC / RST / TP_INT
     - PB8 / PE14 / PD14 / PE1 / PE2
   * - 绿色 LED / 屏幕背光
     - TIM10_CH1 PWM
     - PB8
   * - 音频 ES8388
     - I2S2_WS / SCK / EXT_SD / SD / MCK
     - PB9 / PB10 / PC2 / PC3 / PC6
   * - 以太网 LAN8720A
     - REF_CLK / MDIO / CRS_DV / MDC / RXD0 / RXD1 / TX_EN / TXD0 / TXD1 / NRST
     - PA1 / PA2 / PA7 / PC1 / PC4 / PC5 / PB11 / PB12 / PB13 / PE12
   * - CAN1
     - CAN1_RX / CAN1_TX
     - PD0 / PD1
   * - TF / SDIO
     - D0 / D1 / D2 / D3 / CK / CMD / DET
     - PC8 / PC9 / PC10 / PC11 / PC12 / PD2 / PD3
   * - 用户按键
     - KEY1 / KEY2 / KEY3(EC11)
     - PA0 / PE8 / PC13
   * - 继电器
     - RELAY
     - PA4
   * - 蜂鸣器（有源/无源二选一）
     - GPIO / TIM13_CH1
     - PA6
   * - WS2812
     - RGB_DATA
     - PA3
   * - 电位器
     - ADC1_IN10
     - PC0
   * - EC11 / 电机 2 编码器
     - TIM4_CH1 / TIM4_CH2
     - PD12 / PD13
   * - 电机 1 编码器
     - TIM3_CH1 / TIM3_CH2
     - PB4 / PC7
   * - 步进电机编码器
     - TIM1_CH1 / TIM1_CH2
     - PE9 / PE11
   * - 直流电机 1
     - AT8236 IN1 / IN2
     - PE5 / PE6
   * - 直流电机 2 / 舵机
     - TIM12_CH1 / TIM12_CH2
     - PB14 / PB15
   * - 步进电机 TMC2209
     - STEP / DIR / EN
     - PA15 / PD4 / PD7
   * - HX711
     - DOUT / PD_SCK
     - PB0 / PB1
   * - 单总线
     - DQ
     - PA8

.. note::

   - 核心板 PB2 为普通 GPIO LED，DTS 中作为 ``led0``。
   - PB8 同时作为绿色 LED 和 LCD 背光，当前 DTS 使用 ``pwm-leds`` 建模。
   - 蜂鸣器 PA6 由 SW7 bit4 选择有源/无源，DTS 默认使能有源蜂鸣器，
     无源 PWM 节点默认关闭。
   - 官方底板使用多路拨码开关在部分复用功能之间切换：
     SPI2/I2S2、蜂鸣器有源/无源、EC11/电机 2 编码器、
     舵机/电机 2、板载 RGB/外部灯条、HX711/ADC 排针等。
     因此同一时刻只能使能其中一路。
   - QDEC 的 ``st,counts-per-revolution`` 需要根据实际编码器 PPR 调整。

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
   west flash

默认烧录器是 OpenOCD + CMSIS-DAP。

也可以显式指定烧录器：

.. code-block:: console

   west flash -r openocd
   west flash -r pyocd
   west flash -r jlink
   west flash -r dfu-util

.. _STM32F407VE on www.st.com:
   https://www.st.com/en/microcontrollers/stm32f407ve.html
