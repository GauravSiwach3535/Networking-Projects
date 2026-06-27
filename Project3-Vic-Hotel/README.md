# 🏨 Project 3 – Vic Modern Hotel Network

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Tool](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-blue)
![Level](https://img.shields.io/badge/Level-Advanced-red)

## 📌 Overview

Designed and implemented a full **3-floor hotel network** for **Vic Modern Hotel**. The network covers 8 departments across 3 floors with complete VLAN segmentation, OSPF dynamic routing, DHCP, wireless access, SSH remote management, and port security.

---

## 🎯 Objectives

- ✅ Design a multi-floor network with 3 routers (all in server room)
- ✅ Connect routers via Serial DCE cables
- ✅ Assign VLANs to each department with dedicated networks
- ✅ Provide WIFI access per floor
- ✅ Configure OSPF as the routing protocol
- ✅ Set up router-based DHCP for all devices
- ✅ Configure SSH on all routers for remote login
- ✅ Implement port security on IT switch (sticky MAC, shutdown mode)

---

## 🏢 Floor & Department Layout

### 🟦 Floor 1
| Department | VLAN | Network | Gateway |
|-----------|------|---------|---------|
| Reception | VLAN 80 | `192.168.8.0/24` | `192.168.8.1` |
| Store | VLAN 70 | `192.168.7.0/24` | `192.168.7.1` |
| Logistics | VLAN 60 | `192.168.6.0/24` | `192.168.6.1` |

### 🟩 Floor 2
| Department | VLAN | Network | Gateway |
|-----------|------|---------|---------|
| Finance | VLAN 50 | `192.168.5.0/24` | `192.168.5.1` |
| HR | VLAN 40 | `192.168.4.0/24` | `192.168.4.1` |
| Sales/Marketing | VLAN 30 | `192.168.3.0/24` | `192.168.3.1` |

### 🟥 Floor 3 (Server Room)
| Department | VLAN | Network | Gateway |
|-----------|------|---------|---------|
| Admin | VLAN 20 | `192.168.2.0/24` | `192.168.2.1` |
| IT | VLAN 10 | `192.168.1.0/24` | `192.168.1.1` |

---

## 🌐 Router Interconnection (WAN Links)

| Link | Network | Router A | Router B |
|------|---------|---------|---------|
| Floor 1 ↔ Floor 2 | `10.10.10.0/30` | `10.10.10.1` | `10.10.10.2` |
| Floor 2 ↔ Floor 3 | `10.10.10.4/30` | `10.10.10.5` | `10.10.10.6` |
| Floor 1 ↔ Floor 3 | `10.10.10.8/30` | `10.10.10.9` | `10.10.10.10` |

> All routers are connected via **Serial DCE cables** and placed in the **IT Department server room (Floor 3)**

---

## 🏗️ Topology

> 📸 *See `screenshots/topology.png` for the full network diagram*

```
        [Floor 3 Router] ←—Serial DCE—→ [Floor 2 Router]
               ↑                               ↑
          Serial DCE                      Serial DCE
               ↓                               ↓
        [Floor 1 Router] ←—Serial DCE—→ [Floor 2 Router]

Each Router → Switch (per floor) → VLANs → Departments + WiFi + Printers
```

---

## ⚙️ Key Configurations

### OSPF Routing
```
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
Router(config-router)# network 10.10.10.0 0.0.0.3 area 0
```

### SSH Configuration (All Routers)
```
Router(config)# ip domain-name hotel.local
Router(config)# crypto key generate rsa
Router(config)# username admin privilege 15 secret cisco123
Router(config)# line vty 0 4
Router(config-line)# login local
Router(config-line)# transport input ssh
```

### Port Security (IT Switch – fa0/1)
```
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 1
Switch(config-if)# switchport port-security mac-address sticky
Switch(config-if)# switchport port-security violation shutdown
```

### DHCP Pool Example (Floor 1 Router)
```
Router(config)# ip dhcp pool RECEPTION
Router(dhcp-config)# network 192.168.8.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.8.1
Router(dhcp-config)# dns-server 8.8.8.8
```

---

## 📸 Screenshots

| Screenshot | Description |
|-----------|-------------|
| `screenshots/topology.png` | Full 3-floor network topology |
| `screenshots/vlan_config.png` | VLAN assignments per floor |
| `screenshots/ospf_routes.png` | `show ip route` – OSPF routes |
| `screenshots/ssh_test.png` | SSH remote login from Test-PC |
| `screenshots/port_security.png` | Port security sticky MAC config |
| `screenshots/dhcp_working.png` | Devices receiving auto IP |
| `screenshots/ping_test.png` | Cross-floor ping verification |

---

## 🔧 Key Concepts Used

- **VLANs** – 8 VLANs across 3 floors
- **OSPF** – Dynamic routing protocol between floor routers
- **Serial DCE** – WAN links between routers using `/30` subnets
- **DHCP** – Router-based automatic IP allocation per department
- **SSH** – Secure remote management on all routers
- **Port Security** – Sticky MAC with shutdown violation on IT port
- **Wireless** – Access points per floor for laptops/phones
- **Printers** – One per department

---

## 📂 Files Included

```
Project3/
├── Project3.pkt          ← Cisco Packet Tracer file
├── README.md             ← This file
└── screenshots/
    ├── topology.png
    ├── vlan_config.png
    ├── ospf_routes.png
    ├── ssh_test.png
    ├── port_security.png
    ├── dhcp_working.png
    └── ping_test.png
```

---

> 🔙 [Back to Main Portfolio](../README.md)
