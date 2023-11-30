# WLED

check these
* [WLED](https://kno.wled.ge/)
* [WLED install](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwj6-ZOry-yCAxVJJxAIHar3AskQFnoECAYQAQ&url=https%3A%2F%2Finstall.wled.me%2F&usg=AOvVaw22lJJR6nIpfJtgyzCe5nuF&opi=89978449)

## Components
For this project I used White PCB with IP65 and 5m 150leds .. pick what suites your needs. (also got 5m 300leds which I'll use elsewhere) and punch of SK6812 leds which have separate white pixel aswell.

Calculate your power need based on the amount of leds you are going to use example with strip of 2 meters which has 30leds/m each led max power is 0.3W. 2x30 = 60 leds. 60*0.3W = 18W .. pick something higher than that to be on thesafe side.

* [WS2812B Eco All LED](https://www.amazon.de/dp/B088FJBKS2?ref=ppx_yo2ov_dt_b_product_details&th=1) - White PCB with IP65 and 5m 150leds
* [Power Supply](https://www.amazon.de/-/en/gp/product/B08SVX1TH5/ref=ewc_pr_img_2?smid=A8TRRVFVXLMD9&th=1) - 25W version is more than enough for my 170cm cut.
* [D1 Mini NodeMCU](https://www.amazon.de/-/en/gp/product/B0754W6Z2F/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) but you can go with ESP32 as well, should be more powerful if you use more leds.

## WLED Fireplace Preset
Used the ColorTwinkles as the base and tuned speeds and colors

API Command
```
{"on":true,"bri":255,"transition":7,"mainseg":0,"seg":[{"id":0,"start":0,"stop":52,"grp":1,"spc":0,"of":0,"on":true,"frz":false,"bri":255,"cct":127,"set":0,"col":[[255,160,0],[0,0,0],[0,0,0]],"fx":74,"sx":56,"ix":139,"pal":3,"c1":128,"c2":128,"c3":16,"sel":true,"rev":false,"mi":false,"o1":false,"o2":false,"o3":false,"si":0,"m12":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0},{"stop":0}]}
```
