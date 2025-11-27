# Telstra Traceroute & Network Analysis – Simulated Attack Recording

**Date:** November 2025  
**Author:** David Seabrook  
**Category:** Network Analysis / Incident Review  

---

## 🧠 Summary

This report documents a staged attack simulation captured on a Telstra Cobra modem.  
The goal was to interpret early-stage network anomalies, traceroute behaviour, and Wi-Fi/MAC inconsistencies.

This simulation was used for training and portfolio development.

---

## 🔍 Key Observations

- No confirmed external compromise  
- Router logs (`RTNETLINK`, `conntrack`) aligned with normal kernel behaviour  
- Bufferbloat (BBLOAT) results normal after QoS  
- One internal MAC mismatch validated as an internal link, not an intrusion  
- Wireshark traces matched expected NAT traversal and broadcast noise  

---

## 🧰 Tools Used

- **Telstra Smart Modem / Cobra** log exports  
- **Wireshark**  
- **Linux CLI (nmap, traceroute, ss)**  
- **PDF lab analysis**  
- **AI-assisted interpretation**  

---

## 📎 Files Included

(You will upload these later)

- `traceroute.txt`  
- `router-log.txt`  
- `wireshark-capture.pcapng`

---

## ✅ Conclusion

The scenario behaved consistently with a controlled training simulation.  
No real threat actors were identified, but the workflow reinforced:

- baseline network behaviour  
- router log interpretation  
- packet flow mapping  
- anomaly classification  

Great foundation for future SOC / DFIR work.
