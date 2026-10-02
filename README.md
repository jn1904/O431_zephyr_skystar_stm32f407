# O431_zephyr_skystar_stm32f407

Zephyr module containing two related boards:

| Board name | Description |
|---|---|
| `skystar_stm32f407` | SkyStar STM32F407VET6 core board + LCKFB FDB baseboard |
| `skystar_stm32f407vet6` | SkyStar STM32F407VET6 core board only |

Both boards use the same STM32F407VET6 SoC and are provided by a single
Zephyr module.

## Repository layout

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

## Board summary

### `skystar_stm32f407` — core board + baseboard

Full LCKFB FDB baseboard support, including:

- USART1 / USART2 / USART3 + RS485
- I2C1 six-device bus and software I2C2
- SPI1 LCD, SPI2 Flash / IMU / external SPI
- SDIO / TF card
- Ethernet LAN8720A, CAN1
- WS2812, buzzer, relay, keys, EC11
- DC motors, servos, TMC2209 stepper, HX711, 1-Wire

### `skystar_stm32f407vet6` — core board only

Minimal core board support:

- LED on PB2
- USART1 console on PA9 / PA10
- USB FS on PA11 / PA12
- SWD on PA13 / PA14, SWO on PB3
- HSE 8 MHz and LSE 32.768 kHz
- P1 / P2 headers described in the board documentation

## Build

The workspace `zephyr-env.sh` points `ZEPHYR_EXTRA_MODULES` at this module.

```bash
cd /home/o431/sources/o431_obj
source ./zephyr-env.sh

west boards -n '^skystar'
```

Build the baseboard board:

```bash
west build -p always -b skystar_stm32f407
```

Build the core board:

```bash
west build -p always -b skystar_stm32f407vet6
```

## Flash

```bash
west flash
```

Default runner for both boards is OpenOCD + CMSIS-DAP.

Other runners:

```bash
west flash -r pyocd
west flash -r jlink
west flash -r dfu-util
```

## License

MIT
