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
