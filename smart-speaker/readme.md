# Building DIY a smart speaker

Building a speaker which can control the Home Assistant smart home in my local language (finnish) or in english, inform me about about what is going on at my home, and answer what ever questions I might have.

This projects uses paid subscriptions from Nabu Casa and from OpenAI. You will need a working Home Assistant installation.


### **Parts used**
* Raspberry Pi Zero 2 W
* 2x20 Pin Header for the Pi
* [SeeedStudio ReSpeaker 2-MICS Pi Hat](https://www.amazon.de/dp/B07CXSW6LB?ref=ppx_yo2ov_dt_b_fed_asin_title)
* [Adafruit Speaker - 3" Diameter - 4 Ohm 3 Watt](https://www.amazon.de/dp/B00QSIYXLK?ref=ppx_yo2ov_dt_b_fed_asin_title) - (optionally you could use the 3.5mm speaker jacket for external speaker)
* [Cable with JST PH 2 pin micro plug](https://www.amazon.de/dp/B0CBWX6JM7?ref=ppx_yo2ov_dt_b_fed_asin_title) - (connecting the speaker to the ReSpeaker 2-MICS Hat)
* Micro SD card (I used 16GB Scandisk Ultra)
* Power adapter with a microUSB cord for the Pi - (I used an old 5V 2A power adapter)
* Micro SD card to USB adapter (for installing the Raspberry Pi OS inthe the micro SD card)
* *Optional: M2.5 Hex Spacers* (to support the ReSpeaker Hat)

### **Software used**
* [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
* Raspberry Pi OS Lite (64bit)
* [PuTTy](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjHh-Wo_9OJAxUbIxAIHVVVFhQQFnoECAoQAQ&url=https%3A%2F%2Fwww.putty.org%2F&usg=AOvVaw0iOGrunharr0YuZtN9wsn1&opi=89978449) (for SSH to the Pi)
* [Home Assistant](https://www.home-assistant.io/) (with [Nabu Casa](https://www.nabucasa.com/) subscription for STT & TTS)
* [OpenAI](https://platform.openai.com/) (with subscription/paid model)

<br>

## BUILD

Putting the parts together is quite easy. If you use the Adafruit speaker, tiny bit of soldering is needed.

1. Solder the red wire of the JST cable to the plus (+) side of the speaker and the black wire to the minus (-) side of the speaker
2. Attach the ReSpeaker Hat on to the Raspberry Pi
3. Attach the JST cable to the ReSpeaker 2-pin port

<br>

## Installing OS - Raspberry Pi OS Lite (64bit)
Using the Raspnerry Pi Imager to install the OS

When asking if you'd like to apply customization settings, choose "Edit Settings" and:
* Set a username/password
* Configure the wireless LAN
* Under the Services tab, enable SSH and use password authentication

<br>

## Setting up the Pi (Satellite)

1. Insert the SD card in to the Pi (if you haven't already).
2. attach the MicrUSB power cord to the microUSB port in Pi marked as "power". Optionally you can also power it through the ReSpeaker Hat's microUSB power port.
3. Starting the Pi first time might make it restart few times, but once it is up and running you should find out it's IP address so that you can login through SSH.
4. Once you have the IP address launch **PuTTy**

<br>

Install system dependencies:
```
sudo apt-get update
```
```
sudo apt-get install --no-install-recommends  \
  git \
  python3-venv
```

<br>

Clone the **wyoming-satellite** repository
```
git clone https://github.com/rhasspy/wyoming-satellite.git
```

<br>

Recompile and install the drivers for ReSpeaker 2Mic (this might take some time)
```
cd wyoming-satellite/
sudo bash etc/install-respeaker-drivers.sh
```

<br>

Reboot the Satellite
```
sudo reboot
```
