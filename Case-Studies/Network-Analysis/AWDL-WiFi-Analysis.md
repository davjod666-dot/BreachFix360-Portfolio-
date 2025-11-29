# 📡 AWDL Wireless Behaviour & Unsolicited Device Discovery  
**Analyst:** D. Seabrook  
**Category:** Network Analysis – Wireless / macOS / iOS  
**Context:**  
A device displayed unexpected peer-discovery activity despite no AirDrop/Handoff usage.  
This case documents a controlled analysis to validate whether AWDL traffic was malicious or benign.

---

## 🎯 Trigger Event
- AWDL interface (`awdl0`) repeatedly appeared and disappeared.
- AirDrop discovery packets observed without user interaction.
- Multicast DNS (mDNS) traffic persisted even after sharing features disabled.
- Device logs indicated Wi-Fi scanning during idle periods.

---

## 📁 Evidence Collected
- Wireshark PCAPs  
- macOS/iOS system logs  
- Router-level connection history  
- Known AWDL signature patterns

---

## 🔍 Analysis

### **1. AWDL Virtual Interface Creation**
Frequent `awdl0` creation/teardown events were captured.  
This behaviour matches Apple's **background peer-discovery** used for:

- AirDrop  
- Handoff  
- Peer-to-peer Wi-Fi frameworks  
- Continuity services  

### **2. Discovery Frames Present**
Discovery frames were visible even with the device locked.  
These frames matched Apple AWDL beaconing intervals.

No external MAC addresses showed persistence or pairing attempts outside normal ranges.

### **3. mDNS Persistence**
mDNS (`224.0.0.251`) continued after user-disabled sharing features.  
This is expected, as system-level daemons still use multicast for:

- Sleep Proxy  
- Bonjour service discovery  
- Exposure Notification framework  

### **4. No Signs of Malicious Beacon Spoofing**
No rogue MAC rotation patterns  
No anomalous RSSI spikes  
No AirDrop-pairing negotiation  

---

## 🚨 Indicators Observed (All Expected)
| Indicator | Observation | Assessment |
|----------|-------------|------------|
| AWDL channel hopping | Present | Normal |
| mDNS multicast | Persistent | Expected |
| Peer discovery frames | Present | Benign |
| Locked-device activity | Present | System-level behaviour |

---

## 🧠 Conclusion
AWDL activity did **not** indicate compromise.  
It aligned with normal Apple wireless background behaviour, including peer discovery and Wi-Fi scanning.

No evidence of malicious AWDL spoofing, rogue AirDrop attempts, or unauthorized peer negotiation.

---

## 🛡️ Recommendations
- Disable AirDrop (Receiving Off)  
- Disable Handoff  
- Turn off “Auto-Join Hotspots”  
- Router-level mDNS filtering if hardened environment required  
