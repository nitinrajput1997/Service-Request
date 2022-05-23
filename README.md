# Service-Request

This is the procedure which is used when the device wants to establish a connection to the AMF. There are two possible scenarios in which this can happen

i) this can be used when the device does not have a connection to the AMF and hence uses this procedure to establish a new connection. In this case, the device goes from idle mode to connected mode. 

ii) when the PDU session already exists but the user connection has to be activated for that PDU session (activate the user-plane connections). 

There are two types of service request procedure such as
i) Network Triggered 
ii) UE Triggered 

If there is downlink data that needs to reach the device, then it can be network triggered because the network takes the initiative based on the information that there is downlink data will be sent to the device. Now, if there is the uplink data that needs to be sent from the device, then the device can trigger the UE service request procedure.
