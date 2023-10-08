## Declutter Room Template Card

``` YAML
type: custom:decluttering-card
template: room_card
variables:
  - entity_name: office
  - display_name: OFFICE
  - temperature_sensor: sensor.bedroom_temperature
  - co2_sensor: sensor.bedroom_co2
  - humidity_sensor: sensor.bedroom_humidity
  - device_1: switch.office_pc_power
  - icon_1: mdi:desktop-classic
  - state_1: 'on'
  - animation_1: none
  - device_2: switch.unraid_power_toggle
  - icon_2: mdi:server
  - state_2: 'on'
  - device_3: switch.td_ds1_2
  - icon_3: mdi:nas
  - state_3: 'on'
  - device_4: media_player.bedroom_echo
  - icon_4: mdi:speaker
  - state_4: playing
  - animation_4: blink
  - device_5: media_player.bedroom_display_2
  - icon_5: mdi:speaker
  - state_5: playing
  - animation_5: blink
  - device_6: sensor.ender_5_pro_current_state
  - icon_6: mdi:printer-3d
  - state_6: Printing
  - animation_6: blink
```

``` YAML
decluttering_templates:
  room_card:
    card:
      type: picture-elements
      elements:
        - type: custom:mushroom-chips-card
          chips:
            - type: template
              entity: input_boolean.[[entity_name]]_occupancy
              content: ''
              icon: mdi:account-circle
              icon_color: |
                {% if is_state(config.entity,'on') %}
                  green
                {% else %}
                  gray
                {% endif %}
              card_mod: null
              style: |
                :host {
                  {% set value = states(config.entity) %}
                  {% if value == 'unknown' or value == 'unavailable' %}
                    display: none;
                  {% else %}
                    display: flex;
                  {% endif %}
                }
                ha-card {
                  --chip-box-shadow: 0px 0px;
                  --chip-background: rgba(0,0,0,0);
                  --chip-border-width: 0;
                }
          alignment: left
          style:
            top: 42%
            left: 50%
            width: 100%
            height: 100%
            z-index: 8
          card_mod:
            style: |
              ha-card {
                --chip-height: 45px;
                --chip-border-radius: 45px;
                --chip-border-width: 0;
              }
        - type: custom:mushroom-chips-card
          chips:
            - type: template
              entity: '[[temperature_sensor]]'
              icon: mdi:thermometer
              icon_color: |
                {% set value = states(entity) | float %}
                {% if value > 27 %}
                  red
                {% elif value > 24 %}
                  orange
                {% elif value < 20 %}
                  blue
                {% else %}
                  green
                {% endif %}
              card_mod: null
              style: |
                ha-icon {
                  font-color: rgba(0,0,0,1);
                }
                :host {
                  {% set value = states(config.entity) %}
                  {% if value == 'unknown' or value == 'unavailable' %}
                    display: none;
                  {% else %}
                    {% set value = value | float %}
                    {% if value < 20 or value > 25 %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                    border: none;
                  {% endif %}
                }
                @keyframes blink {
                  50% { opacity: 0; }
                }
                ha-card {
                  animation: blink 1s ease infinite;
                }
            - type: template
              entity: '[[humidity_sensor]]'
              icon: mdi:water-percent
              icon_color: |
                {% set value = states(entity) | float %}
                {% if value > 55 %}
                  blue
                {% elif value < 20 %}
                  orange
                {% else %}
                  green
                {% endif %}
              card_mod: null
              style: |
                :host {
                  {% set value = states(config.entity) %}
                  {% if value == 'unknown' or value == 'unavailable' %}
                    display: none;
                  {% else %}
                    {% set value = value | float %}
                    {% if value < 20 or value > 55 %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                    border: none;
                  {% endif %}
                }
                @keyframes blink {
                  50% { opacity: 0; }
                }
                ha-card {
                  animation: blink 1s ease infinite;
                }
            - type: template
              entity: '[[co2_sensor]]'
              icon: mdi:molecule-co2
              icon_color: |
                {% set value = states(entity) | float %}
                {% if value > 1500 %}
                  red
                {% elif value > 1200 %}
                  orange
                {% elif value > 800 %}
                  yellow
                {% else %}
                  green
                {% endif %}
              card_mod: null
              style: |
                :host {
                  {% set value = states(config.entity) %}
                  {% if value == 'unknown' or value == 'unavailable' %}
                    display: none;
                  {% else %}
                    {% set value = value | float %}
                    {% if value > 800 %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                    border: none;
                  {% endif %}
                }
                @keyframes blink {
                  50% { opacity: 0; }
                }
                ha-card {
                  animation: blink 1s ease infinite;
                }
            - type: template
              entity: '[[voc_sensor]]'
              icon: mdi:cloud
              icon_color: |
                {% set value = states(entity) | float %}
                {% if value > 1500 %}
                  red
                {% elif value > 250 %}
                  orange
                {% else %}
                  green
                {% endif %}
              card_mod: null
              style: |
                :host {
                  {% set value = states(config.entity) %}
                  {% if value == 'unknown' or value == 'unavailable' %}
                    display: none;
                  {% else %}
                    {% set value = value | float %}
                    {% if value > 250 %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                    border: none;
                  {% endif %}
                }
                @keyframes blink {
                  50% { opacity: 0; }
                }
                ha-card {
                  animation: blink 1s ease infinite;
                }
            - type: template
              entity: '[[pm25_sensor]]'
              icon: mdi:blur
              icon_color: |
                {% set value = states(entity) | float %}
                {% if value > 1500 %}
                  red
                {% elif value > 250 %}
                  orange
                {% else %}
                  green
                {% endif %}
              card_mod: null
              style: |
                :host {
                  {% set value = states(config.entity) %}
                  {% if value == 'unknown' or value == 'unavailable' %}
                    display: none;
                  {% else %}
                    {% set value = value | float %}
                    {% if value > 250 %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                    border: none;
                  {% endif %}
                }
                @keyframes blink {
                  50% { opacity: 0; }
                }
                ha-card {
                  animation: blink 1s ease infinite;
                }
            - type: template
              entity: '[[radon_sensor]]'
              icon: mdi:radioactive
              icon_color: |
                {% set value = states(entity) | float %}
                {% if value > 250 %}
                  red
                {% elif value > 150 %}
                  orange
                {% else %}
                  green
                {% endif %}
              card_mod: null
              style: |
                :host {
                  {% set value = states(config.entity) %}
                  {% if value == 'unknown' or value == 'unavailable' %}
                    display: none;
                  {% else %}
                    {% set value = value | float %}
                    {% if value > 250 %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                    border: none;
                  {% endif %}
                }
                @keyframes blink {
                  50% { opacity: 0; }
                }
                ha-card {
                  animation: blink 1s ease infinite;
                }
          alignment: center
          style:
            top: 82%
            left: 50%
            width: 100%
            height: 100%
            z-index: 7
          card_mod:
            style: |
              ha-card {
                --chip-height: 32px;
                --chip-border-radius: 45px;
                --chip-padding: 0px 4px 0px 4px;
                --chip-spacing: 4px;
                --chip-icon-size: 0.8em;
                --chip-font-size: 0.35em;
                --chip-background: rgba(0,0,0,0.5);
                --chip-box-shadow: 0px 0px;
                --chip-border-width: 0;
              }
        - type: custom:mushroom-chips-card
          chips:
            - type: template
              entity: '[[device_1]]'
              icon: '[[icon_1]]'
              icon_color: |
                {% if is_state(entity,'[[state_1]]') %}
                  green
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[state_1]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[animation_1]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.7);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_2]]'
              icon: '[[icon_2]]'
              icon_color: |
                {% if is_state(entity,'[[state_2]]') %}
                  green
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[state_2]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[animation_2]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.7);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_3]]'
              icon: '[[icon_3]]'
              icon_color: |
                {% if is_state(entity,'[[state_3]]') %}
                  green
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[state_3]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[animation_3]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.7);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_4]]'
              icon: '[[icon_4]]'
              icon_color: |
                {% if is_state(entity,'[[state_4]]') %}
                  green
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[state_4]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[animation_4]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.7);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_5]]'
              icon: '[[icon_5]]'
              icon_color: |
                {% if is_state(entity,'[[state_5]]') %}
                  green
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[state_5]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[animation_5]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.7);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_6]]'
              icon: '[[icon_6]]'
              icon_color: |
                {% if is_state(entity,'[[state_6]]') %}
                  green
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[state_6]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[animation_6]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.7);
                    --chip-border-width: 0;
                  }
          alignment: center
          style:
            top: 120%
            left: 50%
            width: 100%
            height: 100%
            z-index: 7
          card_mod:
            style: |
              ha-card {
                --chip-height: 30px;
                --chip-icon-size: 0.55em;
                --chip-border-radius: 0px;
                --chip-spacing: 1px;
                --chip-background: rgba(0,0,0,0.6);
                --chip-box-shadow: 0px 0px;
                --chip-border-width: 0;
              }
        - type: custom:button-card
          entity: light.[[entity_name]]_lights
          show_name: false
          show_icon: false
          tap_action:
            action: navigate
            navigation_path: /lovelace/[[entity_name]]
          hold_action:
            action: toggle
          style:
            top: 50%
            left: 50%
            width: 100%
            height: 100%
            z-index: 9
          styles:
            card:
              - border-radius: 0px
              - height: 100%
              - background-color: rgb(0,0,0,0)
              - box-shadow: 0px 0px
        - type: custom:button-card
          name: '[[display_name]]'
          style:
            top: 0%
            left: 50%
            width: 102%
            height: 0px
            z-index: 7
          styles:
            name:
              - font-family: verdana
              - font-size: 11px
              - font-weight: bold
              - text-transform: uppercase
              - justify-self: center
              - padding-left: 0px
              - color: rgb(255, 255, 255, 1)
              - text-shadow: 0px 0px 4px rgb(0,0,0,5)
            card:
              - border-radius: 0px
              - border: 0px
              - height: 30px
              - background-color: rgb(0,0,0,0.3)
              - box-shadow: 0px 0px 2px rgb(255,255,255,0)
      entity: light.[[entity_name]]_lights
      image: local/rooms/room_[[entity_name]].jpg
      state_filter:
        'on': brightness(100%) saturate(1.2)
        'off': brightness(40%) grayscale(100%) contrast(150%)
      style: |
        ha-card {
          border-top-left-radius: 8px;
          border-top-right-radius: 8px;
          border-bottom-left-radius: 8px;
          border-bottom-right-radius: 8px;
          z-index:0
        }
```
