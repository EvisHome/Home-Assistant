## DOCKER SERVER (Dashboard)

Integrations Used:
* Monitor Docker
* [Scheduler](* [mini-graph-card](https://github.com/nielsfaber/scheduler-component))
* Glances

Frontend Cards:
* [scheduler-card](https://github.com/nielsfaber/scheduler-card)

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
