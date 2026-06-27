# 🏢 Project 2 – XYZ Company Branch Network

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Tool](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-blue)
![Level](https://img.shields.io/badge/Level-Intermediate-orange)

## 📌 Overview

Designed and implemented a **branch office network** for XYZ Company — a fast-growing company in Eastern Australia with over 2 million global customers. The branch is located near the local village **Bonalbo** and operates independently from the company's headquarters.

The network features **3 VLANs**, **wireless access**, **DHCP**, and **inter-VLAN routing** using a single router and switch setup.

---

## 🎯 Objectives

- ✅ Design a small branch network using 1 router and 1 switch (Cisco)
- ✅ Create 3 separate VLANs for each department
- ✅ Provide wireless connectivity for all departments
- ✅ Configure automatic IP addressing via DHCP
- ✅ Enable communication between all departments (Inter-VLAN Routing)

---

## 🏢 Departments & VLANs

| Department | VLAN ID | Network ID | Usable Range | Broadcast |
|-----------|---------|-----------|-------------|-----------|
| Admin / IT | VLAN 10 | `192.168.1.0` | `192.168.1.1` – `192.168.1.62` | `192.168.1.63` |
| Finance / HR | VLAN 20 | `192.168.1.64` | `192.168.1.65` – `192.168.1.126` | `192.168.1.127` |
| Customer Service / Reception | VLAN 30 | `192.168.1.128` | `192.168.1.129` – `192.168.1.190` | `192.168.1.191` |

---

## 🌐 Network Design & Subnetting

### Subnetting Calculation

| Parameter | Value |
|-----------|-------|
| Base Network | `192.168.1.0` |
| Number of Subnets | 3 (Three Departments) |
| Borrowed Bits (n) | 2 |
| Subnet Mask | `255.255.255.192` (/26) |
| Block Size | 64 |

---

## 🏗️ Topology

> 📸 *See `screenshots/topology.png` for the full network diagram*

```
                        [Router]
                           |
                     (Trunk Link)
                           |
                        [Switch]
                  /        |         \
           VLAN 10      VLAN 20     VLAN 30
          (Admin/IT)  (Finance/HR)  (Customer)
              |            |            |
           [AP + PCs]  [AP + PCs]  [AP + PCs]
```

---

## ⚙️ Key Configurations

### Router-on-a-Stick (Inter-VLAN Routing)
The router uses **subinterfaces** on a single physical port to route traffic between VLANs:

```
Router(config)# interface fa0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.1.1 255.255.255.192

Router(config)# interface fa0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.1.65 255.255.255.192

Router(config)# interface fa0/0.30
Router(config-subif)# encapsulation dot1Q 30
Router(config-subif)# ip address 192.168.1.129 255.255.255.192
```

### DHCP Pools on Router
```
Router(config)# ip dhcp pool ADMIN
Router(dhcp-config)# network 192.168.1.0 255.255.255.192
Router(dhcp-config)# default-router 192.168.1.1

Router(config)# ip dhcp pool FINANCE
Router(dhcp-config)# network 192.168.1.64 255.255.255.192
Router(dhcp-config)# default-router 192.168.1.65

Router(config)# ip dhcp pool CUSTOMER
Router(dhcp-config)# network 192.168.1.128 255.255.255.192
Router(dhcp-config)# default-router 192.168.1.129
```

### Switch VLAN Configuration
```
Switch(config)# vlan 10
Switch(config-vlan)# name Admin_IT
Switch(config)# vlan 20
Switch(config-vlan)# name Finance_HR
Switch(config)# vlan 30
Switch(config-vlan)# name Customer_Service
```

---

## 📸 Screenshots

| Screenshot | Description |
|-----------|-------------|
| `screenshots/topology.png` | Full network topology |
| `screenshots/vlan_config.png` | VLAN setup on switch |
| `screenshots/dhcp_working.png` | Devices receiving auto IP |
| `screenshots/ping_test.png` | Inter-VLAN ping verification |
| `screenshots/wireless_config.png` | Access point configuration |

---

## 🔧 Key Concepts Used

- **VLANs** – Network segmentation by department
- **Router-on-a-Stick** – Inter-VLAN routing via subinterfaces
- **DHCP** – Automatic IP addressing for all hosts
- **Wireless (Access Points)** – Wi-Fi per department
- **Trunk Ports** – Carrying multiple VLANs between switch and router
- **802.1Q Encapsulation** – VLAN tagging on subinterfaces

---

## 📂 Files Included

```
Project2/
├── Project2.pkt          ← Cisco Packet Tracer file
├── README.md             ← This file
└── screenshots/
    ├── topology.png
    ├── vlan_config.png
    ├── dhcp_working.png
    ├── ping_test.png
    └── wireless_config.png
```

---

> 🔙 [Back to Main Portfolio](../README.md)
