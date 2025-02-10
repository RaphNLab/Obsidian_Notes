# Terminologi definition
- Charging Station: device providing power to electric vehicules (EV)
- Electric Vehicule Supply Equipment (EVSE): Component of the station that supply electricity to one connector at the time. Each EVSE can only charge one RV at the time. An EVSE can switch between connectors depending on the type of connector the EV driver selected trough the mobile app of RFID-Chip.
![[2_EVSE_3Connector.png]]
# Connector types
+ Type 2 connector: For DC charging
+ CCS connector: For DC charging

# ID representation
+ Each charging station has a unique identifier that can be chosen by every provider.
+ Each EVSE has a unique ID starting from 1 to N
+ Every connector has a unique ID starting from 1 to N
# Communication between Station and CSMS
A web-socket is used to as communication medium to allow stations and CSMS to communicate. Only the station can initiate a new connection by sending a request to the CSMS containing the link of the web-socket with his unique ID at the end of the link. This way the CSMS knows to wich station it is about to establish the communication.

A boot request is send to announce that the station is booting. This is only possible if the CSMS allows the first request. 

Messages are format is JSON. The OCPP describes way  and the content that every messages shall follow (It is the communication protocol). 
A typical boot message looks as follows:

![[BootNotification.png]]
The format is the following:
**[       MessageType, "unique ID", "Action"
	{
		Payload
	}
]**
Message type can be:
* 2 CALL (Request message)
* 3 CALLRESULT (Response message)
* 4 CALLERROR (Response error)

The action field is the telegram type (**==BootNotification, Reset, StatusNotification, etc...==**)

## Heartbeats
Heartbeats are use to notify the SCMS that ever thing is still working. The value of the heartbeat frequency is select by the CSMS. It is also used to synchronize the time between CSMS and Station. 
If messages are exchanged between station and CSMS during the heartbeat interval, the CSMS consider that everything is doing well. This way not only the heartbeat message is used to achieve the notification purpose.

## Station reset
The CSMS can request the station to reset if it's not working properly.
There are two different type of reset:
+ Immediately: the station reset without thinking of anything (Used in emergency situation)
+ On Idle: the station waits until a charging transaction is done before resetting (Used wenn the station is not  being used).

Once reset occurs, the station open a new web-socket connection to the server and send a new boot notification to inform the CSMS that it is back online.

![[Reset_request.png]]

## Status messages
This messages are sent to notify the CSMS which status each station do have.
There are four relevant status:
+ **Occupy**
+ **Available**
+ **Unavailable** (If tho or more connectors are on a single EVSE)
+ **Faulted**
The CSMS shall send a response to acknowledge the notification reception. If no message is received, the CSMS assume that the message was not received and send the notification again (Amount of retries ???). 
For maintenance purpose, the CSMS can command a station to change his status from **"available"** to **"Unavailable"**.

## Alert and monitoring

Alert events are sent the CSMS if the station notice an abnormal behavior
Alerts are sent using a **NotifyEvent** message. This message contains:
* generatedAt: The timestamp
* seqNo: The sequence number. If the CSMS receives a message with a lowes seqNo that the previous one, it assumes that some messages were lost and take some measures to solve the issue like requesting to resend the message
* eventData: Details of the actual alert

