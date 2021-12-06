Silicon Labs Zigbee 3.0 / 3.x firmware.

## Compatible hardware

Built, compiled, and tested with ITead Zigbee 3.0 USB Dongle and easyiot zigbee 3.0 USB Dongle. 

- https://www.itead.cc/zigbee-3-0-usb-dongle.html   

  ![itead dongle](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/Itead%20Dongle.png)
- https://www.aliexpress.com/item/1005002791666029.html

  ![easyiot dongle](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/easyiot%20Dongle.png)

Zigbee 3.0 USB Dongle Model 9888010100045 comes pre-flashed from ITead with with unsigned standard Silicon Labs Zigbee NCP firmware.

Nopte! Flashing custom firmwares may void your warranty. Use at your own Risk!

## Recommended firmware

Currenly recommended firmware for the zigpy/bellows based ZHA integration in Home Assistant:

- ncp-uart-sw_679_115200.gbl

## Versions and changelog

#### 6.7.10 (Zigbee EmberZNet 6.7.10)
Configuration Parameter	| Value
------------------------|------
Part | EFR32MG21A020F768IM32
Version | EZSP 6.7.10
CTUNE value	| 128
Child Table Size | 32
TX | PB01
RX | PB00
CTS	| -
RTS	| -
LED | PC00 
KEY | PA00
Baud rate | 115200


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
* pb0-pb1 = Port used for TXD (Transceive Data) and RXD (Receive Data)
* pa0 = Bootloader GPIO Activation

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
2. Press and hold the Boot button, then press the Rst button, and then release it at the same time
3. Choice "1. upload gbl"
4. Using xmodem(128 byte) send this ota file to you device.

## Join the network
1. Press BOOT for 5 seconds until the LED flashes.
2. Gateway allows access to the network.
3. If the LED is always on, then join the network successfully.

## LED status
LED status | Network Status
-----------|---------------
LED off | NO Netwrok
LED blink | steering network
LED on | Joined to the network 

## Extra features
* If you send data through the serial port, the router will forward the data to the gateway.
* If data is sent to the router through the coordinator, the serial port will receive the data.

## Cluster Identifiers
Identifier | Name 
-----------|---
0x0704 | Tunneling (Smart Energy)
