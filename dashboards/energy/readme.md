# Energy Dashboard (WIP)

![energy dashboard](energy-dashboard.png)

## Overview

I currently have fixed price contract, which adjusts prices every 3 months. Not sure if it's the best one so I want to compare to the spot prices and if I at somepoint change over to spot pricing then I have the setup ready it. I also wanted to see some actual data how much different devices and rooms consume energy, so some Shelly Plus 1PMs and 2.5 have been installed around the house, but not on all outlets. To keep an eye out for total consumption I have an Shelly 3EM, which is still in the mail (I'll try to update this once I have that installed as well)

As a background this all started from a dinner conversation with the kids about the energy costs and what we could do to save energy, and how to actually track how much we could save .. so we started this family challenge, how much energy we could save.

Some items we listed that we thought might make the biggest savings:
* reduce the amount of laundry -> no need to run the washing machine so often
* reduce the amount of dished -> no need to run the dishwasher so often
* turn off devices when not in use (fully off, not just standby mode)
* precense guided lights ([Room Presence](https://github.com/EvisHome/Home-Assistant/blob/main/esphome/presence) & [Presence Box 2](Presence Box 2)
* I have also started to automate turning on/off some rack devices during night or when we are away

## Custom Integrations & Cards

* [Nordpool custom component for Home Assistant](https://github.com/custom-components/nordpool)
* [PowerCalc (virtual power & utility sensors)](https://github.com/bramstroker/homeassistant-powercalc)
* [Apexcharts-card](https://github.com/RomRider/apexcharts-card)

### Nordpool Integration & Sensor Setup

Easiest way to install, is to follow the HACS installation option. After installation, I setup the sensor using the WebUI.
1. Go the Home Assistant Settings
2. Go to Devices & Settings and to the Integrations Tab
3. Click add integration and search for Nordpool and setup the sensor (NOTE: I used prices in Cents, so some of the graph calculations maybe setup according to cents, if you have something else you may need to adjust the calculations)

![](nordpool-sensor.png)

### PowerCalc integration

PowerCalc is a great way to create virtual power (W) and energy (kWh) sensors for lights and power plugs, and also utility sensors (measuring hourly, daily, monthly, yearly consumption). By default it creates quite many new sensors. (there is a great video of it [here](https://www.youtube.com/watch?v=tR1x-cxwK-8) by BeardedTinker. Intially I went with the default settings, but later on I ended up removing individual light utility sensors and made some groupings instead.

Here is my [PowerCalc sensor configuration YAML](powercalc-configuration.yaml). It's still a LOT of additional entities, I may still adjust later on, but for now I just wanted to see all the data I can to see what is possible and what to use.

Not all my lights are Smart lights, but the ones that are not are controlled by smart switches, so I know when they are on or off, and for this PowerCalc lets you still create virtual sensors, all you need to know is how much power (W) the bulbs/lights use. These normal light sensors I created through the integration WebUI.


## Helpers

I created few helper entities to help calculate the costs.

* input_number.energy_base_fee (monthly base fee in euros)
* input_number.energy_fixed_fee (this is the fixed c/kWh fee that adjusts every 3 months)
* input_number.energy_tax (energy tax in c/kWh)
* input_number.energy_transfer_base_fee (monthly energy transfer base fee)
* input_number.energy_transfer_fee (transfer fee in c/kWh)
* input_number.energy_spot_price_base_fee (spot price base fee in c/kWh, this added to the spot price)

## Additional Sensors

Created few sensors which calculate the costs shown in the charts

* sensor.total_energy_price = energy_fixed_fee + energy_tax + energy_transfer_fee
* sensor.total_energy_cost_daily = total_energy_price * total daily energy consumption
* sensor.total_energy_cost_monthly = total_energy_price * total monthly energy consumption
* sensor.total_energy_spot_price = energy spot price + energy_spot_price_base_fee + energy_tax + energy_transfer_fee

## The Dashboard / View

I used nested Grids to place the apexcharts-cards in their places.

## Charts

### Energy Consumption Hourly (kWh) & Spot Price (c/kWh)
This chart shows the hourly consumption (currently from all the outlets, but once I have the shelly 3EM I'll change it the data to that.) Also shows the Nordpool spot price history and pulls todays and tomorrows prices from the integration when available.

* [energy-consumption-hourly.yaml](energy-consumption-hourly.yaml)

![](energy-consumption-hourly.png)

### Spot Price (c/kWh)

Shows the Nordpool integration spot price for today and tomorrow. The tomorrow values can be empty at times, depending when the prices are available, for it seems they update around 14:00.

* [spot-price-chart.yaml](spot-price-chart.yaml)

![](spot-price.png)

### Monitored Appliances Daily (kWh)

### Energy Brush Chart

This is combining the Energy Consumption Hourly, Energy Daily and Spot Price charts in to one brush chart, allowing to narrow down or extend the chart time span. I am still not sure if I'll include it in to my dashboard, due to some slowness at times.

* [energy-brush-chart.yaml](energy-brush-chart.yaml)

![](energy-brush-chart.gif)
