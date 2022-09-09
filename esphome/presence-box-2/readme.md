# Presence Box 2 (Work In Progress)

![](presence-box.png)

Upgrades to the previous version [here](/esphome/presence)

## TOC
* [Diagram](#diagram)
* [Parts](#parts)
* 3D Printable Enclosures
* ESPHome code

## Parts

Notice that not all parts will fit simultaneously in to a one box.

* ESP32 DevKit v1 (fits in to the box stands)
* [AM312 PIR or HC-SR501 PIR](https://www.amazon.de/-/en/gp/product/B08LBDYPYD/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
* [DFROBOT SEN0395 mmWave Radar](https://www.mouser.fi/ProductDetail/426-SEN0395)
* TLS2561 Light Sensor
* AHT21 Temperature & Humidity Sensor
* CCS811 Air Quality Sensor (VOC & eCO2)
* 5mm RGB LED (common catode or anode) / RGB SMD LED
* [OLED Display Module I2C SSD1306](https://www.amazon.de/-/en/gp/product/B07BDFXFRK/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1)

Optionally if powering from DC power supply, instead of USB

* DC plug (can be used for power instead of USB)
* Buck Converter (for voltage adjusting)

## Diagram

Note! I don't have all the sensors in this currently in a same box, but the wiring is the same although different sensors in different places.

![](presence-box-diagram.png)



## Under the hood


![](under-the-hood.jpg)
