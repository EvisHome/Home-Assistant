New Area Card

Required
- entity naming for **area lights**
  - light.[area_name]_lights

- **helpers**
  - select.[area_name]_presence | presence | idle | absence

Change
- HOLD CLICK, toggles area lights
- area presence is shown as a border-color (green), and recent occupancy with time-out as (orange)
- can be used with **streamline_templates** as well, as declutter_card is not maintained anymore.


```YAML
//streamline_templates:
decluttering_templates:
  area_card:
    card:
      type: picture-elements
      elements:
        - type: custom:button-card
          entity: light.[[entity_name]]_lights
          show_name: false
          show_icon: false
          tap_action:
            action: navigate
            navigation_path: /lovelace/[[entity_name]]
          hold_action:
            action: toggle
          double_tap_action:
            action: toggle
          style:
            top: 50%
            left: 50%
            width: 100%
            height: 100%
            z-index: 3
          styles:
            card:
              - border-radius: 8px
              - height: 100%
              - background-color: rgba(0,0,0,0)
              - box-shadow: 0px 0px
          card_mod:
            style: |
              ha-card {
                {% if is_state('input_select.[[entity_name]]_presence','presence') %}
                  border: 3px solid rgba(36, 255, 0, 0.8);
                {% elif is_state('input_select.[[entity_name]]_presence','idle') %}
                  border: 3px solid rgba(255, 163, 0, 0.8);
                {% else %}
                  border: 0px solid rgba(0, 0, 0, 0);
                {% endif %}
              }
        - type: custom:button-card
          name: '[[display_name]]'
          style:
            top: 50%
            left: 50%
            width: 100%
            height: 100%
            z-index: 2
            container-type: inline-size
          styles:
            card:
              - border-radius: 0px
              - border: 0px
              - height: 30%
              - background-color: rgb(0,0,0,0)
              - box-shadow: 0px 0px 2px rgb(255,255,255,0)
              - font-size: 5cqw
            name:
              - font-family: arial
              - font-weight: bold
              - text-transform: uppercase
              - justify-self: left
              - padding-left: 15px
              - color: rgb(255, 255, 255, 1)
              - text-shadow: 0px 0px 5px rgb(0,0,0,1)
        - type: custom:button-card
          entity: '[[temperature_sensor]]'
          icon: mdi:account-circle
          show_name: false
          show_icon: true
          show_state: true
          tap_action:
            action: none
          hold_action:
            action: none
          style:
            top: 50%
            left: 50%
            width: 100%
            height: 100%
            z-index: 2
            container-type: inline-size
          styles:
            name:
              - display: none
            card:
              - border-radius: 0px
              - height: 100%
              - background-color: rgb(0,0,0,0)
              - box-shadow: 0px 0px
            icon:
              - display: none
              - height: 19%
            state:
              - position: absolute
              - top: 7%
              - right: 3%
              - font-size: 5cqw
              - font-weight: bold
              - text-shadow: 0px 0px 5px rgb(0,0,0,1)
        - type: custom:mushroom-chips-card
          chips:
            - type: template
              entity: '[[device_1]]'
              icon: '[[device_1_icon]]'
              icon_color: |
                {% if is_state(entity,'[[device_1_state]]') %}
                  [[device_1_color]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_1_state]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_1_animation]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_2]]'
              icon: '[[device_2_icon]]'
              icon_color: |
                {% if is_state(entity,'[[device_2_state]]') %}
                  [[device_2_color]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_2_state]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_2_animation]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_3]]'
              icon: '[[device_3_icon]]'
              icon_color: |
                {% if is_state(entity,'[[device_3_state]]') %}
                  [[device_3_color]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_3_state]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_3_animation]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_4]]'
              icon: '[[device_4_icon]]'
              icon_color: |
                {% if is_state(entity,'[[device_4_state]]') %}
                  [[device_4_color]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_4_state]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_4_animation]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_5]]'
              icon: '[[device_5_icon]]'
              icon_color: |
                {% if is_state(entity,'[[device_5_state]]') %}
                  [[device_5_color]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_5_state]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_5_animation]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_6]]'
              icon: '[[device_6_icon]]'
              icon_color: |
                {% if is_state(entity,'[[device_6_state]]') %}
                  [[device_6_color]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_6_state]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_6_animation]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
          alignment: center
          style:
            top: 120%
            left: 50%
            width: 100%
            height: 100%
            z-index: 2
            container-type: inline-size
          card_mod:
            style: |
              ha-card {
                --chip-height: 12cqw;
                --chip-icon-size: 8cqw;
                --chip-border-radius: 5px;
                --chip-spacing: 2px;
                --chip-background: rgba(0,0,0,0);
                --chip-box-shadow: 0px 0px;
                --chip-border-width: 0;
              }
        - type: custom:timer-bar-card
          entities:
            - timer.[[entity_name]]_lights_off_timer
          invert: true
          sync_issues: ignore
          bar_height: 2px
          bar_foreground: orange
          bar_background: '#111'
          layout: full_row
          text_width: 0px
          bar_width: 100%
          card_mod:
            style: |
              :host {
                width: 100%;
                margin: 0px;
                padding: 0px;
                border: 0px;
              }
              ha-card {
                left: 44%;
                width: 113%;
                height: 4px;
                padding: 0px;
                z-index: 3;
                margin: 0px;
                margin-top: -39px;
                border: 0px;
                background-color: rgb(0,0,0,0);
                box-shadow: 0px 0px 2px rgb(255,255,255,0);
              }
      entity: light.[[entity_name]]_lights
      image: local/rooms/room_[[entity_name]].jpg
      state_filter:
        'on': brightness(100%) saturate(1.2)
        'off': brightness(40%) grayscale(100%) contrast(150%)
      card_mod:
        style: |
          ha-card {
            top: 0%;
            border: 0px;
            border-top-left-radius: 8px;
            border-top-right-radius: 8px;
            border-bottom-left-radius: 8px;
            border-bottom-right-radius: 8px;
            border-color: rgba(0,0,0,0)
            z-index: 0;
          }
```

## Using the card

```yaml
type: custom:decluttering-card
template: area_card
variables:
  - entity_name: living_room
  - display_name: Living Room
  - temperature_sensor: sensor.airthings_wave_temperature
  - device_1: media_player.70pus9005_12_2
  - device_1_icon: mdi:television
  - device_1_color: green
  - device_1_state: "on"
  - device_1_animation: none
  - device_2: binary_sensor.backyard_door_sensor_contact
  - device_2_icon: mdi:door
  - device_2_color: red
  - device_2_state: "on"
  - device_2_animation: blink
  - device_3: binary_sensor.inner_back_door_contact
  - device_3_icon: mdi:door-open
  - device_3_color: red
  - device_3_state: "on"
  - device_3_animation: blink
  - device_4: input_select.sofa_presence
  - device_4_icon: mdi:sofa
  - device_4_state: presence
  - device_4_color: green
  - device_4_animation: none
  - device_5: fan.philips_air_purifier
  - device_5_icon: mdi:air-filter
  - device_5_state: "on"
  - device_5_color: green
  - device_5_animation: none
  - device_6: light.fireplace
  - device_6_icon: mdi:fireplace
  - device_6_state: "on"
  - device_6_color: orange
  - device_6_animation: none
layout_options:
  grid_columns: 2
```
