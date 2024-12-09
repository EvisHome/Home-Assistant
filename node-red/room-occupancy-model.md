# Room & Area Occupancy Model

## Overview

In each area and room where three are sensors, this flow updates 2 helper entities input_boolean.area_occupancy is set on or off, and input_select.area_presence to one of these options presence | idle | absence. 

Idle here presents a defined time between presence and absence mode, when the room was recently occupied, but sensor is not detecting occupancy anymore. After the idle time has passed the input_select.area_presence changes to absent.

The input_select.area_presence is then to visualize the current area or room occupancy state in my declutter "room card".

The input_select.area_presence is also used in my light automations which can be set the presence mode, absence detection, manual mode or follow-the-sun mode.

For clarity the Node-Red flow has been divided to a subflow, which has one envinronment variable [area] that needs to be defined.

## Area Presence Flow & Declutter Room Card

[Check the room card here](https://github.com/EvisHome/Home-Assistant/blob/main/cards/room-card.md)

<p float="left"> <img src="room-card-demo.gif" width="49%" /> <img src="lobby-presence.gif" width="49%" /> </p> 


