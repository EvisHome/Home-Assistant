## UNRAID DASHBOARD

![Unraid Overview](/dashboards/unraid/img/HA-Unraid-dashboard-overview.png)

## INTEGRATIONS

List of integrations needed to set this up

* Unraid API
* Glances
* Monitor Docker
* browser_mod

### UNRAID

On Unraid side, three Docker containers needs to be set first

**1. Unraid-API**

**2. Glances**

**3. Monitor Docker**

### HOME ASSISTANT

**3. Glances**

On Home Assistant side connection to to your Glances docker is easy, through default integration.

&ensp;&ensp; *Configurations -> Devices & Services -> Add Integration*

Search for Glances and fill in the setup form. For name you want to use unique name (e.g. Unraid-1) so that it's easier to indentify the entities if you have multiple Glances integrations.

## CARDS
