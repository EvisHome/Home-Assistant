# ApexChart Card
I use the [ApexChart Card by RomRider ](https://github.com/RomRider/apexcharts-card) quite a lot, I like it how it can be customized to almost what ever I need. Note that for [apexcharts-card](https://github.com/RomRider/apexcharts-card) there are some features/customizations that are not in the document but can be used from the [apexcharts.js docs](https://apexcharts.com/docs/), but can need a bit experimenting.

## ApexChart with background image

![](ApexChart-with-background.png)

Using card_mod and css to add and position a background image. The box-shadow adds an 60% shadow overlay on top of the image to make the graph more visible.

See [apexchart-with-background.yaml](apexchart-with-background.yaml) for full YAML

```YAML
type: custom:apexcharts-card
card_mod:
  style: |
    ha-card {
# background image URL
      background-image: url("/local/room_bedroom.jpg");
      
# centering the background image
      background-position: center;
      
# Resizing the image for the card view
      background-size: 130%
      
# dimming the background with box-shadow
      box-shadow: inset 0 0 0 1000px rgba(0,0,0,.6);
      
# "dirty" adjustment with padding
      padding-top: 10px;
    }
...
```
