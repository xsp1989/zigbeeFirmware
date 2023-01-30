EmberZNet (EZSP) Zigbee 3.0 / Zigbee Coordinator (NCP) firmmware for Silicon Labs EFR32MG21 (EFR32 Mighty Gecko Series 2) USB dongle.

Warning! Flashing custom firmwares may void your warranty. Use at your own Risk!

## Compatible hardware

Initially built, compiled, and tested with the original first-generation barebone ITead Zigbee 3.0 USB Dongle Model 9888010100045:

  ![itead dongle](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/Itead%20Dongle.png)
  
Zigbee 3.0 USB Dongle Model 9888010100045 came pre-flashed from ITead with with unsigned standard Silicon Labs Zigbee NCP firmware.

Also tested with easyiot zigbee 3.0 USB Dongle model ZB-GW04 based on "SM-011 v1.0" Zigbee module:

  - https://easyiot.aliexpress.com/store/5839056
  - https://www.aliexpress.com/item/1005002791666029.html
  - https://www.aliexpress.com/item/1005003736123654.html
  - https://www.aliexpress.com/item/1005003692212448.html
  - https://www.aliexpress.com/item/1005003578599189.html
  - https://www.aliexpress.com/item/1005003814709714.html
  - https://www.aliexpress.com/item/1005004562353633.html
  - https://www.aliexpress.com/item/1005003501898658.html
  - https://www.aliexpress.com/item/1005004410926709.html
  - https://www.aliexpress.com/item/1005002469947910.html

  ![easyiot dongle](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/easyiot%20Dongle.png)

## Recommended firmware

At the time of writting (2022-08-08) EmberZNet Zigbee version 6.10.3.0 firmware is recommended for the ZHA integration in Home Assistant (which depends on the open source zigpy and bellows libraries):

- ncp-uart-sw_v6.10.3_115200.gbl

The same firmware has also been confirmed to work good with OpenHAB Zigbee Binding, Zigbee2MQTT, IoBroker, Zigbee Plugin for Domoticz, and Zigbee Plugin for Jeedom.

## Versions and changelog

#### 6.10.3.0 (EmberZNet Zigbee 6.10.3.0)
Configuration Parameter	| Value
------------------------|------
Part | EFR32MG21A020F768IM32
Version | EZSP 6.10.3.0
CTUNE value	| 128
Address Table Size | 32
Child Table Size | 32
Source Routes | 200
TX | PB01
RX | PB00
CTS	| PD03
RTS	| PD04
LED | PC00

#### 679 (Zigbee EmberZNet 6.7.9)
- Changed configuration to set HFXO CTUNE value to 128, 
- General upstream bug-fixes from Silabs EmberZNet 6.7.9.0 as per https://www.silabs.com/documents/public/release-notes/emberznet-release-notes-6.7.9.0.pdf

#### 678 (Zigbee EmberZNet 6.7.8)
- Default release with EZSP v8 support shipped with ITead Zigbee 3.0 USB Dongle Model 9888010100045 https://www.itead.cc/zigbee-3-0-usb-dongle.html

#### 655 (Zigbee EmberZNet 6.5.5)
- Legacy firmware for backwards compatible with older applications that are only compatible with EZSP v7.

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
* sw = software flow control (XON/XOFF flow control)
* hw = hardware flow control (RTS/CTS flow control)
* 655 / 678 / 679 = EmberZNet Version which also indoicate version for EZSP (EmberZNet Serial Protocol)
* 115200 = Baud rate speed set to 115200
* 57600 = Baud rate speed set to 57600
* std = Standalone
* btl = Bootloader
* PB00-PB01 = Port used for TXD (Transceive Data) and RXD (Receive Data)
* PA00 = Bootloader GPIO Activation

## Firmware upgrade procedure

#### Prerequisites before upgrading

 - To flash ITead Zigbee 3.0 USB Dongle Model 9888010100045 make sure that the operating-system has device drivers for the CH340E (WCH CH340 E) USB to Serial chip that dongle has, (most newer operating-systems already has has correct device drivers built-in for CH340).
 -  Always stop any software applications/services/integrations that are connected to the USB dongle.
 -  Recommend backup NVRAM on the adapter before upgrading firmware. NVRAM on EZSP (EmberZNet Serial Protocol) based adapters can be backuped (and restored) with example zigpy/bellows https://github.com/zigpy/bellows#nvram-backup-and-restore

