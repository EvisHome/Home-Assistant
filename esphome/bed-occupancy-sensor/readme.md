# Bed Occupancy Sensor

![WhatsApp Image 2024-11-30 at 18 44 25_0a5e4d57](https://github.com/user-attachments/assets/379c5367-62cf-4637-9317-24a8a7bda799)

## Description
Double bed occupancy monitoring, using two pressure sensitive stripes under the bed mattresses. Including a BLE Proxy

I started testing with multiple different resistors, but my I have first a a really thick and heavy memory foam mattress and on top of that I have an 8 cm memory foam mattress topper. Tried 5,6KOhm, 47KOhm, 100KOhm, 3x 100KOhm, until I ended to 1MOhm resistor which worked perfectly for my mattress setup.

I also enabled the BLE Proxy on the ESP32.

## Background
I have mmWave sensors in each rooms, from which some can detect also different areas within the room, but detecting bed occupancy has been tricky, after a while I fall a sleep, I'm not getting detected to be in bed. Not sure if I teleport to somewhere else, just sleep very very very still, or if my 11kg weighted blanked (filled with tiny glass balls) has something to do with that.

I tried a pressure mattress under my mattress topper, but that was so annoying I ended up taking it away. It didn't stay in place, but the most annoying thing was the noise it made, when you turn from side to side.

## Parts

* ESP Wroom 32 (ESP32 DevKit v1)
* Resistors 2 x 1 MOhm
* SF15-600 10 kg - Flexible Thin Film Pressure Sensor
* Wires and connectors

![image](https://github.com/user-attachments/assets/f2c43f53-7ee8-4ed9-a1c7-096777f4c1ab)

## ESPHome Code

```yaml
substitutions:
  name: master
  sensor1: right
  sensor2: left

esphome:
  name: ${name}-bed-sensor
  friendly_name: ${name}-bed-sensor

esp32:
  board: esp32dev
  framework:
    type: arduino

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: !secret api_key

# Over The Air Updates
ota:
  platform: esphome
  password: !secret ota_password

# Connect to Wi-Fi
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  fast_connect: true

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "bed-sensor-${name}"
    password: !secret ap_password

captive_portal:

# BLUETOOTH PROXY
bluetooth_proxy:
  active: true

esp32_ble_tracker:


binary_sensor:
  # Binary sensor for status of device
  - platform: status
    name: ${name} Bed occupancy Status
  # Binary sensor for left side
  - platform: analog_threshold
    name: ${name} Bed occupancy - ${sensor1}
    sensor_id: ${name}_bed_occupancy_${sensor1}_value
    icon: mdi:bed
    threshold: 1 #the voltage treshold when considered occupied
    filters:
      - invert:
  - platform: analog_threshold
    name: ${name} Bed occupancy - ${sensor2}
    sensor_id: ${name}_bed_occupancy_${sensor2}_value
    icon: mdi:bed
    threshold: 1 #the voltage treshold when considered occupied
    filters:
      - invert:


sensor:
  # ADC sensor for left TFP sensor
  - platform: adc
    pin: 32
    attenuation: 0db
    name: ${name} bed occupancy - ${sensor1} value
    id: ${name}_bed_occupancy_${sensor1}_value
    unit_of_measurement: "V"
    update_interval: 5s
    internal: false # Default not exposed to front-end
    raw: true
    filters:
      - multiply: 0.00026862 # 1.1/4095, for attenuation 0db
  # ADC sensor for left TFP sensor
  - platform: adc
    pin: 33
    attenuation: 0db
    name: ${name} bed occupancy - ${sensor2} value
    id: ${name}_bed_occupancy_${sensor2}_value
    unit_of_measurement: "V"
    update_interval: 5s
    internal: false # Default not exposed to front-end
    raw: true
    filters:
      - multiply: 0.00026862 # 1.1/4095, for attenuation 0db
```

## Bed Install

I taped the the SF15-600 sensors to the beams on about chest/shoulder level under the mattresses.

	
## Home Assistant

![image](https://github.com/user-attachments/assets/431e864b-5b74-43d1-a4c6-37b8dcec8373)




	


