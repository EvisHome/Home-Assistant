## UNRAID DASHBOARD

![Unraid Overview](/dashboards/unraid/img/HA-Unraid-dashboard-overview.png)

## HOME ASSISTANT ADD-ONS

* MQTT Broker

&nbsp;

## INTEGRATIONS

List of integrations needed to set this up:

* [Unraid API](https://github.com/ElectricBrainUK/UnraidAPI) - This will allow you to control the 
* Glances
* [Monitor Docker](https://github.com/ualex73/monitor_docker) - I am using this as my default integration to control any docker instance.
* [browser_mod](https://github.com/thomasloven/hass-browser_mod) (this is used for custom popup, to provide more details on the Docker containers.

&nbsp;

### UNRAID

On Unraid side, you need to setup these.

**1. Unraid-API**

The setup process is really well described [here](https://github.com/ElectricBrainUK/UnraidAPI) by ElectricBrainUK

&nbsp;

**2. Glances**

Setup Glances docker container in Unraid

&nbsp;

**3. Monitor Docker**

&nbsp;

### HOME ASSISTANT

**1. Unraid-API**

The setup process is really well described [here](https://github.com/ElectricBrainUK/UnraidAPI) by ElectricBrainUK

&nbsp;

**2. Glances**

On Home Assistant side connection to to your Glances docker is easy, through default integration.

&ensp;&ensp; *Configurations -> Devices & Services -> Add Integration*

Search for Glances and fill in the setup form. You want to use unique name (e.g. Unraid-1) so that it's easier to indentify the entities when you start having multiple Glances integrations.

&nbsp;

## CARDS
