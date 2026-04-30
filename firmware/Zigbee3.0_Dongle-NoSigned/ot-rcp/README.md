# OpenThread (OT-RCP) Thread / Thread Border Router (RCP) Firmware  
for Silicon Labs EFR32MG21 (EFR32 Mighty Gecko Series 2) USB dongle

⚠️ **Warning!** Flashing custom firmware may void your warranty. Use at your own risk!

---

## Compatible hardware

Tested with EasyIoT Thread / multiprotocol USB dongles based on EFR32MG21A020F768IM32 (including Zigbee/Thread capable modules such as “ZYZBP008”):

- https://easyiot.aliexpress.com/store/all-wholesale-products/1101491524.html
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

---

## Recommended firmware

At the time of writing, **OpenThread RCP (Radio Co-Processor)** firmware based on Silicon Labs OpenThread SDK is recommended for Thread Border Router setups such as:

- Home Assistant (OpenThread Border Router / OTBR add-on)
- `ot-br-posix`
- Matter / Thread integrations

Typical firmware file example:

- `ot-rcp-uart-<version>.gbl`

Recommended configuration:
- Interface: UART
- Baud rate: 115200 (or higher like 460800 depending on host)
- Flow control: Optional (RTS/CTS recommended for stability)

---

## Versions and changelog

#### OT-RCP (OpenThread RCP - latest)
Configuration Parameter | Value
----------------------|------
Part | EFR32MG21A020F768IM32
Stack | OpenThread (RCP mode)
Interface | UART
Baudrate | 460800
TX | PB01 
RX | PB00
CTS | Optional (PD03)
RTS | Optional (PD04)
Protocol | Spinel (OpenThread RCP protocol)

#### Notes
- Uses **Spinel protocol** instead of EZSP
- Requires external host (Linux / Raspberry Pi / HA) to run Thread stack
- Supports Thread 1.1 / 1.2 / 1.3 (depending on SDK version)

---

## Abbreviations legend

Commonly used shorthand in OT-RCP firmware:

* rcp = Radio Co-Processor (no full stack on device)
* ot = OpenThread
* spinel = OpenThread serial protocol
* s2 = EFR32 Series 2 (EFR32MG21)
* uart = UART interface
* usb = USB CDC (virtual serial)
* ncp = (not used here, Zigbee-only concept)
* 115200 / 460800 = UART baudrate
* gbl = Gecko Bootloader firmware image
* otbr = OpenThread Border Router

---

## Firmware upgrade procedure

### Prerequisites

- Install USB-UART driver (e.g., CH340 if applicable)
- Stop all services using the dongle:
  - Home Assistant
  - otbr-agent
- (Optional) Backup any existing firmware if needed

---
