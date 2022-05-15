Check out my whole post here https://lab.evishome.com/ha-nest-protect/

## Dashboard
For the dashboard, I replicated James Callaghans nice looking dashboard, with some small changes.
You can find my Nest Protect YAML from my Github below.

![Synology Overview](/dashboards/nest-protect/Nest-Protect-dashboard.png)

## Node-RED | Automation & Notifications (Android)

For most of my automation I use Node-RED, and as I already have built reusable, actionable notification elements for it I am using the same with these notifications.

My goal was to setup up an actionable Home Assistant notification with one of the actions being able to manually send a predefined SMS message to predefined phone numbers (including neighbors and some family members.) Another manual action is the activation/wake-up of the front door lock, for keyless entry if/when needed.

![image](https://user-images.githubusercontent.com/98347572/168471792-3c6fba85-b2c1-4194-be75-9603b5e1dbec.png)

*Events: state* - these nodes trigger, whenever any of the defined Nest Protect entity states change from the off state. Within the nodes, I have defined a few output properties that are used in the Dynamic Message node to formulate the message sent in the push notification.

*Dynamic Message* - is a function node, which defines the notification message to be sent, and some variables for the msg.

*Alarm Group* - is a subflow which is used to define who in our family gets Alarm type notifications (I have categorized notifications into System, Info, and Alarms) these are helper switches that can be turned on or off inside Home Assistant. This is a reusable subflow element, that I can drag and drop where I need it.

*Action Notification* - is a subflow that actually sends the push notification to the family members who have the Alarm Group helper switch turned on. It also links the next nodes as actions to the message. [Actionable Notifications Subflow for Android](https://zachowj.github.io/node-red-contrib-home-assistant-websocket/cookbook/actionable-notifications-subflow-for-android.html#demo-flow)

## Notification Actions

*Lock activation* - one my actions is the front door activation. The activation allows the door lock to be woken up (at the door) within two minutes from the activation. Once the lock is woken up, the door lock is opened. If the lock is not woken up within 2 minutes it automatically deactivates the lock.

Extended SMS message - purpose is to manually send a predefined SMS message to predefined numbers (neighbors, family members etc.) For the SMS sending, I am using paid service, [ClickSend](https://clicksend.com/?u=324136). It can be integrated to a huge amount of systems, including [Home Assistant](https://integrations.clicksend.com/listings/home-assistant) and [Node-RED](https://integrations.clicksend.com/listings/node-red). (Costs €0.11 per SMS).

## Example Flow

![image](https://user-images.githubusercontent.com/98347572/168472361-eec3a708-9dc8-4d11-a811-8ca22e4eddc9.png)

Copy and import this json to you Node-RED [node-red-notification-example.json](https://github.com/EvisHome/home-assistant/blob/main/dashboards/nest-protect/node-red-notification-example.json). Eeplace the entities, messages etc. with your own. If you are using ClickSend add your own numbers and API authentications.




