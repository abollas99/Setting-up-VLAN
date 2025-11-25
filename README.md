# Setting-up-VLAN
I recently bought a new router and wanted to experiment with VLANs, which are commonly used in enterprise environments. In this particular lab, I’m setting up a separate VLAN for my printer. I’ve configured rules so that everything can access the printer, but the printer itself can’t access the rest of my devices.

# Hardware:
- TP-Link ER605 v2 [Click here to Buy](https://www.amazon.com/TP-Link-Integrated-Lightening-Protection-TL-R605/dp/B08QTXNWZ1/ref=sr_1_1?crid=3A02IDG8R6M90&dib=eyJ2IjoiMSJ9.lQbaJJwiOF0uETgCFdrPlcSEoTa3Lj8pzTMnvydBE3DfB9-4SA4XMzmhVdR3g0rlGlU_nd2dEu3a7w9r3fHvNE6kVsKsd7KbP0VhF9sCqnxMPTVmzAxd47beLA1QYcWgibDtf1GJjFaNMDCyroN3rTd1TOvIGIi1m2IQEaICEYgRBLSh6A_0JFtMJXb9lZ-BidVlUAO7RT638nEJu0Qeo1uMXW7rqvtgHW0qpbr8YWA.GMUQnNo2jiVLQ26zYsuEALG8BSoSUk6qlbbGlNywhpc&dib_tag=se&keywords=tp%2Blink%2Ber605&qid=1764096478&sprefix=tplink%2Ber605%2Caps%2C94&sr=8-1&th=1), [Official Support Page](https://support.omadanetworks.com/us/product/er605/)
- TP-Link SG608E [Click here to Buy](https://www.homedepot.com/p/TP-LINK-8-Port-Gigabit-Easy-Smart-Switch-TL-SG608E/323833005), [Official Support Page](https://www.tp-link.com/us/support/download/tl-sg608e/)

###### My setup can be improved with an Omada controller and a supported Omada switch. These are the resources I currently have to work with. Once I obtain an Omada controller, I can create another repository describing the process. 

- Configure Router and obtain the Ip of the switch
- configure the switch
- return to the router and set up access control
- ping device to test

# Configure Router

<br>

1. Once the ER605 has been plugged in and you’re on a device with access to its network, navigate to <strong>192.168.0.1</strong>.
2. 
###### Since this is the first time setting it up it will ask you to create a password for the log in. 

<br>

2. Once you are logged in navigate to Network > LAN and you should be greeted to the page below.

<br>

<img width="1097" height="649" alt="Screenshot 2025-11-25 at 2 17 06 PM" src="https://github.com/user-attachments/assets/58f7f745-cb85-40b5-8b7d-449c8ee87c0e" />

###### Your network list will just display VLAN 1

<br>

3. Next select the "Add" button under Network List and it will provide a form for you to fill out.

<br>

<img width="901" height="463" alt="Screenshot 2025-11-25 at 2 21 58 PM" src="https://github.com/user-attachments/assets/39542881-5061-4567-ae6b-ad0bf79abfb1" />

For this lab, I will be using VLAN 20 for the printer.

|Form        | Input         |
|------------|---------------|
|Name        |Printer        |
|IP Address  | 192.168.20.1  | 
|Subnet      |255.255.255.0  |
|Mode        |Normal         |
|VLAN        |20             |
|DHCP Mode   |DHCP Server    |
|Status      |Enable         |
|Starting IP |192.168.20.100 |
|Ending IP   |192.168.20.199 |
|Lease Time  |120            |

The remaining options were left blank.
Once finished you will have another VLAN under Network List.

<img width="849" height="472" alt="Screenshot 2025-11-25 at 2 45 12 PM" src="https://github.com/user-attachments/assets/d3cedb98-d46b-4385-9804-439251d1ebed" />

<br>

4. Next navigate to DHCP list and find the assigned IP to your network swtich. In this case it is <strong>192.168.0.101<strong>.

<br>

<img width="819" height="364" alt="Screenshot 2025-11-25 at 2 53 16 PM" src="https://github.com/user-attachments/assets/49d19dc1-04a2-4118-b334-3eead362c7a5" />
