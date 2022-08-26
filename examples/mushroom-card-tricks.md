# Home Assistant Mushroom Card - Card Mod Tricks

### Mushroom Card Chips

### Wobbling Chip

```YAML
type: custom:mushroom-chips-card
chips:
  - type: template
    entity: null
    icon: mdi:washing-machine
    icon_color: green
    card_mod: null
    style: |
      @keyframes wobbling {
        0% {
          transform: rotate(-15deg);
        }
        100% {
          transform: rotate(15deg);
        }
      }
      ha-card {
        --chip-box-shadow: 0px 0px;
        animation: wobbling 0.1s linear infinite alternate;
        }
```
