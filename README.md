Here is the full README.md with the complete configuration setup for your small office network:


# Small Office Network Design and Implementation

## Overview
This document outlines the configuration and setup of a small office network for an accounting firm. The network includes wired and wireless connectivity for 8 devices (6 PCs, 2 laptops), a file server, and a printer. The network ensures that all devices can communicate effectively, share resources, and access the internet.

## Objective
To set up a network with the following requirements:
- Wired and wireless connectivity for 8 devices (6 PCs, 2 laptops).
- A file server for shared resources.
- A printer accessible by all employees.
- A router providing DHCP and network connectivity.
- The network will be configured using **IP range 10.100.10.0/24** with specific IP assignments.

## Network Topology

		 [Router 2911]
                
                      |
                [Switch 2960] -- Server | Printer
          /      |      |     \     \
      VLAN10  VLAN10 VLAN10  VLAN20 VLAN20
       PCs     Server Printer   ↳ Access Point
                              ↳ Wireless Laptops

Step-by-Step Setup


1. Router Configuration
The router will provide DHCP and routing for the network. The following steps configure the router to allocate IP addresses dynamically and set up routing.

CLI Commands:



Router> enable
Router# configure terminal

! Configure the router's interface with IP 10.100.10.1/24
Router(config)# interface gigabitethernet0/0
Router(config-if)# ip address 10.100.10.1 255.255.255.0
Router(config-if)# no shutdown

! Configure DHCP on the router
Router(config)# ip dhcp pool OfficeNetwork
Router(dhcp-config)# network 10.100.10.0 255.255.255.0
Router(dhcp-config)# default-router 10.100.10.1
Router(dhcp-config)# dns-server 8.8.8.8


2. Switch Configuration
Switch> enable
Switch# configure terminal
Switch(config)# hostname OfficeSwitch
OfficeSwitch(config)# interface range fa0/1 - 8
OfficeSwitch(config-if-range)# switchport mode access
OfficeSwitch(config-if-range)# description Connected_to_Employee_PCs
OfficeSwitch(config-if-range)# exit

OfficeSwitch(config)# interface fa0/9
OfficeSwitch(config-if)# switchport mode access
OfficeSwitch(config-if)# description Connected_to_Network_Printer
OfficeSwitch(config-if)# exit

OfficeSwitch(config)# interface fa0/10
OfficeSwitch(config-if)# switchport mode access
OfficeSwitch(config-if)# description Connected_to_File_Server

# Assign switch ports to VLAN 10 (default)
Switch(config)# interface range fa0/1 - 10
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 1
Switch(config-if-range)# exit

# Configure the trunk port for future expansion if needed
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit

3. Wireless Access Point (AP) Configuration

Connect the AP to the Switch

Use a copper straight-through cable.

Connect AP-PT-N Port 1 to Switch0 (e.g., FastEthernet 0/11).

Configure the AP

Click on AP-PT-N.

Go to the Config tab.

Under Interface -> Port 1:

Check that "Port Status" is set to On (this should be the default).

Set to DHCP (leave default to receive IP from router).

You do not need to manually assign an IP here.

Under Wireless -> Settings:

SSID: DefaultSSID

Authentication Mode: WPA2-PSK

Passphrase: password123

Under Wireless -> Port 0 (for reference only):

No changes are needed; this is used by wireless clients to connect.

4. File Server Configuration
Click on the File Server to open its configuration window.

Go to the Config tab.

Set Static IP Address: Assign a static IP address to the File Server. For example, 10.100.10.100.

IP Address: 10.100.10.100

Subnet Mask: 255.255.255.0 (same as the router's subnet).

Default Gateway: 10.100.10.1 (router's IP).

 5. Printer Configuration:
Click on the Printer device to open its configuration window.

Go to the Config tab.

Set Static IP Address: Assign a static IP address to the printer. For example, 10.100.10.150.

IP Address: 10.100.10.150

Subnet Mask: 255.255.255.0 (same as the router's subnet).

Default Gateway: 10.100.10.1 (router's IP).

6. PC and Laptop Configuration
All devices (PCs and laptops) will receive dynamic IP addresses from the router’s DHCP server. Once connected to the network, they will automatically be assigned IP addresses within the range 10.100.10.2 to 10.100.10.9.

Ensure that each device's network adapter is set to Obtain an IP address automatically (DHCP).

7. Testing Connectivity
Ping the File Server:

laptop0> ping 10.100.10.100   # Ping File Server from laptop0

Ping the Printer:
laptop0> ping 10.100.10.150   # Ping Printer from laptop0
These tests will ensure that all devices are connected properly and can communicate with the file server, printer, and router.

8. Documenting Configuration
After completing the setup, document all the key configuration parameters:

Router IP: 10.100.10.1

File Server IP: 10.100.10.100

Printer IP: 10.100.10.150

PCs IP Range: 10.100.10.2 to 10.100.10.7

Laptops IP Range: 10.100.10.8 to 10.100.10.9

SSID for AP: default

Wireless Password: password123

Conclusion
This setup ensures that all devices in the office are connected properly, have access to shared resources like the file server and printer, and can connect securely via wireless or wired connections.

Additional Notes
Security Considerations: For better security, it is advised to change the default SSID name and password after setup.

Future Upgrades: Consider adding more APs if the office space expands or if you have issues with wireless coverage in certain areas.

Troubleshooting Tips
Issue: Devices can't connect to the network.

Solution: Check the DHCP configuration on the router and ensure that the IP address range is correct.

Issue: The printer isn't accessible.

Solution: Ensure that the printer's static IP is correctly set and verify that there are no IP conflicts.

License
This document is released under the MIT License.

markdown



---

### Explanation:
- **Overview**: Describes the goal of setting up a small office network and key components.
- **Network Topology**: A simple diagram shows how devices are connected in the network.
- **Step-by-step setup**: Detailed instructions and CLI commands are provided for configuring the router, switch, AP, file server, printer, and PCs/laptops.
- **Testing**: Instructions to test the network's functionality and verify connectivity.
- **Configuration Documentation**: Lists key IP addresses for easy reference.

This **README.md** provides a comprehensive guide for configuring the network, including all CLI commands, setup instructions, and troubleshooting tips. It is structured for both technical users who will follow the setup and non-technical users who may need an overview.






