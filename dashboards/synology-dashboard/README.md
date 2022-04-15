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

This goes to the sensors section in the configuration.yaml, and you need to change the sensor names to correspond your actual sensors. Currently the volumes values are presented as strings which include the unit, the unit needs to be removed and value converted make the calculation.

```
  - platform: template
    sensors:
      synology_free_space_volume_1:
        value_template: >-
          {{ (states('sensor.synology_total_size_volume_1')|replace('Tb','')|float - states('sensor.synology_used_space_volume_1')|replace('Tb','')|float)|round(2) }}
        unit_of_measurement: 'TB'
        friendly_name: Synology Free Space Volume 1
  
```

## BUTTONS

Now days the Synology DSM integration offers reboot and shutdown buttons, before that I create few shell_commands to do the shutdown and reboot and I am still using those. I also have WOL (Wake-On-LAN) setup to turn the NAS back on, I am not going through the shell-command and certification setup here (unless there is enough interest how to do that), so you should replace the shell_commands with the new integration buttons, I think this is anyway a lot easier and better way for now.

```
  ## WAKE-ON-LAN ##
  - platform: wake_on_lan
    mac: {your-nas-mac-1}
    name: "TD_DS1"
    host: {your-nas-lan-ip-1}
    turn_off:
      service: shell_command.td_ds1_shutdown
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
