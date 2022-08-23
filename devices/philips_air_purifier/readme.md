![image](air-purifier.gif)

For Philips Air Purifier 1214/10 whitch uses the HTTP protocol for communication, I used https://github.com/GeorgeSG/philips_airpurifier_http integration, which is a fork of xMrVizzy/philips-airpurifier..

The Dashboard controls use Grid, Mushroom Cards and Card Mod.

You can switch the mode from the four buttons, or change the speed from the slider, which then automatically puts the purifier into manual mode. Few visual tricks for the fan spinning faster or slower, depending the actual speed percentage. The filter turn to yellow, when there is a week left, and to red when 48 hours left.

Everything is wrapped in a one column Grid
```yaml
type: grid
square: false
columns: 1
cards:
```

1. First Row is a mushroom-fan-card
- change the entity *fan.philips_air_purifier* to your fan entity
```yaml
  - type: custom:mushroom-fan-card
    entity: fan.philips_air_purifier
    show_percentage_control: true
    layout: horizontal
    tap_action:
      action: toggle
    hold_action:
      action: more-info
    double_tap_action:
      action: none
    card_mod:
      style: |
        ha-card {
          border-bottom-right-radius: 0px;
          border-bottom-left-radius: 0px;
        }
```

2. Second Row - is Grid of 4 Columns
```yaml
  - square: false
    columns: 4
    type: grid
    cards:
```
- Using *custom:mushroom-template-card*
  - change replace the *fan.philips_air_purifier* with your fan entity, and make the same change in the in the card_mod style part where used.
  - In each card the *mode == auto* matches the modes the device supports (modify in 2 places to your needs), change for each card. Also change the *primary: Auto* text.
 
```yaml
      - type: custom:mushroom-template-card
        entity: *fan.philips_air_purifier*
        primary: Auto
        secondary: ''
        icon: mdi:fan
        layout: vertical
        icon_color: |
          {% set status = states(entity) %}
          {% if status == 'on' %}
          {% set mode = state_attr(entity,'preset_mode') %}
          {% if mode == 'auto' %}
            blue
          {% else %}
            disabled
          {% endif %}
          {% else %}
            disabled
          {% endif %}
        tap_action:
          action: call-service
          service: fan.set_preset_mode
          data:
            preset_mode: auto
          target:
            entity_id: fan.philips_air_purifier
        card_mod: null
        style:
          mushroom-shape-icon:
            $: |
              .shape ha-icon
                {
                  {% set status = states('fan.philips_air_purifier') %}
                  {% if status == 'on' %}
                  {% set mode = state_attr('fan.philips_air_purifier','preset_mode') %}
                  {% if mode == 'auto' %}
                  {% set speed = state_attr('fan.philips_air_purifier','percentage') | int %}
                  {% if speed < 60 %}
                  --icon-animation: rotation 2s linear infinite;
                  {% elif speed < 80 %}
                  --icon-animation: rotation 1s linear infinite;
                  {% elif speed < 100 %}
                  --icon-animation: rotation 0.6s linear infinite;
                  {% else %}
                  --icon-animation: rotation 0.3s linear infinite;
                  {% endif %}
                  {% endif %}
                  {% endif %}
                }
                @keyframes rotation {
                  0% {
                    transform: rotate(0deg);
                  }
                  100% {
                    transform: rotate(360deg);
                  }
                }
            .: |
              ha-card {
                border-radius: 0px;
                box-shadow: 0px 0px;
                background-color: rgba(0,0,0,0);
                border: 5px solid #222;
              }
              :host {
              }
```
