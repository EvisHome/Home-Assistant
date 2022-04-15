## SYNOLOGY DASHBOARD



![Synology Overview](/dashboards/synology-dashboard/img/synology-dashboard.png)

&nbsp;

&nbsp;

## INTEGRATIONS

List of integrations needed to set this up:

* [Synology DSM](https://www.home-assistant.io/integrations/synology_dsm)

The LAN switches, in the button row, are through Unifi Network Integration

* [Unifi Network](https://www.home-assistant.io/integrations/unifi/)

&nbsp;

&nbsp;

## SENSORS

I used a template sensor to calculate the Free Space for the Apex Chart donut

This goes to the sensors section in the configuration.yaml, and you need to change the sensor names to correspond your actual sensors. Currently the volumen values are presented as strings which include the unit, the unit needs to be removed and value converted make the calculation.

```
  - platform: template
    sensors:
      synology_free_space_volume_1:
        value_template: >-
          {{ (states('sensor.synology_total_size_volume_1')|replace('Tb','')|float - states('sensor.synology_used_space_volume_1')|replace('Tb','')|float)|round(2) }}
        unit_of_measurement: 'TB'
        friendly_name: Synology Free Space Volume 1
  
```


&nbsp;

&nbsp;

## VIEW & CARDS

Standard Masonry view was used for this

### FRONTEND ELEMENTS & CUSTOM CARDS

List of cards used:

* vertical-stack
* horizontal-stack
* picture-elements
* custom:button-card
* custom:apexcharts-card
