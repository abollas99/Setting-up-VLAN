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
   
###### Since this is the first time setting it up it will ask you to create a password for the log in. 

<hr>
<br>

2. Once you are logged in navigate to Network > LAN and you should be greeted to the page below.

<br>

<img width="1097" height="649" alt="Screenshot 2025-11-25 at 2 17 06 PM" src="https://github.com/user-attachments/assets/58f7f745-cb85-40b5-8b7d-449c8ee87c0e" />

###### Your network list will just display VLAN 1

<hr>
<br>

3. Next select the "Add" button under Network List and it will provide a form for you to fill out.

<br>

<img width="901" height="463" alt="Screenshot 2025-11-25 at 2 21 58 PM" src="https://github.com/user-attachments/assets/39542881-5061-4567-ae6b-ad0bf79abfb1" />

For this lab, I will be using VLAN 20 for the printer.

|Form        | Input         |
|------------|---------------|
|Name        |Printer        |
|IP Address  |192.168.20.1  | 
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

<hr>
<br>

4. Next navigate to DHCP list and find the assigned IP to your network swtich. In this case it is <strong>192.168.0.101<strong>.

<br>

<img width="819" height="364" alt="Screenshot 2025-11-25 at 2 53 16 PM" src="https://github.com/user-attachments/assets/49d19dc1-04a2-4118-b334-3eead362c7a5" />

# Configure Switch

1. Navigate to the ip of your switch. Once you have logged in the screen should appear like the image below.

<img width="1108" height="475" alt="Screenshot 2025-11-25 at 3 24 20 PM" src="https://github.com/user-attachments/assets/677d55b5-9f0a-4e7e-ae66-9ff76b1878ab" />

2. Navigate to the VLAN > 802.1Q VLAN section. Since this is not an Omada switch and I don’t have an Omada controller, we need to add the VLAN here as well.

<img width="759" height="403" alt="Screenshot 2025-11-25 at 3 27 42 PM" src="https://github.com/user-attachments/assets/92caea8b-18ae-49d5-b762-bd07aa63da16" />
  
- Before adding the VLAN you want to enable "802.1Q VLAN configuration" at the top and hit apply. Once that is complete we will add a VLAN by filling "VLAN ID" as 20 and "VLAN Name" as Printer. Now, you’ll need to identify which ports on your switch are connected to your router and printer. For me the router is on Port 8 and the printer is on Port 2. For your router port you want to select tagged and for your printer port you want to select untagged. The remaining ports will be left under "Not Member". Once you have adjusted the correct ports hit "Add/Modify". Below is what it looks like for me.

<img width="671" height="81" alt="Screenshot 2025-11-25 at 3 31 58 PM" src="https://github.com/user-attachments/assets/321c9080-9a63-4b7c-9f93-0ac9d8a7fa55" />

3. Now you want to navigate to "802.1Q PVID Setting" in the VLAN menu. 

- You are going to select the port for your printer and change the "PVID" to your VLAN. For me it was port 2 and set the "PVID" to 20. After you hit apply your VLAN 20 will be created.

<img width="721" height="422" alt="Screenshot 2025-11-25 at 3 36 08 PM" src="https://github.com/user-attachments/assets/1031d4e4-5b2a-4aa2-ae03-2446ff68c388" />

4. To test if you were successful navigate back to your router which will be at 192.168.0.1. Once there go to Network > LAN then in the tabs above select DHCP Client List. Now manually unplug your printer port and plug it back in. This should reset the lease time. When you hit refresh you should see an ip address that will be somewhat like 192.168.20.100. If you do not see this go back and recheck all the settings. Make sure you hit apply to all the changes you made.

# Configuring VLAN Rules

1. For us to configure the VLAN rules we have to go into the firewall settings of the router. In the router we are using navigate to FIrewall > Access Control. Once there you will see an empty list. Click add for us to add our first rule.

|Form|Input|
|----|-----|
|Name|Block_Printer_Outbound|
|Policy|Block|
|Service Type|ALL|
|IP Type|IPv4|
|Direction|LAN->LAN|
|Source Network|Printer|
|Destination Network|LAN|
|Effective Time|Any|
|States|Leave as Default|
|ID|*Leave Empty*|
