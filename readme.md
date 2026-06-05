# Testing Adafruit Mikro SD Card with SPI for Nucleo STM32WB55RG Board

https://github.com/STMicroelectronics/STM32CubeF0/blob/master/Drivers/BSP/Adafruit_Shield/stm32_adafruit_sd.c

tutorial video: https://www.youtube.com/watch?v=PBIm8BCnbyQ
using this for fatfs: https://github.com/kiwih/cubeide-sd-card/tree/master

# setup build 
configure cmake to create build directory:
`cmake --preset Debug`

then build:
`cmake --build --preset Debug`

## Build and flash
using st flash or openocd:

```bash
st-flash --reset write build/Debug/test-sd-card.bin 0x08000000
```

```bash
openocd -f interface/stlink.cfg -f target/stm32wbx.cfg -c "program build/Debug/test-sd-card.elf verify reset exit"
```

## MX Setup
Enable RCC in System Core (Pinout & Configuration)
Set HSE in (Clock Config), sysclock 64 MHz
Enable SPI, 8 bits and PRESCALE (for baud rate) to highest, 256
Move CLK to PA5 with control click

Pins:
Chipselect: PA4 as GPIO_Output, Output level `HIGH` (name it SP1_CS), GPIO PULLUp/PUlldown: `Pull up`

System Core > SYS > Debug: Serial Wire
## Wiring

Adafruit SD card -----> Nucleo wb55
__________________________
CLK -----> PA5 (D13)
MOSI -----> PA7 (D11)
MISO -----> PA6 (D12)
CS -------> PA4 (D10)
VCC -------> 3V3
GND --------> GND

the rest is unwired
