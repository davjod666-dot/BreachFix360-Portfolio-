# 📶 STUN Multicast & UDP Event Analysis  
**Analyst:** D. Seabrook  
**Category:** UDP / WebRTC / NAT Traversal  
**Context:**  
Device displayed periodic STUN packets and multicast bursts, raising questions about whether NAT traversal or P2P activity was occurring.

---

## 🎯 Trigger Event
- STUN binding requests observed on idle network  
- UDP 3478 activity  
- Multicast traffic to 224.x.x.x  
- Router logs flagged bursts during quiet periods

---

## 📁 Evidence Collected
- Wireshark PCAPs  
- Router connection logs  
- mDNS packet breakdown  
- NAT traversal analysis  

---

## 🔍 Analysis

### **1. STUN Traffic**
STUN is used by:

- WebRTC  
- FaceTime  
- Wi-Fi calling  
- Messaging frameworks  
- Browser-based P2P frameworks  

Packets matched **standard NAT keep-alive patterns**.

No foreign STUN servers were contacted.

### **2. Multicast Behaviour**
mDNS (`224.0.0.251`) persisted due to:

- Sleep Proxy  
- Service discovery  
- Local network enumeration  

SSDP was active at normal DHCP renewal intervals.

### **3. No Malicious Indicators**
No suspicious ports  
No random high-entropy STUN behaviour  
No hole-punch attempts  
No rogue external peers  

---

## 🚨 Indicators Observed
| Indicator | Observation | Assessment |
|----------|-------------|------------|
| STUN NAT keep-alive | Present | Benign |
| mDNS multicast | Persistent | Expected |
| UDP bursts | Periodic | Normal |
| Foreign STUN IPs | None | Clean |

---

## 🧠 Conclusion
Traffic patterns were **normal WebRTC/mDNS behaviour**, not attacker-controlled UDP signalling.

---

## 🛡️ Recommendations
- Disable Wi-Fi calling if unnecessary  
- Restrict WebRTC in browsers  
- Apply multicast filtering if hardening  
