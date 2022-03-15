## DOCKER SERVER (Dashboard)

Standard HA Integrations
* Glances (glances container needs to run on the remote docker)

Custom Integrations Used:
* [Monitor Docker](https://github.com/ualex73/monitor_docker) (dockerproxy container needs to run on the remote docker)
* [Scheduler](https://github.com/nielsfaber/scheduler-component)
* [ESXi Stats](https://github.com/wxt9861/esxi_stats) (This Docker server runs as VM in ESXi, to fully use this a proper license is needed)

Frontend Cards:
* [scheduler-card](https://github.com/nielsfaber/scheduler-card) (For Weekly Backup Jobs, Montlys is a BigTimer in Node-RED)
* [button-card](https://github.com/custom-cards/button-card)
* [mini-graph-card](https://github.com/kalkih/mini-graph-card)
* [auto-entities](https://github.com/thomasloven/lovelace-auto-entities)
* [card-mod](https://github.com/thomasloven/lovelace-card-mod)

## NETWORK (Dashboard)

Standard HA Integrations:
* Unifi Network

Custom Integrations Used:
* [sensor.unifigateway](https://github.com/custom-components/sensor.unifigateway)
* [unifi-device-info](https://github.com/w1tw0lf/Unifi-Device-info) | created separate sensors scripts for APs, switch and UDMP to pull more info.

Custom HACS frontend cards & elements used:
* [mini-graph-card](https://github.com/kalkih/mini-graph-card)
* [card-mod](https://github.com/thomasloven/lovelace-card-mod)

![HA Overview](/examples/Network-dashboard.png)

## Access Points (Dashboard)

![Access Points](/examples/HA-AccessPoints.png)

## DNS (Dashboard)

Standard HA Integrations:
* Adguard Home
* Glances

Custom Integrations Used:
* Monitor Docker

Custom HACS frontend cards & elements used:
* [multiple-entity-row](https://github.com/benct/lovelace-multiple-entity-row)
* [mini-graph-card](https://github.com/kalkih/mini-graph-card)

![DNS](/examples/HA-DNS-dashboard.png)
