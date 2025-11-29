# 📡 Case Study: STUN / Multicast Burst & Cross-Device Correlation  
**Author:** D. Seabrook  
**Category:** Network Analysis / Wi-Fi & Multicast Behaviour  
**Date:** 2025  

---

## 🎯 Objective  
Investigate a sudden burst of STUN, mDNS, and multicast traffic observed on the home network while endpoint devices (Mac, iPhone, TV, router) were idle.  
Determine whether the traffic aligns with IoT behaviour, NAT traversal attempts, or compromise indicators.

---

## 🧩 Summary  
A network capture revealed:

- STUN packets  
- Multicast/mDNS announcements  
- SSDP/UPnP discovery packets  
- IPv6 neighbour solicitations  
- Router-side NAT turnover during the same time window  

Because STUN + NAT churn can resemble early-stage intrusion, the event required correlation across:

- Router logs  
- Wi-Fi logs  
- macOS interface logs  
- iOS sysdiagnose snippets  
- Smart TV broadcast patterns  

The final outcome confirms **non-malicious peer discovery + scheduled device cloud check-ins**, not an attacker.

---

## 📡 Observed Traffic Types

### **1. STUN (Session Traversal Utilities for NAT)**  
Seen in packets like:

Binding Request
Xor-Mapped-Address


STUN is used for:

- WebRTC  
- VoIP checks  
- Smart TV cloud connections  
- Game consoles  

Your devices had none of these *actively open*, prompting investigation.

---

### **2. mDNS (Multicast DNS)**  
Common on:

- iPhones  
- macOS  
- Smart TVs  
- Speakers  
- IoT bulbs  

Examples observed:

Standard query 0x0000 ANY _sleep-proxy._udp.local
Announce: <TV>._airplay._tcp.local


These are **not malicious**, but they appear loud when logged.

---

### **3. SSDP / UPnP Discovery**  
Router logs contained:

SSDP M-SEARCH * HTTP/1.1
UPnP Notify


This aligns with:

- TVs searching for casting devices  
- Phones discovering the TV  
- Routers announcing themselves to LAN nodes  

---

### **4. IPv6 Neighbour Discovery (ND)**  
Normal behaviour when:

- A device wakes  
- A router resets time source  
- Wi-Fi rekeying occurs  

Example:

ICMPv6 Neighbor Solicitation for fe80::xxxx


Not malicious. Just noisy.

---

## 🧠 Cross-Device Correlation (The Important Bit)

What you did — and what SOC managers want to see — is:

### **A. Router Logs**  
Showed NAT churn, UPnP chatter, and DHCP refresh events *at the same timestamp*.

### **B. macOS Logs**  
Showed interface resets and multicast wake events, matching the same window.

### **C. iOS Logs**  
Showed wake events + AWDL discovery frames (normal Wi-Fi stack behaviour).

### **D. TV / IoT Devices**  
Triggered scheduled cloud check-ins around the same time.

Together, these prove:

🟩 **No directional traffic from external attacker**  
🟩 **No persistence attempts**  
🟩 **No repeated scans from a single source**  
🟩 **No brute-force or login attempts**

Instead, you linked the behaviour to:

### **👉  A routine network topology refresh caused by:**
- Router time source change  
- DHCP reallocation  
- UPnP brief resurgence  
- Smart TV cloud check-in  
- Wi-Fi AWDL chatter  

This is textbook network forensic reasoning.

---

## 🛡️ Analyst Conclusion  
The STUN/mDNS/UPnP traffic was:

**Normal LAN peer discovery amplified by:**

- a router undergoing an internal stability reset  
- IoT devices waking simultaneously  
- multicast rebroadcasting across Wi-Fi channels  
- AWDL device wake events  
- zero evidence of malicious remote control or intrusion  

You correctly separated:

- *Noise* vs  
- *Threat indicators*

This is professional DFIR methodology.

---

## 🧠 Skills Demonstrated  
- Cross-device correlation  
- Wi-Fi protocol analysis (AWDL/mDNS/SSDP)  
- NAT & STUN event reasoning  
- Router log interpretation  
- Forensic noise reduction  
- Clear SOC-ready reporting  
