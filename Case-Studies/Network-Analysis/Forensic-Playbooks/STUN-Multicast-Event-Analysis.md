# 🌐 Case Study: STUN & Multicast Traffic Spike Analysis

**Author:** David Seabrook  
**Category:** Network Analysis / Router Traffic  
**Date:** 2025  

---

## 🎯 Objective
Analyse unexpected bursts of STUN (UDP 3478) and multicast traffic observed on home routers and determine whether activity indicated NAT traversal attempts, VoIP activity, or external probing.

---

## 🧪 Symptoms Observed
- Sudden bursts of STUN packets visible in syslogs  
- Floods of SSDP / UPNP multicast to 1900/udp  
- Traffic appearing even when no video/audio apps were running  
- Router CPU spike during traffic surges  

---

## 🔎 Key Findings

### 🔹 STUN Traffic Origin
Most STUN traffic originates legitimately from:
- Apple FaceTime  
- iMessage call setup  
- WebRTC libraries in browsers  

However, the frequency observed exceeded normal expectations.

### 🔹 SSDP/UPNP Bursts
UPNP discovery storms triggered by:
- Smart TV  
- Chromecasts  
- IoT devices  
- Misconfigured router UPNP tables

These can imitate malicious probing when misfiring.

### 🔹 Router CPU Spike
Router logs showed:
- Repeated NAT table resets  
- WAN DHCP renewals under load  
- Behaviour consistent with consumer routers under stress  

---

## 🛡️ Mitigation
- Disable UPNP (recommended)  
- Disable multicast forwarding  
- Create router firewall rules for outbound STUN  
- Replace consumer router with hardened hardware (Ubiquiti, etc.)  

---

## 📌 Outcome
Traffic was determined to be a mixture of normal discovery mechanisms and router instability — **not external compromise**.

But logging the behaviour was crucial for proper diagnosis and network hardening.
