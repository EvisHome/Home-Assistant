# Home Assistant Mushroom Card - Card Mod Tricks

## MUSHROOM CHIPS CARD
```YAML
type: custom:mushroom-chips-card
chips:
```

### CHIP ANIMATIONS

#### Wobbling Chip

```YAML
# Wobbling Template Chip
  - type: template
    icon: mdi:washing-machine
    icon_color: orange
    card_mod:
      style: |
        @keyframes wobbling {
          0% { transform: rotate(-15deg); }
          100% { transform: rotate(15deg); }
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

### Chip Without Shadow

#### Chip Box Shadow
```YAML
# Shadowless Template Chip
  - type: template
    icon: mdi:lightbulb
    icon_color: green
    card_mod:
      style: |
        ha-card {
          /* chip box shadow */
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
          /* chip opacity */
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
          /* chip background color & opacity */
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
          /* chip icon size */
          --chip-icon-size: 0.8em;
          /* chip font size */
          --chip-font-size: 0.5em;
        }
```

#### MUSHROOM CHIP CARD
* change the all chip sizes withing the chip card
* change chips spacing
* change chip icon sizes
* chips border radius

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




