## UNRAID DASHBOARD

![Unraid Overview](/dashboards/unraid/img/HA-Unraid-dashboard-overview.png)

## ADD-ONS

* MQTT Broker

&nbsp;

## INTEGRATIONS

List of integrations needed to set this up:

* [Unraid API](https://github.com/ElectricBrainUK/UnraidAPI)
* Glances
* [Monitor Docker](https://github.com/ualex73/monitor_docker)
* browser_mod

&nbsp;

### UNRAID

On Unraid side, three Docker containers needs to be set first

**1. Unraid-API**

The setup process is really well described [here](https://github.com/ElectricBrainUK/UnraidAPI/wiki/Home-Assistant-Integration) by ElectricBrainUK

&nbsp;
**2. Glances**

&nbsp;
**3. Monitor Docker**

&nbsp;

### HOME ASSISTANT

**1. Unraid-API**

&nbsp;

**2. Glances**

On Home Assistant side connection to to your Glances docker is easy, through default integration.

&ensp;&ensp; *Configurations -> Devices & Services -> Add Integration*

Search for Glances and fill in the setup form. You want to use unique name (e.g. Unraid-1) so that it's easier to indentify the entities when you start having multiple Glances integrations.

&nbsp;

## CARDS
