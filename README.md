# Service-Request

This is the procedure which is used when the device wants to establish a connection to the AMF. There are two possible scenarios in which this can happen

i) this can be used when the device does not have a connection to the AMF and hence uses this procedure to establish a new connection. In this case, the device goes from idle mode to connected mode. 

ii) when the PDU session already exists but the user connection has to be activated for that PDU session (activate the user-plane connections). 

There are two types of service request procedure such as
i) Network Triggered 
ii) UE Triggered 

If there is downlink data that needs to reach the device, then it can be network triggered because the network takes the initiative based on the information that there is downlink data will be sent to the device. Now, if there is the uplink data that needs to be sent from the device, then the device can trigger the UE service request procedure.


**UE Triggered Service Request**

UE triggered service request is initiated whenever there is uplink data to be sent. In the first step, the device sends the services request message to the RAN and the RAN forward it to the AMF. We have previously discussed the two scenarios. Suppose a device is in idle mode and wants to go to the connected mode then the service request procedure is straightforward.

Alternatively, if there is already a PDU session and only a user-plane connection needs to be established. In that case, the service request message will have the information about that, this is the PDU session ID, for this PDU session create the user-plane connection. In the second step, there can be an optional authentication that can be performed to make sure that the device has the credentials to do the service request.

In Step 3, the AMF notifies the SMF that there is a need to activate the user-plane connection. If there is already an existing user-plane tunnelling endpoint, then the SMF will directly reply that this is the UPF endpoint that can be used. 

On the other hand, if the device has moved and now there is a need to move the connection to a new UPF. Then the SMF does more steps to make sure that the connection is migrated from the previous UPF to the new UPF. Now the AMF have received the session related information from the SMF, it forwards this back to the RAN including the information about the UPF endpoint. Using this, the RAN established the tunnel back to the UPF because it knows the other endpoint i.e UPF-endpoint. 

So based on this information, now the tunnel is established and hence the device is ready to send the uplink data. One thing to remember here is that it is the RAN that knows the UPF tunnel endpoint, not vice versa. 

In Step 5, the AMF will notify the SMF about the RAN tunnel endpoint and SMF uses this to update the UPF, about the RAN tunnel endpoint identifier. Meanwhile, the PCF might be interested to know if there is a change in the UE location. So the SMF update the PCF whatever the current location of the UE. Now the UPF knows where to find the RAN endpoint. It can make the connection and the downlink data can also be sent.


**Network Triggered Service Request**

It is used when there is downlink data to be sent to the device. In step 1, there is downlink data at the UPF but the UPF does not know where to send the data because there is no connection to the device. Then the UPF buffers the data and notifies the SMF that there is data for the device to be received. 

In step 2, the SMF contacts the AMF that there is data corresponding to this PDU session from this kind of data network that needs to be reached to the device. 

In step 3, the AMF notifies by saying that go and find this device. Because in this case, we have two possible options. Either we don't know where the device is or we know the device if it is in connected mode. 

First, let us assume that the device is in idle mode, then the network does not exactly know where it is. So the network has to do paging. The RAN does the page and when the device received the paging message, it sends the service request back to the network. This is the service request triggered, which is the same as the UE trigger service request. So the network trigger procedure is the network paging and asking the device to start by UE triggered procedure.

Now in another scenario, the device is in connected mode. So the network knows where to contact the device. In this case, the RAN tunnel endpoint identifier needs to be conveyed back to the UPF. Similar to steps 3 to 4 in the UE service request procedure, the RAN tunnel end-point identifier is followed by the AMF to SMF and SMF configured the UPF with the correct information about, what is the RAN tunnel endpoint. Once the information is available then the downlink data can be sent from the UPF to the RAN. 
