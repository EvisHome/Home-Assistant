## ESXi DASHBOARD

Monitor and control your ESXi host and virtual machines. I wanted to have a single page overview of my home ESXi installation, to monitor and have notifications/alerts and some automations like taking snapshots.

*E.g I have my Plex instance alerting me if there is a new server version available, with an actionable notification (showing also if there is someone currently streaming, link to release notes, and button to update the server). When I press update, the automation waits until no streams are active, takes a snapshot of the VM and updates the Plex.*

Couple of notications running for datastores and high CPU.

From the dashboard you can also run some service calls (these need a "real" ESXi license to access the API)

* Start/Stop/Suspend VMs
* Take Snapshot of a VM

![ESXi Overview](/dashboards/esxi-vm-dashboard/img/HA_ESXi_dashboard.gif)
