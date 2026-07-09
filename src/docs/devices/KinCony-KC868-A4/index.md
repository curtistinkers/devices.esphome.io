---
title: KinCony KC868-A4
date-published: 2023-04-19
type: relay
standard: global
board: esp32
---

![Product](KC868-A4_01.jpg "Product Image")

## GPIO Pinout

| Pin    | Function            |
| ------ | ------------------- |
| GPIO2  | Relay 1             |
| GPIO15 | Relay 2             |
| GPIO5  | Relay 3             |
| GPIO4  | Relay 4             |
| GPIO36 | Digital input 1     |
| GPIO39 | Digital input 2     |
| GPIO27 | Digital input 3     |
| GPIO14 | Digital input 4     |
| GPIO32 | Analog input 1      |
| GPIO33 | Analog input 2      |
| GPIO34 | Analog input 3      |
| GPIO35 | Analog input 4      |
| GPIO25 | Analog output 1     |
| GPIO26 | Analog output 2     |
| GPIO13 | 1-Wire GPIO         |
| GPIO18 | Piezo buzzer        |
| GPIO16 | RS232 RXD           |
| GPIO17 | RS232 TXD           |
| GPIO21 | 433 MHz transmitter |
| GPIO19 | 433 MHz receiver    |
| GPIO23 | IR receiver         |
| GPIO22 | IR transmitter      |
| GPIO0  | PCB button S1       |

[Additional pinout/design details](https://www.kincony.com/arduino-esp32-4-channel-relay-module.html)

## Basic Configuration

```yaml
# Basic Config
esphome:
  name: kc868-a4

esp32:
  variant: esp32

# Enable logging
logger:

# Enable Home Assistant API
api:

ota:
  password: "4d5a388de4f759bf88e71cde7a31af6f"

wifi:
  ssid: "KinCony"
  password: "a12345678"

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Kc868-A4 Fallback Hotspot"
    password: "QOU4hbAjJ5Wb"

captive_portal:

switch:
  - platform: gpio
    name: "light1"
    pin: 2
    inverted: false

  - platform: gpio
    name: "light2"
    pin: 15
    inverted: false

  - platform: gpio
    name: "light3"
    pin: 5
    inverted: false

  - platform: gpio
    name: "light4"
    pin: 4
    inverted: false

binary_sensor:
  - platform: gpio
    name: "input1"
    pin:
      number: 36
      inverted: true

  - platform: gpio
    name: "input2"
    pin:
      number: 39
      inverted: true

  - platform: gpio
    name: "input3"
    pin:
      number: 27
      inverted: true

  - platform: gpio
    name: "input4"
    pin:
      number: 14
      inverted: true
```
