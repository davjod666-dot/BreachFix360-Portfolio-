# 📡 Case Study: AWDL & Wi-Fi P2P Activity Investigation

**Author:** David Seabrook  
**Category:** Network Analysis / Wireless Forensics  
**Date:** 2025  

---

## 🎯 Objective
Analyze unexpected Wi-Fi activity related to Apple's AWDL (Apple Wireless Direct Link) to determine whether it contributed to unexplained device pairing attempts or network surface exposure.

---

## 🧪 Symptoms Noticed
- Multiple Wi-Fi MAC addresses appearing/disappearing rapidly  
- AWDL creation/teardown events during unrelated usage  
- Persistent Bonjour/mDNS queries even after service disabled  
- Attempted AirDrop pairing events on locked devices  

---

## 🔎 Analysis Summary
### 🔹 AWDL Interface Activity
- Logs show repeated creation of `awdl0` virtual interface.  
- Activity continued despite AWDL-dependent services being disabled.  
- Behaviour consistent with **background peer discovery**.

### 🔹 Unsolicited Peer Discovery
- AirDrop-like discovery frames captured without user interaction.  
- Strong indicator that discovery traffic wasn’t user-initiated.

### 🔹 mDNS / Multicast Behaviour
- Background mDNS queries persisted even after Bonjour service disabled.  
- Suggests an underlying system-level component still advertising/consuming discovery packets.

---

## 🛡️ Mitigation & Hardening
- Disable AirDrop, Handoff, and Wi-Fi Sharing  
- Enable Lockdown Mode for advanced protection  
- Block mDNS/SSDP multicast at router layer  
- Disable “Auto-Join Hotspots” feature  

---

## 📌 Outcome
AWDL was verified as active during periods where it should not have been.

This reinforces the need to inspect background wireless frameworks during intrusion investigations, as peer-to-peer discovery can expand the attack surface unnoticed.