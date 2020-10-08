# Balboa Spa HomeKit

GO HERE: https://github.com/vincedarley/homebridge-plugin-bwaspa as this work is more complete and took it to the next level!

 Using MQTT, Homebridge & Node-Red to expose Balboa Spa controller in Homekit
 
 Let's be honest here...I have a day job...this is me hacking over weekends and nights to figure this out. I used a logic analyzer to snoop on the bus (it is serial BTW) and then found some people online who had hacked this before. I thank them and will collect up licks to their work and to all the things below when I have a tad more time.
 
# Recent Changes
* added a lockout feature where you can lock the setting to keep anyone from messing with them
* addded some more error handling
* added data collection for a influxdb data collection (trying to get the rate of heat loss and time to ready so I know...)
 
# Requirements
* Spa controller on your network
* Node-Red - https://nodered.org
* The nodes listed in this flow - Node-Red will tell you which ones you are missing
* MQTT Server (I use mosquitto docker image) - https://hub.docker.com/_/eclipse-mosquitto
* the paths follow a pattern of /hottub/circpump and I guess I should pull a list of all of them, but when you look at the flow you should see them all. Basically one for each control.
* homebridge with the MQTT things plugin
* if you dont care about the data logging remove the parts of the flow touching influxdb

Example of one of the Homebridge accessories (you will need one of these for each item you want to put in homekit)
```
		{
            "accessory": "mqttthing",
            "type": "switch",
            "name": "Hot Tub Lights",
            "url": "http://MQTT SERVER:1883",
            "topics": {
                "getOn": "/hottub/lights",
                "setOn": "/hottub/lights/set"
            },
            "onValue": "3",
            "offValue": "0"
        }
```

# Helpful Screenshots

![Flow](https://github.com/ntableman/Balboa-Spa-HomeKit/blob/master/Node-Red%20Flow.png)

![Homekit](https://github.com/ntableman/Balboa-Spa-HomeKit/blob/master/Home%20Kit.png)
