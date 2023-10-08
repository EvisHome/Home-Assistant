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
            navigation_path: /dashboard-dev/declutter/#[[entity_name]]
          hold_action:
            action: toggle
          double_tap_action:
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
            top: 50%
            left: 50%
            width: 100%
            height: 100%
            z-index: 7
            container-type: inline-size
          styles:
            card:
              - border-radius: 0px
              - border: 0px
              - height: 29%
              - background-color: rgb(0,0,0,0.5)
              - box-shadow: 0px 0px 2px rgb(255,255,255,0)
              - font-size: 6cqw
            name:
              - font-family: arial
              - font-weight: bold
              - text-transform: uppercase
              - justify-self: center
              - padding-left: 0px
              - color: rgb(255, 255, 255, 1)
              - text-shadow: 0px 0px 4px rgb(0,0,0,1)
        - type: custom:button-card
          entity: input_boolean.[[entity_name]]_occupancy
          icon: mdi:account-circle
          show_name: false
          show_icon: true
          tap_action:
            action: none
          hold_action:
            action: none
          style:
            top: 50%
            left: 50%
            width: 140%
            height: 115%
            z-index: 8
          styles:
            card:
              - border-radius: 0px
              - height: 100%
              - background-color: rgb(0,0,0,0)
              - box-shadow: 0px 0px
            icon:
              - display: none
              - height: 19%
              - top: 0%
              - left: 0%
          state:
            - value: 'on'
              styles:
                icon:
                  - color: lightgreen
                  - display: box
            - value: 'off'
              styles:
                icon:
                  - color: gray
                  - display: box
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
            z-index: 8
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
              - font-size: 5.5cqw
              - font-weight: bold
        - type: custom:mushroom-chips-card
          chips:
            - type: template
              entity: '[[device_1]]'
              icon: '[[device_icon_1]]'
              icon_color: |
                {% if is_state(entity,'[[device_state_1]]') %}
                  [[device_color_1]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_state_1]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_animation_1]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_2]]'
              icon: '[[device_icon_2]]'
              icon_color: |
                {% if is_state(entity,'[[device_state_2]]') %}
                  [[device_color_2]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_state_2]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_animation_2]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_3]]'
              icon: '[[device_icon_3]]'
              icon_color: |
                {% if is_state(entity,'[[device_state_3]]') %}
                  [[device_color_3]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_state_3]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_animation_3]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_4]]'
              icon: '[[device_icon_4]]'
              icon_color: |
                {% if is_state(entity,'[[device_state_4]]') %}
                  [[device_color_4]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_state_4]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_animation_4]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_5]]'
              icon: '[[device_icon_5]]'
              icon_color: |
                {% if is_state(entity,'[[device_state_5]]') %}
                  [[device_color_5]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_state_5]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_animation_5]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
            - type: template
              entity: '[[device_6]]'
              icon: '[[device_icon_6]]'
              icon_color: |
                {% if is_state(entity,'[[device_state_6]]') %}
                  [[device_color_6]]
                {% else %}
                  gray
                {% endif %}
              card_mod:
                style: |
                  @keyframes blink {
                    50% { opacity: 0; }
                  }
                  :host {
                    {% if is_state(config.entity,'[[device_state_6]]') %}
                      display: flex;
                    {% else %}
                      display: none;
                    {% endif %}
                  }
                  ha-card {
                    animation: [[device_animation_6]] 1s ease infinite;
                    --chip-box-shadow: 0px 0px;
                    --chip-background: rgba(0,0,0,0.8);
                    --chip-border-width: 0;
                  }
          alignment: center
          style:
            top: 115%
            left: 50%
            width: 100%
            height: 100%
            z-index: 7
            container-type: inline-size
          card_mod:
            style: |
              ha-card {
                --chip-height: 14cqw;
                --chip-icon-size: 8cqw;
                --chip-border-radius: 0px;
                --chip-spacing: 1px;
                --chip-background: rgba(0,0,0,0);
                --chip-box-shadow: 0px 0px;
                --chip-border-width: 0;
              }
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
