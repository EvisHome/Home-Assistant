# ApexChart Card
I use the ApexChart card quite a lot, I find it more informative with the various axis options, and I like it how it can be customized.

## ApexChart with background image

![](ApexChart-with-background.png)

Using card_mod and css to add and position a background image. The box-shadow adds an 60% shadow overlay on top of the image to make the graph more visible.

```YAML
type: custom:apexcharts-card
card_mod:
  style: |
    ha-card {
      padding-top: 10px;
      background-image: url("/local/room_bedroom.jpg");
      /* centering the background image */
      background-position: center;
      /* Resizing the image for the card view */
      background-size: 130%
      /* dimming the background with box-shadow */
      box-shadow: inset 0 0 0 1000px rgba(0,0,0,.6);
    }
...
...
```
