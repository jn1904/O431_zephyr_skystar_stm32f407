# O431_zephyr_skystar_stm32f407

这是一个 Zephyr module，包含两个相关的板级配置：

| Board 名称 | 说明 |
|---|---|
| `skystar_stm32f407` | 天空星 STM32F407VET6 核心板 + 立创筑基学习板底板 |
| `skystar_stm32f407vet6` | 只有天空星 STM32F407VET6 核心板 |

两个 board 都使用相同的 STM32F407VET6 SOC，统一放在同一个 Zephyr module 中维护。

## 目录结构

```text
O431_zephyr_skystar_stm32f407/
├── zephyr/
│   └── module.yml
├── boards/
│   ├── skystar_stm32f407/
│   │   ├── board.yml
│   │   ├── board.cmake
│   │   ├── Kconfig.*
│   │   ├── skystar_stm32f407.dts
│   │   ├── skystar_stm32f407.yaml
│   │   ├── skystar_stm32f407_defconfig
│   │   ├── doc/index.rst
│   │   └── support/openocd.cfg
│   └── skystar_stm32f407vet6/
│       ├── board.yml
│       ├── board.cmake
│       ├── Kconfig.*
│       ├── skystar_stm32f407vet6.dts
│       ├── skystar_stm32f407vet6.yaml
│       ├── skystar_stm32f407vet6_defconfig
│       ├── doc/index.rst
│       └── support/openocd.cfg
└── README.md
```

## 板级说明

### `skystar_stm32f407` — 核心板 + 底板

完整的立创筑基学习板支持，包括：

- USART1 / USART2 / USART3 + RS485
- I2C1 六设备总线 + 软件 I2C2
- SPI1 LCD、SPI2 Flash / IMU / 外部 SPI
- SDIO / TF 卡
- 以太网 LAN8720A、CAN1
- WS2812、蜂鸣器、继电器、按键、EC11
- 直流电机、舵机、TMC2209 步进电机、HX711、单总线

### `skystar_stm32f407vet6` — 只有核心板

最小核心板支持：

- LED：PB2
- USART1 控制台：PA9 / PA10
- USB FS：PA11 / PA12
- SWD：PA13 / PA14，SWO：PB3
- HSE 8 MHz、LSE 32.768 kHz
- P1 / P2 排针说明见板级文档

## 构建

工作区里的 `zephyr-env.sh` 会把本 module 加入 `ZEPHYR_EXTRA_MODULES`。

```bash
cd /home/o431/sources/o431_obj
source ./zephyr-env.sh

west boards -n '^skystar'
```

构建带底板的 board：

```bash
west build -p always -b skystar_stm32f407
```

构建只有核心板的 board：

```bash
west build -p always -b skystar_stm32f407vet6
```

## 烧录

```bash
west flash
```

两个 board 默认都使用 OpenOCD + CMSIS-DAP。

也可以显式指定其他烧录器：

```bash
west flash -r pyocd
west flash -r jlink
west flash -r dfu-util
```

## 许可证

MIT
