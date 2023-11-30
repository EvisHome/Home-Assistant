## ESXi DASHBOARD

### *This might not work properly anymore? I have moved to Proxmox myself, and haven't maintained this for a while.*

Monitor and control your ESXi host and virtual machines. I wanted to have a single page overview of my home ESXi installation, to monitor and have notifications/alerts and some automations like taking snapshots.

*E.g I have my Plex instance alerting me if there is a new server version available, with an actionable notification (showing also if there is someone currently streaming, link to release notes, and button to update the server). When I press update, the automation waits until no streams are active, takes a snapshot (or a Veeam Backup) of the VM and updates the Plex. (These automations and notification are mostly built with Node-RED*

Couple of notications running for datastores and high CPU.

From the dashboard you can also run some service calls (these need a "real" ESXi license to access the API)

* Start/Stop/Suspend VMs
* Take Snapshot of a VM

![ESXi Overview](/dashboards/esxi-vm-dashboard/img/HA_ESXi_dashboard.gif)

&nbsp;

&nbsp;

## INTEGRATIONS

List of integrations needed to set this up:

* [ESXi_Stats](https://github.com/wxt9861/esxi_stats)

&nbsp;

&nbsp;

## HELPERS

To make the graphs collapsible, there is one helper switch switch.esxi_vm_graphs, that controls the state.

* switch.esxi_vm_graphs

&nbsp;

&nbsp;

## CONFIGURATIONS

I calculate the datastore used space, used in the "donuts", with this template sensor.

```
#sensor:
  - platform: template
    sensors:
      esxi_datastore1_used_space_gb:
        value_template: >-
          {{ (state_attr('sensor.esxi_datastore_datastore1', 'total_space_gb') | float - states('sensor.esxi_datastore_datastore1') | float) }}
        unit_of_measurement: 'GB'
        friendly_name: ESXi Datastore 1 Used Space
```

&nbsp;

&nbsp;

## VIEW & CARDS

Standard Masonry view was used for this

### FRONTEND ELEMENTS & CUSTOM CARDS

List of cards used:

* vertical-stack
* horizontal-stack
* picture-elements
* entities
* entity
* custom:layout-card
* custom:button-card
* custom:auto-entities
* custom:apexcharts-card