#### Flashing firmware for ITEAD Zigbee 3.0 USB Dongle

Firmware can be updated via Elelabs EZSP Firmware Update Utility after stop any software that use it.  

https://github.com/Elelabs/elelabs-zigbee-ezsp-utility/

Example command (copy firmware file to elelabs-zigbee-ezsp-utility data directory and substitute '/dev/ttyUSB1' for the actual path to your USB stick):
```
#python3 Elelabs_EzspFwUtility.py flash -f data/ncp-uart-sw_679_115200.gbl -p /dev/ttyUSB0
#python3 Elelabs_EzspFwUtility.py probe -p /dev/ttyUSB0
```
Alternatively could update firmware using Docker image by walthowd. Substitute '/dev/ttyUSB1' for the actual path to your USB stick.

https://github.com/walthowd/husbzb-firmware

Example command (substitute '/dev/ttyUSB1' for the actual path to your USB stick):
```
wget https://github.com/xsp1989/zigbeeFirmware/blob/master/firmware/Zigbee3.0_Dongle/ncp-uart-sw_679_115200.gbl
docker run --rm --device=/dev/ttyUSB1:/dev/ttyUSB1 -it -v `pwd`:/data walthowd/husbzb-firmware bash
./ncp.py flash -p /dev/ttyUSB1 -f /data/ncp-uart-sw_679_115200.gbl
./ncp.py scan
```

## Firmware recovery procedure

1. ETX - Pin PB01 ERX Pin PB00 connect to your pc
2. Press and hold the “BOOT” button, then press the “RST” button, and then release it at the same time
3. Choice "1. upload gbl"
4. Using xmodem(128 byte) send this ota file to you device.

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
Address Table Size | 8
Child Table Size | 32
Source Routes | 128
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

## EFR32, EmberZNet and EZSP Protocol Versions

EZSP stands for "EmberZNet Serial Protocol" which is the default serial interface used in compatible Zigbee coordinator firmware for the Silicon Labs EFR32 hardware family such as the EFR32MG21/MGM210 and EFR32MG12/MGM12 series.

- https://www.silabs.com/wireless/zigbee/efr32mg21-series-2-socs
- https://www.silabs.com/wireless/zigbee/efr32mg21-series-2-modules
- https://www.silabs.com/wireless/zigbee/efr32mg12-series-1-socs
- https://www.silabs.com/wireless/zigbee/efr32mg12-series-1-modules

Silicon Labs do not currently have a consolidated list of changes by EmberZNet SDK or EZSP protocol versions. The EZSP additions, changes and deletions have only ever been listed in the [Zigbee EmberZNet Release Notes](https://www.silabs.com/search#q=Zigbee%20EmberZNet%20Release%20Notes&t=All&sort=relevancy) (EmberZNet SDK) under the "New items" section as well as the matching UG100 EZSP Reference Guide included with each EmberZNet SDK release.

The largest change was between EZSP v4 (first added in EmberZNet 4.7.2 SDK) and EZSP v5 that was added in EmberZNet 5.9.0 SDK which requires the Legacy Frame ID 0xFF. The change from EZSP v5 to EZSP v6 was done in EmberZNet 6.0.0 SDK. The change from EZSP v6 to EZSP v7 was in EmberZNet 6.4.0 SDK. EmberZNet 6.7.0 SDK added EZSP v8 (and Secure EZSP Protocol Version 2).

Perhaps more important to know is that EZSP v5, v6 and v7 (EmberZNet 6.6.x.x) use the same framing format, but EmberZNet 6.7.x.x/EZSP v8 introduced new framing format and expanded command id field from 8 bits to 16 bits.

See Silabs [Zigbee & Thread Knowledge Base Articles List](https://silabs-prod.adobecqms.net/community/wireless/zigbee-and-thread/knowledge-base.entry.html/2020/04/01/zigbee_thread_knowledgebasearticleslist-ih5r) for background information.
