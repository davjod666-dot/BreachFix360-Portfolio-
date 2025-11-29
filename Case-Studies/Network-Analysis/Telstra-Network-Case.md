# 🛰️ Telstra Router Log Investigation – DHCP, TR-069 & Line Drops  
**Analyst:** D. Seabrook  
**Category:** ISP Log Analysis  
**Context:**  
Router displayed frequent DHCP renewals, TR-069 polling, NTP drift, and periodic WAN dropouts.

---

## 🎯 Trigger Event
- Router time fell out of sync → causing HTTPS errors  
- DHCP churn observed during quiet hours  
- Multiple ACS (TR-069) contact attempts  
- Sudden WAN drops following a local outage reported

---

## 📁 Evidence Collected
- Telstra Cobra router logs  
- WAN connection history  
- Device event tables  
- NTP sync error messages  

---

## 🔍 Analysis

### **1. TR-069 Remote Management**
TR-069 is legitimate for Telstra’s modem management.  
Polling intervals matched their documentation.

### **2. DHCP Renewals**
Lease renewal timings aligned with ISP defaults.  
No rogue DHCP servers detected.

### **3. NTP Drift**
Router time fell behind by hours.  
This caused:

- certificate validation failures  
- HTTPS connection issues  
- misleading network telemetry  

NTP resync resolved the errors.

### **4. WAN Dropouts**
Dropped sessions correlated exactly with:

- local outages  
- reported line instability  
- post-maintenance reboot window  

---

## 🚨 Indicators Observed
| Indicator | Finding | Assessment |
|----------|---------|-----------|
| TR-069 | Expected | Benign |
| Time drift | Significant | Benign but disruptive |
| DHCP churn | Present | Normal |
| WAN drops | Present | ISP-related |

---

## 🧠 Conclusion
All anomalies were attributed to **normal ISP behaviour**, NTP issues, and external outages.  
No malicious network control or interception detected.

---

## 🛡️ Recommendations
- Replace router if WAN instability persists  
- Maintain consistent NTP sync  
- Run periodic manual log collection for baseline comparisons  
