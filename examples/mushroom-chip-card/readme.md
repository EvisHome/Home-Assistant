# Mushroom Chip Card - Card Mods

[mushroom-cards](https://github.com/piitaya/lovelace-mushroom) by piitaya

Storing some mods I was experimenting with here as examples/reference

NOTE! Quoting the developer (piitay)
"Be careful with card mod. The structure of the card (name of the components, class, etc…) may change at any time. I can not guarantee you that your override will work with the future update."

### TOC

CHIP ANIMATIONS
* [Wobbling Chip](#wobbling-chip)
* [Rotating Chip](#rotating-chip)
* [Blinking Chip](#blinking-chip)

CHIP STYLING
* [Chip Box Shadow](#chip-box-shadow)
* [Chip Opacity](#chip-opacity)
* [Chip Background Color & Background Opacity](#chip-background-color--opacity)
* [Chip Icon & Text Size](#chip-icon--text-size)

MUSHROOM CHIPS CARD
* [Applying Changes To All Chips](#mushroom-chip-card)

REFERENCING THE ENTITY
* [Referencing the entity withing the cards](d#referencing-the-entity-withing-the-cards)

## MUSHROOM CHIPS CARD
```YAML
type: custom:mushroom-chips-card
chips:
```

### CHIP ANIMATIONS

![image](mushroom-chip-card-animations.gif)

#### Wobbling Chip

```YAML
# Wobbling Template Chip
  - type: template
    icon: mdi:washing-machine
    icon_color: orange
    card_mod:
      style: |

# Keyframes for animation
        @keyframes wobbling {
          0% { transform: rotate(-15deg); }
          100% { transform: rotate(15deg); }

# Animating the chip
        }
        ha-card {
          animation: wobbling 0.1s linear infinite alternate;
        }
```

#### Rotating Chip
```YAML
# Rotating Template Chip
  - type: template
    icon: mdi:fan
    icon_color: green
    card_mod:
      style: |
        @keyframes rotation {
          0% { transform: rotate(0deg); }
          100% { transform: rotate(360deg); }
        }
        ha-card {
          animation: rotation 1s linear infinite;
        }
```

#### Blinking Chip
```YAML
# Blinking Template Chip
  - type: template
    icon: mdi:lightbulb
    icon_color: green
    card_mod:
      style: |
        @keyframes blink {
          50% { opacity: 0; }
        }
        ha-card {
          animation: blink 1s ease infinite;
        }
```

### CHIP STYLING

#### Chip Box Shadow
```YAML
# Shadowless Template Chip
  - type: template
    icon: mdi:lightbulb
    icon_color: green
    card_mod:
      style: |
        ha-card {
# chip box shadow
          --chip-box-shadow: 0px 0px 0px 0px;
        }
```
#### Chip Opacity
```YAML
# 25% Opacity Template Chip
  - type: template
    icon: mdi:lightbulb
    icon_color: green
    card_mod:
      style: |
        ha-card {
# chip opacity
          opacity: 25%;
        }
```

#### Chip Background Color & Opacity
```YAML
# Background color changed & background opacity set to 50%
  - type: template
    icon: mdi:lightbulb
    icon_color: orange
    card_mod:
      style: |
        ha-card {
# chip background color & opacity
          --chip-background: rgba(255,155,155,0.5);
        }
```

#### Chip Icon & Text Size
```YAML
  - type: template
    icon: mdi:lightbulb
    icon_color: orange
    content: text
    card_mod:
      style: |
        ha-card {
# chip icon size
          --chip-icon-size: 0.8em;
# chip font size
          --chip-font-size: 0.5em;
        }
```

#### MUSHROOM CHIP CARD

Applying changes to all chips
* chip sizes withing the chip card
* chips spacing
* chip icon sizes
* chips border radius

![image](mushroom-chip-card-mods.png)

```YAML
alignment: center
card_mod:
  style: |
    ha-card {
      --chip-height: 34px;
      --chip-border-radius: 0px;
      --chip-icon-size: 0.5em;
      --chip-spacing: 2px;
    }
```

## Referencing the entity withing the cards

by using *entity* or *config.entity*

```YAML
  - type: template
    entity: switch.power_socket
    icon: mdi:eye
    icon_color: |
      {% if is_state(entity,'on') %}
        green
      {% else %}
        gray
      {% endif %}
    card_mod: null
    style: |
      ha-card {
        {% if is_state(config.entity,'on') %}
          opacity: 100%;
        {% else %}
          opacity: 25%;
        {% endif %}
      }
```

#### Hide Template Chip If Entity Value Not Withing The Limits
* show sensor value & unit
* change color of the icon based on temperature values

```YAML
      - type: template
        entity: sensor.bedroom_temperature
        content: '{{ states(entity), state_attr(entity,''unit_of_measurement'') }}'
        icon: mdi:thermometer
        icon_color: |
          {% set value = states(entity) | float %}
          {% if value > 27 %}
            red
          {% elif value > 25 %}
            orange
          {% elif value < 20 %}
            blue
          {% else %}
            green
          {% endif %}
        card_mod: null
        style: |
          :host {
            {% set value = states(config.entity) | float %}
            {% if value < 20 or value > 22 %}
              display: flex;
            {% else %}
              display: none;
            {% endif %}
          }
```




