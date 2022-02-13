# home-assistant
My Home Assistant Theme

```
# Get the theme from the folder
/themes/evis-theme.yaml
```

I am using an automation on Home Assistant start to set the theme to my custom theme, so I everyone has the same theme though backend-selected.

```
- id: '1602845089462'
  alias: Set Default Theme
  description: Set Default Theme on start
  trigger:
  - platform: homeassistant
    event: start
  condition: []
  action:
  - service: frontend.set_theme
    data:
      name: Evis Theme
  mode: single
```


Some examples of my dashboards below

## NETWORK (Dashboard)

Standard HA Integrations:
* Unifi Network

Custom Integrations Used:
* [sensor.unifigatewar](https://github.com/custom-components/sensor.unifigateway)

Custom HACS frontend cards & elements used:
* [mini-graph-card](https://github.com/kalkih/mini-graph-card)
* [card-mod](https://github.com/thomasloven/lovelace-card-mod)

![HA Overview](/examples/Network-dashboard.png)


## Home Assistant Overview

![HA Overview](/examples/HA-overview-dashboard.png)



