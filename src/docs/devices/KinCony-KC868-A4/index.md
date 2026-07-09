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

uart:
  - id: rs232
    baud_rate: 115200
    rx_pin: GPIO16
    tx_pin: GPIO17

switch:
  - platform: gpio
    name: "Relay 1"
    id: relay_1
    pin: GPIO2

  - platform: gpio
    name: "Relay 2"
    id: relay_2
    pin: GPIO15

  - platform: gpio
    name: "Relay 3"
    id: relay_3
    pin: GPIO5

  - platform: gpio
    name: "Relay 4"
    id: relay_4
    pin: GPIO4

binary_sensor:
  - platform: gpio
    name: "Digital input 1"
    id: digital_input_1
    pin:
      number: GPIO36
      inverted: true

  - platform: gpio
    name: "Digital input 2"
    id: digital_input_2
    pin:
      number: GPIO39
      inverted: true

  - platform: gpio
    name: "Digital input 3"
    id: digital_input_3
    pin:
      number: GPIO27
      inverted: true

  - platform: gpio
    name: "Digital input 4"
    id: digital_input_4
    pin:
      number: GPIO14
      inverted: true

sensor:
  - platform: dht
    id: sensor_dht
    pin: GPIO13
    temperature:
      name: Temperature
      id: dht_temperature
      icon: "mdi:thermometer"
    humidity:
      name: Humidity
      id: dht_humidity
      icon: "mdi:water-percent"

  - platform: adc
    name: "Analog input 1"
    id: analog_input_1
    pin: GPIO32
    
  - platform: adc
    name: "Analog input 2"
    id: analog_input_2
    pin: GPIO33
    
  - platform: adc
    name: "Analog input 3"
    id: analog_input_3
    pin: GPIO34

  - platform: adc
    name: "Analog input 4"
    id: analog_input_4
    pin: GPIO35

output:
  - platform: esp32_dac
    id: analog_output_1
    pin: GPIO25
    
  - platform: esp32_dac
    id: analog_output_2
    pin: GPIO26
    
  - platform: ledc
    id: beep_1
    pin: GPIO18

rtttl:
  output: beep_1
  id: buzzer

script:
  - id: play_siren
    then:
      - rtttl.play: Siren:d=8,o=5,b=100:d,e,d,e,d,e,d,e

button:
  - platform: template
    name: "Test Buzzer"
    icon: "mdi:volume-high"
    entity_category: diagnostic
    on_press:
      - script.execute: play_siren
```
