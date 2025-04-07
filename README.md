# 🏢 Small Office Network - Cisco Packet Tracer Lab

## 📘 Scenario
A small accounting firm has 8 employees and requires a simple network with both wired and wireless access. The network includes shared access to a file server and a printer. This lab implements the setup using **Cisco Packet Tracer** with **only built-in device models**.

---

## 📦 Devices Used

| Device         | Model              | Quantity | Purpose                    |
|----------------|--------------------|----------|----------------------------|
| Router         | Cisco 2911         | 1        | DHCP, Gateway              |
| Switch         | Cisco 2960         | 1        | Wired Connectivity         |
| Access Point   | AccessPoint-PT-N   | 1        | Wireless Bridge            |
| PCs            | PC                 | 6        | Wired Users (DHCP)         |
| Laptops        | Laptop             | 2        | Wireless Users (DHCP)      |
| File Server    | Server             | 1        | Shared Resource (Static)   |
| Printer        | Printer            | 1        | Shared Printing (Static)   |

---

## 🌐 IP Addressing Scheme

| Device         | IP Address       | Notes                        |
|----------------|------------------|------------------------------|
| Router         | 192.168.10.1     | Default Gateway              |
| DHCP Range     | 192.168.10.1–254 | Full range (minus static IPs manually configured) |
| File Server    | 192.168.10.100   | Static IP                    |
| Printer        | 192.168.10.150   | Static IP                    |
| Access Point   | *N/A*            | Uses switch port (no IP)     |

- **Subnet Mask:** `255.255.255.0`
- **DNS Server:** `8.8.8.8`

---

## 📡 Wireless Configuration

- **SSID:** `default`  
- **Security:** WPA2-PSK  
- **Passphrase:** `password123`  
- **Connected Devices:** 2 Laptops  

**Note:** The `AccessPoint-PT-N` does not have an IP address and simply bridges wireless devices to the switch port.

---

## ⚙️ Router Configuration (Cisco 2911)

```plaintext
Router> enable
Router# configure terminal

! Set interface IP
Router(config)# interface g0/0
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! Configure DHCP
Router(config)# ip dhcp pool OFFICE
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit

Router(config)# end
Router# write memory

## 🎥 Video Tutorial

[![How to Upload a Project to GitHub](https://img.youtube.com/vi/ClkMbWItdoY/0.jpg)](https://www.youtube.com/watch?v=ClkMbWItdoY)
