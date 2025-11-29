# 🌐 Case Study: Telstra Router DHCP / UPnP / NAT Anomaly  
**Author:** D. Seabrook  
**Category:** Network Forensics / Edge Device Behaviour  
**Date:** 2025  

---

## 🎯 Objective  
Analyse abnormal DHCP, NAT traversal, and UPnP behaviour observed on a Telstra home router (Cobra/DumaOS variant).  
Determine whether the events represent remote access, internal misconfiguration, or benign network chatter.

---

## 🧩 Summary  
During routine network monitoring, the router produced a burst of events involving:

- DHCP reassignments without user action  
- Repeated NAT table rebuilds  
- UPnP port mapping appearing/disappearing  
- STUN- and mDNS-like traffic from devices that were idle  
- Sessions initiating from the WAN side but not completing  
- Intermittent DoS-like bursts without corresponding external traffic volume  

These patterns warranted investigation due to their overlap with common remote-access and NAT-hole-punching behaviours.

---

## 📡 Key Indicators Observed

### **1. DHCP Lease Cycling**  
Router logs showed multiple instances of:

daemon.info dnsmasq-dhcp: DHCPACK(br-lan) <device> <MAC> <IP>
daemon.info dnsmasq-dhcp: DHCPREQUEST(br-lan)
daemon.info dnsmasq-dhcp: DHCPACK


Despite the devices not reconnecting.  
This often appears when:

- A device’s network stack resets silently  
- UPnP or NAT-PMP subsystems trigger ephemeral refreshes  
- A remote host attempts NAT hole punching (less common)

---

### **2. UPnP Port Maps Flapping**  
Entries similar to:

upnp: external port 49152 mapped to 192.168.x.x:49152
upnp: external port removed
upnp: recreate map (same port)


This *can* appear in gaming or P2P workloads — but your device was idle.  
Suspicious enough to warrant deeper review.

---

### **3. NAT Table Reconstruction Events**  
Router kernel reported:

nf_conntrack: table full, dropping packet
rebuilding NAT table


This indicates:

- A spike in connection attempts  
- Or ghost devices generating flows  
- Or consumer-router firmware bug causing conntrack saturation

---

### **4. STUN-style Traffic**  
STUN often indicates peer-discovery behaviour for:

- WebRTC  
- VoIP  
- P2P tunnels  
- Smart devices performing cloud checks  

Seeing STUN when **no apps were running** raises legitimate questions.  
(This is why STUN was split into its own case file — additional depth.)

---

### **5. No Evidence of Sustained Remote Access**  
After correlation:

- No consistent bi-directional flow  
- No external IP maintaining long session durations  
- No valid authentication logs  
- No repeated port scan signature from the same IP  
- No evidence of telnet/SSH exploitation attempts  

This supports a conclusion of:  

> **Transient behaviour + firmware quirks + network stack resets**,  
> not active compromise.

---

## 🧪 Analytical Summary  
The router exhibited *unusual but not malicious* behaviour:

- UPnP flapping consistent with misbehaving smart devices  
- NAT rebuilds consistent with DumaOS bugs  
- DHCP refreshes common under load or firmware instability  
- STUN bursts tied to “cloud check-in” behaviour from TV/IoT hardware  
- No persistent or authenticated intrusion  

Your documentation style **correctly separated each anomaly**, making it clear, measurable, and repeatable — the exact skill SOC teams look for.

---

## 🛡️ Hardening Applied  
- Disabled UPnP  
- Locked DHCP reservations  
- Disabled WAN management  
- Forced DNS to Cloudflare 1.1.1.1  
- Verified NAT tables stable post-reboot  
- Updated router time source (the “frozen time bug” was root cause of failed log correlation)

---

## 🧠 Skills Demonstrated  
- Understanding of edge-router behaviours (DumaOS/Telstra Cobra)  
- Ability to distinguish **odd** from **malicious**  
- DHCP / NAT / UPnP / STUN traffic interpretation  
- Evidence-based reporting with zero fluff  
- Clear decision-making under uncertainty  
