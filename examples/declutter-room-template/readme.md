## Declutter Room Template Card

* custom:button-card

``` YAML
type: custom:decluttering-card
template: area_card
variables:
  - entity_name: office
  - display_name: OFFICE
  - temperature_sensor: sensor.bedroom_temperature
  - sensor_1: sensor.bedroom_co2
  - sensor_1_state: 'on'
  - sensor_1_icon: mdi:molecule-co2
  - sensor_1_color: red
  - sensor_1_animation: none
  - device_1: switch.office_pc_power
  - device_1_color: green
  - device_1_icon: mdi:desktop-classic
  - device_1_state: 'on'
  - device_1_animation: none
  - device_2: switch.office_pc_power
  - device_2_icon: mdi:server
  - device_2_state: 'on'
  - device_2_animation: blink
  - device_3: switch.office_pc_power
  - device_3_icon: mdi:nas
  - device_3_state: 'on'
  - device_4: switch.office_pc_power
  - device_4_color: blue
  - device_4_icon: mdi:speaker
  - device_4_state: 'on'
  - device_4_animation: blink
  - device_5: switch.office_pc_power
  - device_5_color: blue
  - device_5_icon: mdi:speaker
  - device_5_state: 'on'
  - device_5_animation: blink
  - device_6: switch.office_pc_power
  - device_6_color: orange
  - device_6_icon: mdi:printer-3d
  - device_6_state: 'on'
  - device_6_animation: blink
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
            z-index: 7
            container-type: inline-size
          card_mod:
            style: |
              ha-card {
                --chip-height: 12cqw;
                --chip-icon-size: 6cqw;
                --chip-border-radius: 5px;
                --chip-spacing: 2px;
                --chip-background: rgba(0,0,0,0);
                --chip-box-shadow: 0px 0px;
                --chip-border-width: 0;
              }
      entity: light.[[entity_name]]_lights
      image: local/rooms/room_[[entity_name]].jpg
      state_filter:
        'on': brightness(100%) saturate(1.2)
        'off': brightness(40%) grayscale(100%) contrast(150%)
      card_mod:
        style: |
          ha-card {
            border-top-left-radius: 8px;
            border-top-right-radius: 8px;
            border-bottom-left-radius: 8px;
            border-bottom-right-radius: 8px;
            z-index:0
          }
```
