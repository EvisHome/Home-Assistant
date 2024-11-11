# Building DIY a smart speaker

Building a speaker which can control the Home Assistant smart home in my local language (finnish) or in english, inform me about about what is going on at my home, and answer what ever questions I might have.

This projects uses paid subscriptions from Nabu Casa and from OpenAI. You will need a working Home Assistant installation.


### **Parts used**
* Raspberry Pi Zero 2 W
* 2x20 Pin Header for the Pi
* [SeeedStudio ReSpeaker 2-MICS Pi Hat](https://www.amazon.de/dp/B07CXSW6LB?ref=ppx_yo2ov_dt_b_fed_asin_title)
* [Adafruit Speaker - 3" Diameter - 4 Ohm 3 Watt](https://www.amazon.de/dp/B00QSIYXLK?ref=ppx_yo2ov_dt_b_fed_asin_title) - (optionally you could use the 3.5mm speaker jacket for external speaker)
* Micro SD card (I used 16GB Scandisk Ultra)
* Power adapter with a microUSB cord for the Pi - (I used an old 5V 2A power adapter)
* [Cable with JST PH 2 pin micro plug](https://www.amazon.de/dp/B0CBWX6JM7?ref=ppx_yo2ov_dt_b_fed_asin_title) - (connecting the speaker to the ReSpeaker 2-MICS Hat)

### **Software used**
* [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
* [PuTTy](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjHh-Wo_9OJAxUbIxAIHVVVFhQQFnoECAoQAQ&url=https%3A%2F%2Fwww.putty.org%2F&usg=AOvVaw0iOGrunharr0YuZtN9wsn1&opi=89978449) (for SSH to the Pi)
* [Home Assistant](https://www.home-assistant.io/) (with [Nabu Casa](https://www.nabucasa.com/) subscription for STT & TTS)
* [OpenAI](https://platform.openai.com/) (with subscription/paid model)

