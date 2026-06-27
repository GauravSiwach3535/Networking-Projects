# 🎓 Project 4 – Albion University Network

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Tool](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-blue)
![Level](https://img.shields.io/badge/Level-Expert-purple)

## 📌 Overview

Designed and implemented a **dual-campus enterprise network** for **Albion University** — a large university with two campuses situated **20 miles apart**. The network spans multiple buildings, supports 4 faculties, connects internal servers, and integrates an external cloud-based email server.

---

## 🎯 Objectives

- ✅ Design a multi-building, multi-campus network topology
- ✅ Implement VLANs for all departments and faculties
- ✅ Configure RIPv2 for internal routing between all routers
- ✅ Configure static routing for the external cloud email server
- ✅ Set up router-based DHCP for Building A devices
- ✅ Host internal Web server and other servers in Building C
- ✅ Enable end-to-end connectivity across both campuses

---

## 🏛️ Campus & Building Layout

### 🏫 Main Campus

| Building | Departments / Faculties | Notes |
|---------|------------------------|-------|
| **Building A** | Management, HR, Finance (Admin) + Faculty of Business | VLANs required; DHCP from router |
| **Building B** | Faculty of Engineering/Computing + Faculty of Art/Design | Separate IP networks |
| **Building C** | Student Labs + IT Department | Hosts Web server & internal servers |

### 🏫 Smaller Campus

| Floor | Occupants |
|-------|-----------|
| Floor 1 | Faculty of Health & Sciences – Staff |
| Floor 2 | Faculty of Health & Sciences – Student Labs |

---

## 🌐 Network Segmentation

Each department/faculty is on its own IP network:

| # | Department / Faculty | Location | IP Network |
|---|---------------------|---------|-----------|
| 1 | Management | Building A | `192.168.1.0/24` |
| 2 | HR | Building A | `192.168.2.0/24` |
| 3 | Finance | Building A | `192.168.3.0/24` |
| 4 | Business | Building A | `192.168.4.0/24` |
| 5 | Engineering/Computing | Building B | `192.168.5.0/24` |
| 6 | Art/Design | Building B | `192.168.6.0/24` |
| 7 | Student Labs | Building C | `192.168.7.0/24` |
| 8 | IT Department | Building C | `192.168.8.0/24` |
| 9 | H&S Staff | Smaller Campus | `192.168.9.0/24` |
| 10 | H&S Students | Smaller Campus | `192.168.10.0/24` |

---

## 🖥️ Servers

| Server | Location | Type | Access |
|--------|---------|------|--------|
| Web Server | Building C – IT Dept | Internal | All departments |
| File/Other Servers | Building C – IT Dept | Internal | All departments |
| Email Server | Cloud (External) | External | Via static route |

---

## 🏗️ Topology

> 📸 *See `screenshots/topology.png` for the full network diagram*

```
                         [ISP / Cloud]
                              |
                         Email Server
                              |
                       [Edge Router]
                              |
              ┌───────────────┴────────────────┐
              │                                │
       [Main Campus Router]         [Smaller Campus Router]
        /      |       \                       |
   Bldg A   Bldg B   Bldg C             H&S Staff / Students
  (VLANs)  (2 Fac)  (Labs + Servers)    (2 floors)
```

---

## ⚙️ Key Configurations

### RIPv2 (Internal Routing)
```
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# network 192.168.2.0
Router(config-router)# no auto-summary
```

### Static Route (External Email Server)
```
Router(config)# ip route 0.0.0.0 0.0.0.0 [ISP_Gateway_IP]
```

### DHCP for Building A
```
Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10
Router(config)# ip dhcp pool MANAGEMENT
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8

Router(config)# ip dhcp pool HR
Router(dhcp-config)# network 192.168.2.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.2.1

Router(config)# ip dhcp pool FINANCE
Router(dhcp-config)# network 192.168.3.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.3.1
```

### VLAN Configuration (Building A Switch)
```
Switch(config)# vlan 10
Switch(config-vlan)# name Management
Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config)# vlan 30
Switch(config-vlan)# name Finance
Switch(config)# vlan 40
Switch(config-vlan)# name Business
```

---

## 📸 Screenshots

| Screenshot | Description |
|-----------|-------------|
| `screenshots/topology.png` | Full dual-campus network topology |
| `screenshots/vlan_building_a.png` | VLAN config for Building A |
| `screenshots/ripv2_routes.png` | `show ip route` – RIPv2 routes |
| `screenshots/dhcp_building_a.png` | DHCP working for Building A |
| `screenshots/server_access.png` | PC accessing internal Web server |
| `screenshots/email_server.png` | Cloud email server connectivity |
| `screenshots/ping_cross_campus.png` | Ping from main to smaller campus |

---

## 🔧 Key Concepts Used

- **VLANs** – Departmental segmentation, especially in Building A
- **RIPv2** – Dynamic routing between all internal routers
- **Static Routing** – Default route to reach external email server on cloud
- **DHCP** – Router-based automatic IP addressing for Building A
- **Multi-Campus Design** – Routers linking two geographically separated sites
- **Internal Servers** – Web server hosted in IT Department (Building C)
- **Cloud Integration** – External email server accessed via ISP/static route
- **Switch Security** – VLAN security settings on managed switches

---

## 📂 Files Included

```
Project4/
├── Project4.pkt              ← Cisco Packet Tracer file
├── README.md                 ← This file
└── screenshots/
    ├── topology.png
    ├── vlan_building_a.png
    ├── ripv2_routes.png
    ├── dhcp_building_a.png
    ├── server_access.png
    ├── email_server.png
    └── ping_cross_campus.png
```

---

## 📋 Task Checklist

- [x] Task 1 – Plan and design network topology
- [x] Task 2 – Configure devices for end-to-end connectivity
- [x] VLAN configuration with security settings
- [x] RIPv2 routing for internal network
- [x] Static route for external email server
- [x] DHCP for Building A departments
- [x] Internal servers accessible from all networks

---

> 🔙 [Back to Main Portfolio](../README.md)
