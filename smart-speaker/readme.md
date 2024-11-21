# Building DIY a smart speaker

Building a speaker which can control the Home Assistant smart home in my local language (finnish) or in english, inform me about about what is going on at my home, and answer what ever questions I might have.

This projects uses paid subscriptions from Nabu Casa and from OpenAI. You will need a working Home Assistant installation.

<br>

## TOC

* [Parts Used](#Parts-Used)
* [Software Used](#Software-Used)
* [Building The Speaker](#Build)
* [Installing OS](#Installing-OS)
* [Setting Up The Wyoming Satellite](#Setting-Up-The-Wyoming-Satellite)
* [Checking The Audio Devices](#Checking-The-Audio-Devices)
* [Home Assistant Discovery](#Home-Assistant-Discovery)
* [Audio Enhancements](#Audio-Enhancements)
* [Local Wake Word Detection](#Local-Wake-Word-Detection)
* [LED service](#LED-service)

<br>

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

### **Software Used**
* [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
* Raspberry Pi OS Lite (64bit)
* [PuTTy](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjHh-Wo_9OJAxUbIxAIHVVVFhQQFnoECAoQAQ&url=https%3A%2F%2Fwww.putty.org%2F&usg=AOvVaw0iOGrunharr0YuZtN9wsn1&opi=89978449) (for SSH to the Pi)
* [Home Assistant](https://www.home-assistant.io/) (with [Nabu Casa](https://www.nabucasa.com/) subscription for STT & TTS)
* [OpenAI](https://platform.openai.com/) (with subscription/paid model)

<br>

## Build

Putting the parts together is quite easy. If you use the Adafruit speaker, tiny bit of soldering is needed.

1. Solder the red wire of the JST cable to the plus (+) side of the speaker and the black wire to the minus (-) side of the speaker
2. Attach the ReSpeaker Hat on to the Raspberry Pi
3. Attach the JST cable to the ReSpeaker 2-pin port

<br>

## Installing OS
Using the Raspnerry Pi Imager to install the OS, Raspberry Pi OS Lite (64bit)

When asking if you'd like to apply customization settings, choose "Edit Settings" and:
* Set a username/password
* Configure the wireless LAN
* Under the Services tab, enable SSH and use password authentication

*if SSH is not working for some reason, then this can be fixed, by adding a file in to the boot (bootfs).
Add a file called **ssh** into the bootfs directory. And restart the Pi, now SSH with the created username and password should work.*

<br>

## Setting up the Wyoming Satellite

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

<br>

Reconnect to the satellite with SSH and continue
```
cd wyoming-satellite/
python3 -m venv .venv
.venv/bin/pip3 install --upgrade pip
.venv/bin/pip3 install --upgrade wheel setuptools
.venv/bin/pip3 install \
  -f 'https://synesthesiam.github.io/prebuilt-apps/' \
  -r requirements.txt \
  -r requirements_audio_enhancement.txt \
  -r requirements_vad.txt
```
Test if the installation was succesful
```
script/run --help
```

<br>

## Checking The Audio Devices

### List your available microphones
```
arecord -L
```
With ReSpeaker 2MIC Hat you should see
```
plughw:CARD=seeed2micvoicec,DEV=0
    seeed-2mic-voicecard, bcm2835-i2s-wm8960-hifi wm8960-hifi-0
    Hardware device with all software conversions
```
![image](https://github.com/user-attachments/assets/56ae517d-21ed-45e9-afa3-82fd295acbcb)

Record a 5 second sample
```
arecord -D plughw:CARD=seeed2micvoicec,DEV=0 -r 16000 -c 1 -f S16_LE -t wav -d 5 test.wav
```

<br>

### List your speakers
```
aplay -L
```
With ReSpeaker 2MIC Hat you should see
```
plughw:CARD=seeed2micvoicec,DEV=0
    seeed-2mic-voicecard, bcm2835-i2s-wm8960-hifi wm8960-hifi-0
    Hardware device with all software conversions
```
![image](https://github.com/user-attachments/assets/6cd08e11-b900-427b-8125-5d9e8d0cd8bc)

<br>

Play back your recorded sample WAV:
```
aplay -D plughw:CARD=seeed2micvoicec,DEV=0 test.wav
```
You should be hearing the sample you recorded.
**Make note of your microphone and speaker devices, those will be needed for running the satellite**

## Running the Satellite

In the directory *wyoming-satellite* run the the following. Change the name to you area or room.

```
script/run \
  --debug \
  --name 'office satellite' \
  --uri 'tcp://0.0.0.0:10700' \
  --mic-command 'arecord -D plughw:CARD=seeed2micvoicec,DEV=0 -r 16000 -c 1 -f S16_LE -t raw' \
  --snd-command 'aplay -D plughw:CARD=seeed2micvoicec,DEV=0 -r 22050 -c 1 -f S16_LE -t raw'
```

<br>

## Home Assistant Discovery

After a while you should see the the satellite as *Discovered (Wyoming Protocol)*, you can clikc *Configure* and *Submit*, choose the area for your satellite and click *Finish*.

![image](https://github.com/user-attachments/assets/6de9e63f-507c-4568-94dc-577385de3077)

![image](https://github.com/user-attachments/assets/468d5a55-13ae-4544-8970-0dcb8efcbc3f)



<br>

## Create Services

Running wyoming-satellite as a systemd service

create a service file
```
sudo systemctl edit --force --full wyoming-satellite.service
```

Insert the content in to the file. Change the *evis* to what every your directiory is.
```
[Unit]
Description=Wyoming Satellite
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
ExecStart=/home/evis/wyoming-satellite/script/run \
  --name 'office satellite' \
  --uri 'tcp://0.0.0.0:10700' \
  --mic-command 'arecord -D plughw:CARD=seeed2micvoicec,DEV=0 -r 16000 -c 1 -f S16_LE -t raw' \
  --snd-command 'aplay -D plughw:CARD=seeed2micvoicec,DEV=0 -r 22050 -c 1 -f S16_LE -t raw'
WorkingDirectory=/home/evis/wyoming-satellite
Restart=always
RestartSec=1

[Install]
WantedBy=default.target
```

Save the file and exit with the editor *CTRL + X*

<br>

Enable the service to start at boot
```
sudo systemctl enable --now wyoming-satellite.service
```

To get back to the shell prompt use *CRTL + C*

To check the logs in real-time
```
journalctl -u wyoming-satellite.service -f
```
When needed the service can be disabled and stopped with
```
sudo systemctl disable --now wyoming-satellite.service
```

## Audio Enhancements
Using Automatic gain control and noise suppression
```
script/run \
  ... \
  --mic-auto-gain 5 \
  --mic-noise-suppression 2
```

```
  --mic-volume-multiplier X
```

```
  --snd-volume-multiplier 0.25
```

## Local Wake Word Detection

Install dependencies

```
sudo apt-get update
```
```
sudo apt-get install --no-install-recommends  \
  libopenblas-dev
```

In your *home* directory clone the repository and run
```
git clone https://github.com/rhasspy/wyoming-openwakeword.git
```
```
cd wyoming-openwakeword
script/setup
```

Create a systemd service for open wake word
```
sudo systemctl edit --force --full wyoming-openwakeword.service
```

Replace the /home/evis directories with your home directories
```
[Unit]
Description=Wyoming openWakeWord

[Service]
Type=simple
ExecStart=/home/evis/wyoming-openwakeword/script/run \
  --uri 'tcp://127.0.0.1:10400'
WorkingDirectory=/home/evis/wyoming-openwakeword
Restart=always
RestartSec=1

[Install]
WantedBy=default.target
```

### Update the Satellite Service

```
sudo systemctl edit --force --full wyoming-satellite.service
```

update the parts below

```
[Unit]
...
Requires=wyoming-openwakeword.service

[Service]
...
ExecStart=/home/pi/wyoming-satellite/script/run ... \
  --wake-uri 'tcp://127.0.0.1:10400' \
  --wake-word-name 'ok_nabu'
...

[Install]
...
```
You can change the wake word to any of the included ones:

* ok_nabu
* hey_jarvis
* alexa
* hey_mycroft
* hey_rhasspy


Reload the Satellite Service and restart it
```
sudo systemctl daemon-reload
```
```
sudo systemctl restart wyoming-satellite.service
```

You should see the open wake word service automatically loaded

```
sudo systemctl status wyoming-satellite.service wyoming-openwakeword.service
```

Both services should read "active (running)" and show up as green color

Testing this now by saying (I have an entity called office lights in Home Assistant)

*ok, nabu. turn off office lights*

Use journal to check the logs of services for errors

```
sudo systemctl status wyoming-satellite.service wyoming-openwakeword.service
```

If you make changes remember to run 
```
sudo systemctl daemon-reload
```

## LED service

The ReSpeaker 2MIC hat has some LEDs included, and this will change the color of the LEDs depending on the stallite state.

From your home directory, run

```
cd wyoming-satellite/examples
python3 -m venv --system-site-packages .venv
.venv/bin/pip3 install --upgrade pip
.venv/bin/pip3 install --upgrade wheel setuptools
.venv/bin/pip3 install 'wyoming==1.5.2'
```

```
sudo apt-get install python3-spidev python3-gpiozero
```

Test the service
```
.venv/bin/python3 2mic_service.py --help
```

Create a new systemd service for the LEDs
```
sudo systemctl edit --force --full 2mic_leds.service
```

insert

```
[Unit]
Description=2Mic LEDs

[Service]
Type=simple
ExecStart=/home/evis/wyoming-satellite/examples/.venv/bin/python3 2mic_service.py \
  --uri 'tcp://127.0.0.1:10500'
WorkingDirectory=/home/evis/wyoming-satellite/examples
Restart=always
RestartSec=1

[Install]
WantedBy=default.target
```

Updating the Satellite service
```
sudo systemctl edit --force --full wyoming-satellite.service
```

with the parts ..
```
[Unit]
...
Requires=2mic_leds.service

[Service]
...
ExecStart=/home/evis/wyoming-satellite/script/run ... \
  --event-uri 'tcp://127.0.0.1:10500'
...

[Install]
...
```

Reload and restart the satellite service
```
sudo systemctl daemon-reload
```
```
sudo systemctl restart wyoming-satellite.service
```

Check that the LED service is automatically loaded
```
sudo systemctl status wyoming-satellite.service 2mic_leds.service
```

Try a voice command and you should see the LEDs change color based ot the status.

To check the logs run
```
journalctl -u 2mic_leds.service -f
```


**When ever you make changes to the service, remember to run**
```
sudo systemctl daemon-reload
```
