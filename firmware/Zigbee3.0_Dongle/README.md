Silicon Labs Zigbee 3.0 / 3.x firmware.

## Compatible hardware

Built, compiled, and tested with ITead Zigbee 3.0 USB Dongle Model 9888010100045 https://www.itead.cc/zigbee-3-0-usb-dongle.html

Zigbee 3.0 USB Dongle Model 9888010100045 comes pre-flashed from ITead with with unsigned standard Silicon Labs Zigbee NCP firmware.

Nopte! Flashing custom firmwares may void your warranty. Use at your own Risk!

## Recommended firmware

Currenly recommended firmware for the zigpy/bellows based ZHA integration in Home Assistant:

- ncp-uart-nsw_679_115200.gbl

## Versions and changelog

#### 679 (Zigbee EmberZNet 6.7.9)
- Changed configuration to set HFXO CTUNE value to 128, 
- General upstream bug-fixes from Silabs EmberZNet 6.7.9.0 as per https://www.silabs.com/documents/public/release-notes/emberznet-release-notes-6.7.9.0.pdf

#### 678 (Zigbee EmberZNet 6.7.8)
- Default release with EZSP v8 support shipped with ITead Zigbee 3.0 USB Dongle Model 9888010100045 https://www.itead.cc/zigbee-3-0-usb-dongle.html

#### 655 (Zigbee EmberZNet 6.5.5)
- Legacy firmware for backwards compatible with older applications that are only compatible with EZSP v4, EZSP v5 or/and EZSP v6.

## Abbreviations legend:

Commonly used shorthand and acronyms used in firmware image file names for Silabs based adapters:

* ncp = Silabs NCP
* s2 = EFR32 Series 2 (eg. EFR32MG2x such as EFR32MG21)
* s1 = EFR32 Series 1 (eg. EFR32MG1x)
* F1024 = 1024k Flash Size
* F512 = 512k Flash Size
* F256 = 256k Flash Size
* com = Combined (necessary for EFR32 Series 1)
* uart = UART interface
* nsw = no flow control
* sw = software flow control
* 655 / 678 / 679 = EmberZNet Version which also indoicate version for EZSP (EmberZNet Serial Protocol)
* 115200 = Baud rate speed set to 115200
* 57600 = Baud rate speed set to 57600
* std = Standalone
* btl = Bootloader
* pb0-pb1 = Port used for TXD (Transceive Data) and RXD (Receive Data)
* pa0 = Bootloader GPIO Activation

## Firmware recovery procedue

1. ETX - Pin PB01 ERX Pin PB00 connect to your pc
2. Ground PA00
3. Temporary ground the reset pin Z_RST (nRST) to reset
4. Choice "1. upload gbl"
5. Using xmodem(128 byte) send this ota file to you device.

## Configurations used when compiling your own firmware with Silabs Simplicity Studio and EmberZNet Zigbee Stack

#### EmberZNet NCP Zigbee application firmware

EFR32MG21 target
NCP UART TX --> PA0
NCP UART RC <-- PA1
EZSP Version 8
EmberZNet 6.7.9
DCDC

Configuration Parameter | Value
----------------------- | ------
Address Table Size | 16
Child Table Size | 32
Source Routes | 200
CTUNE value | 128

The remaining parameters are at the default values.

#### Gecko Bootloader firmware

EFR32MG21 target
Standalone Bootloader
NCP UART TX --> PA0
NCP UART RC <-- PA1
PB00/UART_BUTTON_RESET is bootloader activiation pin/button
Version: x.xx.x
DCDC

Use "1. upload gbl" and "xmodem(128 byte)" to send bootloader ota file to device.
