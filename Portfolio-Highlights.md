# ⭐ Portfolio Highlights – D. Seabrook

This document provides a high-level summary of selected cybersecurity case studies and analyses from the BreachFix360 portfolio.

---

## 📡 Wireless & Local Network Behaviour

### **1. AWDL & Unexpected Device Discovery**
**Category:** Wi-Fi / Wireless Forensics  
**Summary:**  
Investigated irregular AWDL traffic leading to unsolicited peer discovery, AirDrop beaconing, and mDNS persistence.  
Conclusion: **System-level Apple discovery traffic, not adversarial.**

---

## 🔐 TLS / Port Behaviour

### **2. Port 443 Loopback Activity**
**Category:** TLS / Process Correlation  
**Summary:**  
Observed persistent TLS sessions to localhost:443.  
Conclusion: **Background Apple telemetry using ATS/internal routing. No external hosts.**

---

## 🌐 UDP / NAT Traversal

### **3. STUN Multicast Events**
**Category:** UDP / WebRTC / NAT**  
**Summary:**  
Unsolicited STUN + UDP multicast packets on idle network.  
Conclusion: **WebRTC keep-alives & mDNS service discovery, not malicious.**

---

## 🛰️ ISP / Router Events

### **4. Telstra WAN, DHCP & TR-069 Noise**
**Category:** ISP Logs Review  
**Summary:**  
Unexpected line drops, time drift, TR-069 polls.  
Conclusion: **Standard Telstra ACS polling & NTP issues, not attacker behaviour.**

---

## 📱 iOS / System Log Analysis

### **5. iOS Firmware Version Mismatch**
**Category:** iOS Forensics  
**Summary:**  
UI displayed version 18.6.1 after a DFU restore, but system logs indicated an older build during restore.  
Conclusion: **Benign restore artefact caused by mid-restore version reporting logic.**

---

# 📈 Strengths Demonstrated
- Clear articulation of findings  
- Correct identification of benign vs malicious indicators  
- Pattern-based analysis  
- Defensive recommendations  
- SOC-style summary formatting  
- Experience with Apple platforms, Wireshark, router logs, and OS-level telemetry  

---

# 🏁 Summary
This portfolio demonstrates practical, real-world analytical ability and readiness for Tier 1 SOC, junior DFIR, or security operations work.  
All analysis is original, evidence-based, and structured for professional evaluation.

---
