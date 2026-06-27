# 📡 Project 1 – Two Department Network

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Tool](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-blue)
![Level](https://img.shields.io/badge/Level-Beginner-yellow)

## 📌 Overview

Designed and implemented a basic network topology in **Cisco Packet Tracer** to facilitate communication between two distinct departments: **Accounts** and **Delivery**.

The project focuses on fundamental networking concepts including subnetting, IP addressing, and basic routing between two separate department networks.

---

## 🎯 Objectives

- ✅ Connect two departments (Accounts & Delivery) over a routed network
- ✅ Each department contains at least 2 PCs
- ✅ Configure appropriate IP addresses, subnet masks, and gateways
- ✅ Connect all devices using correct cable types
- ✅ Verify end-to-end communication using ping

---

## 🌐 Network Design & IP Addressing

### Subnetting Calculation

| Parameter | Value |
|-----------|-------|
| Base Network | `192.168.40.0` |
| Number of Subnets | 2 (Two Departments) |
| Borrowed Bits (n) | 1 |
| Subnet Mask | `255.255.255.128` (/25) |
| Block Size | 128 |

### Subnet Table

| Subnet | Department | Network ID | Usable Range | Broadcast |
|--------|------------|-----------|-------------|-----------|
| Subnet 1 | Accounts | `192.168.40.0` | `192.168.40.1` – `192.168.40.126` | `192.168.40.127` |
| Subnet 2 | Delivery | `192.168.40.128` | `192.168.40.129` – `192.168.40.254` | `192.168.40.255` |

---

## 🖥️ Device Configuration

### Accounts Department (Subnet 1)
| Device | IP Address | Subnet Mask | Gateway |
|--------|-----------|------------|---------|
| PC1 | 192.168.40.1 | 255.255.255.128 | 192.168.40.126 |
| PC2 | 192.168.40.2 | 255.255.255.128 | 192.168.40.126 |
| Router (Fa0/0) | 192.168.40.126 | 255.255.255.128 | — |

### Delivery Department (Subnet 2)
| Device | IP Address | Subnet Mask | Gateway |
|--------|-----------|------------|---------|
| PC3 | 192.168.40.129 | 255.255.255.128 | 192.168.40.254 |
| PC4 | 192.168.40.130 | 255.255.255.128 | 192.168.40.254 |
| Router (Fa0/1) | 192.168.40.254 | 255.255.255.128 | — |

---

## 🏗️ Topology

> 📸 *See `screenshots/topology.png` for the full network diagram*

```
[Accounts PCs] — Switch1 — Router — Switch2 — [Delivery PCs]
     Subnet 1                              Subnet 2
  192.168.40.0/25                     192.168.40.128/25
```

---

## 📸 Screenshots

| Screenshot | Description |
|-----------|-------------|
| `screenshots/topology.png` | Full network topology |
| `screenshots/ping_test.png` | Successful ping between departments |
| `screenshots/ip_config.png` | IP configuration on PCs |

---

## 🔧 Key Concepts Used

- **Subnetting** – Dividing a network into two subnets using /25 mask
- **Static Routing** – Configured on router for inter-department communication
- **IP Addressing** – Manual assignment of IPs, masks, and gateways
- **Cable Selection** – Straight-through and crossover cables used appropriately

---

## 📂 Files Included

```
Project1/
├── Project1.pkt          ← Cisco Packet Tracer file
├── README.md             ← This file
└── screenshots/
    ├── topology.png
    ├── ping_test.png
    └── ip_config.png
```

---

## ✅ Verification

Communication between Accounts and Delivery departments was verified using the **ping** command from PC1 (Accounts) to PC3 (Delivery) — confirming successful end-to-end connectivity.

---

> 🔙 [Back to Main Portfolio](../README.md)
