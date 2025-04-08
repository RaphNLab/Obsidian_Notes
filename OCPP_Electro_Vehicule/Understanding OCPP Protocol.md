
# Terminology definition

- CSMS: 
- OCPP: 
- Charging Station: device providing power to electric vehicle (EV)
- Electric Vehicle Supply Equipment (EVSE): Component of the station that supply electricity to one connector at the time. Each EVSE can only charge one RV at the time. An EVSE can switch between connectors depending on the type of connector the EV driver selected trough the mobile app of RFID-Chip.
![[2_EVSE_3Connector.png]]
# Connector types
+ Type 2 connector: For DC charging
+ CCS connector: For DC charging

# ID representation
+ Each charging station has a unique identifier that can be chosen by every provider.
+ Each EVSE has a unique ID starting from 1 to N
+ Every connector has a unique ID starting from 1 to N
# Communication between Station and CSMS
A web-socket is used to as communication medium to allow stations and CSMS (Charging Station Management System) to communicate. Only the station can initiate a new connection by sending a request to the CSMS containing the link of the web-socket with his unique ID at the end of the link. This way the CSMS knows to which station it is about to establish the communication.

A boot request is send to announce that the station is booting. This is only possible if the CSMS allows the first request. 

Messages are format is JSON. The OCPP(Open Charge Point Protocol) describes way  and the content that every messages shall follow (It is the communication protocol). 
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
* seqNo: The sequence number. If the CSMS receives a message with a lowest seqNo that the previous one, it assumes that some messages were lost and take some measures to solve the issue like requesting to resend the message
* eventData: Details of the actual alert


# Authorization of new charges
To be able to charge a EV, the EV-Driver has to be authorized. Most charging station a only available to person who has a contract with the charging station provider.
There are several ways to get authorization:
+ RFID
+ Mobile apps
+ Push button
+ Credit cards terminals
## Charging process using RFID
The **idToken** is used to identify the user/vehicle requesting for authentication. It's a code assign to the user/vehicle by the CSMS.
How does it work:
1. The user places its RFID-Tag on the stastion transponder 
2. The station sends a authorize-message to the central system containing the idToken
3. The CSMS responds (Accepted | Rejected | a different status)
4. The station indicates the result to the driver (Display or LED)

![[RFID_Authorization.png]]

A **Transaction** describes a charging event. Configuring the transaction start and stop logic is important for billing purposes. 

### Charging flow
After authorization, the charging session can start.
1. The driver connects a cable to the station 
2. The station sends a **TransactionEvent** to the CSMS (eventType=Started, triggerReason=Authorization, idToken= 123456) 
3. The CSMS confirms that is has received the message
4. The Station starts to provide energy to the EV


## Charging process using Mobile App
Users can use a mobile App to request charging authorization. The mechanism used between the mobile app and the CSMS is out of the scope of OCPP.
To start a transaction the user muss:
1. Open the mobile app and select the charging station (EVSE, Connector) he wants to use
2. The CSMS sends a **RequestStartTransction** message to the station
3. The Station verify and responds back to the CSMS (Accepted, rejected, unknow)
4. The driver connects the cable to the EV
5. The station sends an **TransactionEventRequest**  (Type=started) message the the CSMS
6. The CSMS responds (No particular information in the telegram)

![[Mobile_App_Authorization.png]]

# Obtaining charging data (Energy, Batery status)

Metering messages are send periodically to indicate specific values from the station to the CSMS.
A station can still send metering messages to the CSMS even though a transaction has not started. Typically information about the stations data like its temperature.

The **meterValue** message is used when the transaction has not started yet.
The  **TransactionEvent** contains transaction values related to the power consumption.

![[Transaction_Event.png]]

# Stopping a charging transaction
The are several ways to stop a transaction:
+ RFID tags
+ Mobile App
+ Disconnect the cable
+ Physical buttons
A **TransationEvent** message  containing the counter value of the power consumption is sent when the transaction ends.
To calculate the final energy consumption, the counter start value is subtracted from the counter end value. The result is used to create the invoice for the costumer.

The user may use a remote app to stop the transaction.
1. The user press the stop button
2. The CSMS sends a **RequestStopTransaction** to the station (Containing the transaction Id that need to be stop)
3. The station send a **RequestStopTransactionResponse** message (Accepted, Rejected)
4. The station send **TransactionEventRequest** (eventType=Ended, triggerReason=RemoteStop, stopReason=Remote)
5. The CSMS send back a response

# Advance topics:
1. ISO 15118 Plug and charge can be used to start and stop transaction when the connector is plugged in or aout.
2. Firmware mamangement
3. Displaying messages


