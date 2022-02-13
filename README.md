# home-assistant
My Home Assistant Configurations

I am using an automation on Home Assistant start to set the theme to my custom theme

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
