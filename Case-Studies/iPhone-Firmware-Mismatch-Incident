# Case Study: iPhone Firmware Masking & Version Mismatch Investigation

**Author:** David Seabrook  
**Category:** Mobile Security / Device Triage  
**Date:** November 2025  

---

## 🎯 Objective

Investigate an iPhone 14 Pro Max that appeared to be running a modern iOS version (18.6.1) but, after forensic triage, was proven to be running a much older firmware (16.x).  
This case study demonstrates mobile device triage, log interpretation, and identifying spoofed system reporting.

---

## 🧩 Symptoms Observed

- Device UI reported **iOS 18.6.1**  
- DFU restore logs showed **16.x firmware**  
- System services exhibited behaviour inconsistent with 18.x  
- Multiple subsystem logs (e.g., lockdownd, analytics) did not match expected iOS version schema  

---

## 🔍 Methods Used

- **DFU Mode Full Restore**  
- Examination of:
  - `lockdownd.log`
  - `MAAutoAsset_Atomic_History`
  - Apple Mobile Restore logs
  - System analytics  
- Cross-checking build identifiers  
- Eliminating MDM/supervision possibilities  
- Verifying OTA history  

---

## 📑 Key Findings

- The iPhone was **not running** the version reported in the UI  
- The spoofing was *superficial*, likely a UI-only mismatch caused by corrupted or inconsistent system metadata—not a remote compromise  
- Post-DFU logs confirmed:
  - correct firmware restored  
  - no unauthorised configuration persisted  
  - device services returned to normal behaviour  

---

## 🧠 Conclusion

This incident demonstrates the importance of:

- validating UI-reported information against system logs  
- using DFU mode for trustworthy baselines  
- correlating findings across multiple log sources  
- avoiding assumptions during mobile triage

A strong example of mobile security analysis and log interpretation.

---

## 📎 Files (to add later)
- `lockdownd.log`
- `restore.log`
- `MAAutoAsset_Atomic_History.log`
