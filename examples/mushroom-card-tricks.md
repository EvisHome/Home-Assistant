# Home Assistant Mushroom Card - Card Mod Tricks

### Mushroom Chips Card
```YAML
type: custom:mushroom-chips-card
chips:
```

### Wobbling Chip

```YAML
# Wobbling Template Chip
  - type: template
    icon: mdi:washing-machine
    icon_color: orange
    card_mod:
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
          animation: wobbling 0.1s linear infinite alternate;
        }
```
