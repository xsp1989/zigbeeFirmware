# Firmware description

## ZigbeeBridge_SM-011-Signed
The following two bridges are used

- ![itead bridge](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/Sonoff_ZigbeeBridge.png)

- ![easyiot dongle](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/ZY_ZigbeeGW.jpg)


## Zigbee3.0_Dongle-NoSigned
The following dongle can be used

- https://www.itead.cc/zigbee-3-0-usb-dongle.html   

  ![itead dongle](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/Itead%20Dongle.png)
- https://www.aliexpress.com/item/1005002791666029.html

  ![easyiot dongle](https://github.com/xsp1989/zigbeeFirmware/blob/master/Pic/easyiot%20Dongle.png)


## Special Note

- Normally, ZB-Bridge and ZB-GW03 use signed firmware, and dongle use unsigned firmware. 
- But a more general judgment method is the version of the bootloader. If the bootloader version is displayed as 1.9.1.xx (xx==02/03/04), the signed firmware is used, and if the bootloader version is displayed as 1.9.2, the unsigned firmware is used.

