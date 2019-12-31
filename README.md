# <img src='https://raw.githack.com/FortAwesome/Font-Awesome/master/svgs/solid/broadcast-tower.svg' card_color='#40DBB0' width='50' height='50' style='vertical-align:bottom'/> Mesh
send MQTT messages and commands between multiple mycroft.ai devices.

## About
A flock of Seagulls, a pride of Lions, a swarm of Bees, and a "mesh of Mycrofts".

This skill utilizes the lightweight MQTT messaging protocol to connect a group ("mesh") of Mycroft units together. The skill has the ability to send messages (intercom) and commands (messagebus) to one or more remote Mycroft units.
1. Each Mycroft unit has the ability to publish both Mycroft requests and responses to the the MQTT broker.
The MQTT Topics for this communication is...
- ```Mycroft/deviceUUID/request```
- ```Mycroft/deviceUUID/response```
2. The deviceUUID is a unique ID created from the MAC of the sending Mycroft unit.
*This is intended to be a general MQTT broadcast and can be subscribed to by any MQTT client (ie. Home Assistant?).
3. Each Mycroft unit has it's own Device Name (location_id) that can be set in the web interface.
4. The Mycroft unit will automatically subscribe to all messages sent to it's own Device Name (location_id).
- ```Mycroft/RemoteDevices/location_id```
5. When a message is sent from any Mycroft unit, the message will be published to "Mycroft/RemoteDevices/location_id".
6. The destination location_id is specified in the skill dialog.
7. The message payload will contain the following...
-```[{"source":"<source_location_id>"},{"message":"is dinner ready yet"}]


## Examples
* "Send a remote message"
* "Send a remote command"

## Credits
pcwii

## Category
**IoT**

## Tags
#mesh
#remote
#connect
#control


## Conversational Context
- Example 1 (from basement to kitchen)
```
hey mycroft...
    send a remote message...
where would you like to send the message?...
    kitchen...
what would you like the message to be?...
    Is dinner ready yet?
Sending message, is dinner ready yet to the kitchen.
mycroft publishes...
"Mycroft/RemoteDevices/Kitchen/[{"source":"basement"},{"message":"is dinner ready yet"}]
```
- Example 2 (from kitchen to basement)
```
hey mycroft...
    send a remote command...
where would you like to send the command?...
    basement...
what would you like the command to be?...
    set a timer for 5 minutes?
Sending command, set a timer for 5 minutes to the basement.
mycroft publishes...
"Mycroft/RemoteDevices/Basement/[{"source":"basement"},{"command":"set a timer for 5 minutes"}]
```