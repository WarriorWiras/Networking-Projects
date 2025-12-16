# 🛡️🌐 Enterprise Network Security Project

[![Network Security](https://img.shields.io/badge/Domain-Network%20Security-red)]()
[![Blue Team](https://img.shields.io/badge/Focus-Defence-blue)]()
[![Red Team](https://img.shields.io/badge/Focus-Attack-orange)]()
[![Platform](https://img.shields.io/badge/Environment-Enterprise%20Lab-green)]()

> **An end-to-end enterprise network security project** that combines **secure network design**, **attack simulation**, and **defensive monitoring** - built and tested in a controlled academic environment.

This project is designed to feel **real**, not theoretical. It mirrors how modern enterprises design networks, defend them, and validate their security posture through authorised attack testing.

---

## 📘 Section 1 - Enterprise Network Overview

### 🎯 Design Objectives & Security Philosophy

This enterprise network was designed with a **defence-in-depth philosophy**, combining strong architectural controls with operational visibility. The goal was not just to make attacks *difficult*, but to ensure that **any abnormal behaviour becomes observable, traceable, and containable**.

The core objectives guiding the design were:

* 🔐 **Least-Privilege by Default** - users, servers, and administrators only access what they need
* 🧩 **Strong Segmentation** - clear trust boundaries between departments, services, and management
* 🔄 **Resilience & Redundancy** - eliminate single points of failure where feasible
* 👁️ **Visibility over Obscurity** - detect attacks rather than assuming prevention is perfect
* ⚖️ **Realism** - mirror how enterprise networks are actually built and operated

This philosophy ensures the network remains **secure, observable, and defensible**, even under active attack.

---

### 🏗️ Enterprise Topology Architecture

The network follows a **hierarchical enterprise design**, separating responsibilities across layers to improve scalability, fault isolation, and security control.

#### 🧠 Core Layer

* Dual **Core Switches (A & B)** provide aggregation and high availability
* Trunk links carry multiple VLANs across the backbone
* Redundancy ensures continued operation if a core device fails

The core layer is responsible for **fast, reliable internal connectivity** and forms the backbone of inter-VLAN communication.

#### 🖧 Access Layer

* Multiple **Layer-2 access switches** connect departmental endpoints
* Each department is isolated within its own VLAN
* Access switches enforce segmentation at the edge, limiting lateral movement

This prevents a compromise in one department from automatically spreading across the enterprise.

#### 🚪 Perimeter & Edge Layer

* An **ASA Firewall** sits between internal networks and external connectivity
* Enforces north–south traffic inspection and policy control
* Provides a single, auditable enforcement point for inbound and outbound flows

---

### 🗂️ VLAN & Subnet Design Strategy

Network segmentation is a **primary security control**, not an afterthought.

The enterprise network is divided into:

* 🏢 **Departmental VLANs** - isolating user groups and business functions
* 🧱 **Infrastructure VLANs** - routing, DHCP, and internal services
* 🌐 **Service / DMZ-like Zones** - hosting exposed or semi-exposed services
* 🛠️ **Management Networks** - restricted administrative access only

Each VLAN represents a **trust boundary**. Traffic between VLANs must traverse controlled routing or firewall paths, ensuring that:

* East–west movement is limited
* Compromised hosts have reduced blast radius
* Security policies are enforceable and auditable

---

### 🔥 Perimeter Security & DMZ Design

The firewall is not merely a packet filter - it is the **security gatekeeper** of the enterprise.

Its responsibilities include:

* Stateful traffic inspection
* Application-aware visibility
* Enforced access control policies
* Detection of abnormal connection behaviour

Public-facing or higher-risk services are deliberately **segregated** from internal user networks. This ensures that even if an exposed service is compromised, the attacker does not gain unrestricted internal access.

---

### ☁️ Virtualisation & Server Architecture

A **Proxmox virtualisation platform** hosts enterprise services, reflecting how modern organisations consolidate infrastructure.

Key characteristics:

* Multiple virtual machines mapped to different logical LANs
* Separation of services such as:

  * Web services
  * DNS services
  * VPN and remote access
  * Jump host / administrative services
  * TACACS+ server
  * And Many More!

This separation ensures that **service compromise does not equal infrastructure compromise**.

---

### 🛠️ Management & Monitoring Plane

Administrative access is treated as **high-risk and high-value**.

Management traffic is:

* Isolated from user and service networks
* Restricted to authorised systems
* Logged for audit and investigation

This design ensures defenders maintain control even during partial compromise, and enables accurate forensic reconstruction during incident response.

---

### ⚖️ Security Assumptions & Trade-offs

To maintain realism, the design acknowledges that:

* No system is perfectly secure
* Some services must remain reachable to fulfil business needs
* Monitoring and detection are as important as prevention

As such, certain attack paths are **intentionally possible**, allowing the security posture to be tested and validated in later phases.

This completes the architectural foundation upon which the **attack and defence analyses** are performed.

---

### 🏗️ High-Level Architecture

The environment consists of:

* 🖧 **Access Layer** - Departmental endpoints connected via L2 switches
* 🧠 **Core Layer** - Redundant core switches handling aggregation and routing
* 🚪 **Perimeter Layer** - ASA firewall enforcing inspection and policy control
* ☁️ **Virtualised Server Zone** - Enterprise services hosted on Proxmox
* 🛠️ **Management Network** - Isolated administrative and monitoring access

This layered approach ensures both **north–south** and **east–west** traffic is tightly controlled.

---

### 🗂️ Network Segmentation Highlights

* Multiple **departmental VLANs** to isolate users
* Dedicated **DMZ-like service zones** for exposed services
* Separate **management and infrastructure networks**
* Centralised **DHCP and routing control**

Segmentation ensures that a compromise in one zone does **not** automatically endanger the entire environment.

---

## ⚔️ Section 2 - Attack Report (Red Team Perspective)

### 🎯 Objective

The attack phase evaluates how well an enterprise network withstands **realistic attacker behaviour**. All activities were conducted with permission and within scope.

The focus is on:

* 🔎 Discovering exposed services
* 🔑 Evaluating authentication strength
* 🧪 Testing service resilience
* 📉 Identifying weak configurations

---

### 🧭 Attack Methodology

The red team activities follow a structured lifecycle:

1. **Reconnaissance & Enumeration** 🕵️

   * Network discovery
   * Service fingerprinting

2. **Attack Surface Analysis** 🧩

   * Web and infrastructure exposure
   * Access control behaviour

3. **Credential & Access Testing** 🔐

   * Authentication hardening checks
   * Brute-force resistance evaluation

4. **Availability Testing** 🌊

   * Service behaviour under stress
   * Resilience against resource exhaustion

---

### 🚨 High-Level Findings

* Strong perimeter filtering reduced attack surface
* Limited but **high-value services** were externally reachable
* Authentication mechanisms lacked sufficient hardening
* Certain services showed **degraded behaviour under load**

These findings help validate which defensive controls are effective - and which require improvement.

---

## 🛡️ Section 3 - Defence Report (Blue Team Perspective)

### 🎯 Objective

The defence phase focuses on **visibility, detection, and analysis** rather than prevention alone. The goal is to answer one key question:

> *Can defenders see and understand what is happening on the network?*

---

### 🔍 Defensive Controls & Visibility

Implemented controls include:

* 🔥 Stateful firewall inspection
* 📊 Application-aware traffic visibility
* 📈 Conversation and flow monitoring
* 🗃️ Centralised system and authentication logs
* 🧠 Cross-host log correlation

These layers allow defenders to detect activity even when attacks do not immediately succeed.

---

### 👁️ Defensive Observations

From monitoring and logs, defenders were able to:

* Detect **reconnaissance and scanning patterns** early
* Identify **abnormal traffic volumes** from untrusted sources
* Observe **authentication anomalies**
* Spot signs of **potential persistence behaviour** through system logs

This demonstrates how **visibility is just as critical as prevention** in modern enterprise security.

---

## 🔁 Attack ↔ Defence Relationship

This project intentionally highlights the **feedback loop** between attackers and defenders:

* Attacks expose weak assumptions
* Defences reveal blind spots
* Improvements strengthen the overall system

Security is not static - it evolves through **continuous testing and monitoring**.

---

## ⚠️ Disclaimer

> 🛑 This project was conducted **strictly for educational purposes** in an authorised academic environment.

* No real-world systems were targeted
* All attack activities were approved and controlled
* Content is shared to promote **learning and defensive improvement**, not misuse

Always obtain **explicit permission** before testing any system.

---

## 📄 License

This repository is provided for **educational reference only** and is not intended for commercial use.

---

✨ *Secure by design. Tested by attack. Strengthened through defence.*
