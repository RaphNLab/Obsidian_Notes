

🚗 :luc_battery_charging: 

A transaction represents the procedure during wich energy transfer starts and stops. This  Meanwhile information are exchanged between the charging station and the CSMS which are very important for billing purpose:
+ Transaction ID
+ Tart time of a transaction
+ End time of a transaction
+ Power amount transfered

Many scenarios shall be implemented:
* **Parking bay occupancy:** Here transaction starts when a parking bay occupancy sensor detects an EV  
```
TxStartPoint: ParkingBayOccupancy
```

![[Transaction_ParkingBay.png]]


* **Charging cable plugged:** In this scenario the transaction starts when a connection between the charging station and the EV is established by plugging the charging cable from the charging station to the EV.
```
TxStartPoint: EVConnected
```

 
![[Transaction_CablePlugged.png]]

* **Authorization:** The transaction starts when the driver is authorized to charge by providing his identification.
```
TxStartPoint: Authorized
```

 ![[Transaction_Authorized.png]]

* **When the first meter value is provided:** The transaction starts only when the first meter values are received from the charging station. The EV driver plugs in the cable at the charging station and the EV, The charging station request the meter for a signed value.

```
TxStartPoint: DataSigned
and 
SampledDataSignReadings set to true
```

 ![[Transaction_MeterValue.png]]


* **All preconditions have been met:** In this case the transaction only starts when the EV-Driver was authorized and the connection was established but no energy transfer took place. 
```
TxStartPoint: PowerPathClosed 
```

 ![[Transaction_AllPrerequisites.png]]

* **Energy flow:** Here the transaction starts when the energy flow starts, this means first that all prerequisites are met (Authorized, EV Connected)
```
TxStartPoint: EnergyTransfer
```

  ![[Transaction_EnergyTransfer.png]]


