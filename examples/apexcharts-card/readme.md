# ApexCharts Card
I use the [ApexCharts Card by RomRider ](https://github.com/RomRider/apexcharts-card) quite a lot, I like it how it can be customized to almost what ever I need. Note that for [apexcharts-card](https://github.com/RomRider/apexcharts-card) there are some features/customizations that are not in the document but can be used from the [apexcharts.js docs](https://apexcharts.com/docs/), but can need a bit experimenting.

### TOC

* [ApexCharts with background image](#apexcharts-with-background-image)

## ApexCharts with background image

![](apexcharts-with-background.png)

Using card_mod and css to add and position a background image. The box-shadow adds an 60% shadow overlay on top of the image to make the graph more visible.

See [apexcharts-with-background.yaml](apexcharts-with-background.yaml) for full YAML

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

In my room card I am using the chart without header or legend values, since I implemented other cards to show the values either all the time or if set threshold are triggered. Anyway the header and/or the legend values are easy to enable in the config.

![](apexcharts-with-background-and-labels.png)

## Multiple ApexCharts Background In a Swipe Card

If you have multiple charts on your dashboard, but do not nessarily need to monitor them all at once you can save some screen space and put them on a swipe card and set it on autoplay, and stop it if interacted with.

![](swipe-card-charts.gif)

```YAML
type: custom:swipe-card
# which card is shown first
start_card: 1
parameters:
# If you want to show navigation arrows, uncomment the line 'navigation: null'
#  navigation: null
  navigation: null
  autoplay:
# this will disable autoplay if interacted with.
    disableOnInteraction: true
# Time to show one chart
    delay: 5000
  scrollbar:
    hide: false
    draggable: true
    snapOnRelease: false
cards:
```

