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

![image](https://user-images.githubusercontent.com/98347572/168565679-6e02aaf6-8a34-48d2-8c54-c8fbfd0bcb0f.png)


*Dynamic Message* - is a function node, which defines the notification message to be sent, and some variables for the msg.

![image](https://user-images.githubusercontent.com/98347572/168565775-5425fb0c-0344-439f-abf3-c522423034dd.png)


*Alarm Group* - is a subflow which is used to define who in our family gets Alarm type notifications (I have categorized notifications into System, Info, and Alarms) these are helper switches that can be turned on or off inside Home Assistant. This is a reusable subflow element, that I can drag and drop where I need it.

![image](https://user-images.githubusercontent.com/98347572/168565882-42a90489-1818-4ce3-bdd3-91ad9f9bae1f.png)

*Action Notification* - is a subflow that actually sends the push notification to the family members who have the Alarm Group helper switch turned on. It also links the next nodes as actions to the message. [Actionable Notifications Subflow for Android](https://zachowj.github.io/node-red-contrib-home-assistant-websocket/cookbook/actionable-notifications-subflow-for-android.html#demo-flow)

From the GUI you can define the name, you could define the message also, but I have already done it in the Dynamic Message node so it will just pick that up. I have defined two actions the Extended SMS and front door lock activation. I have defined the notification as Sticky, and color as red.

![image](https://user-images.githubusercontent.com/98347572/168566157-fb5e3ae3-9b5f-4c00-951a-ca132b317303.png)


## Notification Actions

*Lock activation* - one my actions is the front door activation. The activation allows the door lock to be woken up (at the door) within two minutes from the activation. Once the lock is woken up, the door lock is opened. If the lock is not woken up within 2 minutes it automatically deactivates the lock.

![image](https://user-images.githubusercontent.com/98347572/168566237-cede2f5e-d156-4683-91b6-364c4c3e57b8.png)


Extended SMS message - purpose is to manually send a predefined SMS message to predefined numbers (neighbors, family members etc.) For the SMS sending, I am using paid service, [ClickSend](https://clicksend.com/?u=324136). It can be integrated to a huge amount of systems, including [Home Assistant](https://integrations.clicksend.com/listings/home-assistant) and [Node-RED](https://integrations.clicksend.com/listings/node-red). (Costs €0.11 per SMS).

![image](https://user-images.githubusercontent.com/98347572/168566377-f34f0fd1-ef48-4347-9cb3-b8c050e64e6d.png)
![image](https://user-images.githubusercontent.com/98347572/168566492-642ca0ae-b228-4ac7-be66-ffb346d18407.png)
![image](https://user-images.githubusercontent.com/98347572/168566526-85d42bd0-802b-4178-96fd-b6512378a111.png)


## Example Flow

![image](https://user-images.githubusercontent.com/98347572/168472361-eec3a708-9dc8-4d11-a811-8ca22e4eddc9.png)

Copy and import this json to you Node-RED [node-red-notification-example.json](https://github.com/EvisHome/home-assistant/blob/main/dashboards/nest-protect/node-red-notification-example.json). Eeplace the entities, messages etc. with your own. If you are using ClickSend add your own numbers and API authentications.




