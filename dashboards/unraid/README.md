## UNRAID DASHBOARD

Monitor and control you Unraid instance(s). This allows run Mover, Parity Check, Power Unraid On/Off, monitor various statistics, control and monitor Docker containers. And you can build automations and alarms based on all these sensors or like actionable notifications of containers with higher than normal CPU/MEM usage etc. .. imaginations is the limit.


![Unraid Overview](/dashboards/unraid/img/HA-Unraid-dashboard-overview.png)

## HOME ASSISTANT ADD-ONS

* MQTT Broker

&nbsp;

&nbsp;

## INTEGRATIONS

List of integrations needed to set this up:

* [Unraid API](https://github.com/ElectricBrainUK/UnraidAPI) - This will allow you to control the 

* [Glances](https://github.com/nicolargo/glances) - This is my go to integration for monitoring my servers statistics (depending on your system and OS you can get different access to different sensors, CPU usage, RAM usages, disck usasge, container stats, temps, Fan speeds etc.)

* [Monitor Docker](https://github.com/ualex73/monitor_docker) & [Docker-Socket-Proxy](https://github.com/Tecnativa/docker-socket-proxy) - Control your docker instances/containers, pay attention to the security! I am using this as my integration to my other docker instances also, but you could instead modify the dashboard to use Unraid-API only.

* [browser_mod](https://github.com/thomasloven/hass-browser_mod) - In this dashboard I used browser_mod for custom popups, to provide more details on the Docker containers.

&nbsp;

&nbsp;

### UNRAID

On Unraid side, you must have Docker enabled to setup the containers below.

**1. Unraid-API**

The setup process is really well described [here](https://github.com/ElectricBrainUK/UnraidAPI) by ElectricBrainUK

&nbsp;

**2. Glances**

Setup Glances docker container in Unraid, this is quite straight forward.

&ensp;&ensp; APPS -> Search for Glances -> Install

Take note of the ip and port you Glances is runnign, you need these in Home Assistant when setting up the integration. You can also open the WebUI to check all the info Glances is giving (Note! all might not be available through the integration).

&nbsp;

**3. Monitor Docker & Docker-Socket-Proxy**

In order the Monitor Docker integration to work, you need run to Docker-Socket-Proxy on Unraid side. Check the QA part of the [Monitor Docker readme](https://github.com/ualex73/monitor_docker), also check the [Tecnativa Docker-Socket-Proxy](https://github.com/Tecnativa/docker-socket-proxy) security recommendations.

&nbsp;

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

**3. Docker Monitor**

Install Monitor Docker through HACS [Monitor Docker readme](https://github.com/ualex73/monitor_docker). To use the monitor_docker you have to add the config in to your configuration.yaml, below is my config.

```YAML
## MONITOR DOCKER ##
monitor_docker:
  - name: UnraidDocker
    url: tcp://Your-Unraid-IP:Docker-Socket-Proxy-Port
    scan_interval: 30
    monitored_conditions:
      - version
      - containers_running
      - containers_paused
      - containers_stopped
      - containers_cpu_percentage
      - containers_memory_percentage
      - cpu_percentage
      - health
      - uptime
      - memory
      - memory_percentage
      - network_speed_up
      - network_speed_down
      - allinone
```

&nbsp;

&nbsp;

## VIEW & CARDS

For this view I used I used *View Type Horizontal (layout-card)* and *vertical-stacks* to define the columns of cards. You can easily arrange yours as needed.

### FRONTEND ELEMENTS & CUSTOM CARDS

List of cards used:

* vertical-stack
* horizontal-stack
* picture-elements
* custom:layout-card
* custom:button-card
* custom:auto-entities
* custom:bar-card
* custom:apexcharts-card
* history-graph
* custom:logbook-card

&nbsp;

&nbsp;

### CARDS


