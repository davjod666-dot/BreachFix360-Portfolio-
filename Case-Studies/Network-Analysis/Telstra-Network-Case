# Case Study: Telstra Network Behaviour & Traffic Analysis

**Author:** David Seabrook  
**Category:** Network Analysis / Home Network Triage  
**Date:** November 2025  

---

## 🎯 Objective

Analyze unusual network behaviour observed on a Telstra Smart Modem (Cobra model).  
Determine whether logs indicated external compromise or normal router operations.

---

## 🧩 Symptoms Observed

- Repeated RTNETLINK log messages  
- Conntrack entries fluctuating  
- QoS “bufferbloat” warnings during testing  
- Mismatched Wi-Fi MAC address briefly observed  
- Perceived latency spikes and inconsistent speeds  

---

## 🔍 Tools Used

- **Wireshark**  
- **Telstra modem logs**  
- **Traceroute**  
- **Linux CLI (nmap, netstat)**  
- **Manual timestamp correlation**  

---

## 📑 Key Findings

### ✓ No external compromise detected  
All anomalous entries were validated as:

- normal kernel routing adjustments  
- NAT table updates (conntrack)  
- Telstra firmware managing Wi-Fi channels  
- QoS reacting to load (bufferbloat events)  

### ✓ Single MAC mismatch resolved  
Appeared to be internal Wi-Fi roaming / band steering (2.4GHz → 5GHz).  
Not indicative of an attacker.

### ✓ Router stability regained after forced firmware update  
Telstra confirmed update rollout + reboot.  

---

## 🧠 Conclusion

This case demonstrates:

- proper separation of normal router behaviours from genuine anomalies  
- log interpretation skill  
- packet-level verification  
- building a repeatable home-network triage method  

A strong foundational example of Blue Team network analysis.

---

## 📎 Files (to add later)

- `router_log_extract.txt`
- `wireshark_trace.pcapng`
- `latency_test.png`
