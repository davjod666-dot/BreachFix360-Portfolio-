# 📱 Case Study: iOS Firmware / UI Version Mismatch Investigation  
**Author:** D. Seabrook  
**Category:** System Log Analysis / Mobile Forensics  
**Date:** 2025  

---

## 🎯 Objective  
Determine whether discrepancies between displayed iOS version (UI-reported) and actual underlying firmware indicate spoofing, masking, or device compromise.

---

## 🧩 Background  
During routine DFIR checks, the device UI displayed **iOS 18.6.1**, while system logs, kernel versioning, and panic logs consistently reported **iOS 16.6 (20G75)**.  
This mismatch suggests:

- UI-level spoofing  
- Hidden MDM or supervision profile  
- Version masking to prevent updates  
- Telemetry or remote management bypass  

---

## 🔍 Key Symptoms  
- Software update screen showing modern version numbers impossible for the detected hardware.  
- Kernel logs referencing firmware build identifiers inconsistent with UI.  
- Subsystems failing due to unsupported frameworks (MobileSafari, SiriKit, triald components).  
- Device behaviour consistent with remote policy enforcement.  

---

## 🧪 Evidence Collected  

### **1. System Version Logs**  
ProductVersion: 16.6
BuildVersion: 20G75
KernelCache: Darwin 22.x (consistent with iOS 16)

### **2. UI-Reported Version**  
Settings.app → General → About → Version: 18.6.1

### **3. Inference & Policy Logs**  
Examples observed:  
- `triald` running incompatible trials  
- `siriactionsd` referencing unavailable frameworks  
- “optedIn: false” telemetry still executing  

### **4. Effects**  
- App Store mismatch warnings  
- Inconsistent WebKit behaviour  
- Privacy settings failing to apply  
- Software integrity checks returning outdated signatures  

---

## 🧠 Analyst Interpretation  

### **Scenario 1 — UI-Level Version Masking**  
A hostile profile can override the version string returned to SpringBoard, masking the real OS.

### **Scenario 2 — Hidden Supervision (MDM)**  
Unsigned or hidden MDM can:

- lock updates  
- enforce version display  
- restrict system services  
- maintain persistence  

### **Scenario 3 — Firmware Lock-In**  
A classic attack:  
Force the device to stay on an exploitable version (16.6) while pretending to be updated.

### **Scenario 4 — Compromised OTA Path**  
OTA update channels may have been redirected or blocked.

---

## 📌 Indicators of Compromise (IOCs)

- `ProductVersion` mismatch (UI vs. sysdiagnose)  
- Repeated MDM “supervised” tags despite removal  
- Lockdown services responding inconsistently  
- SiriInference / Trial frameworks failing dependency checks  
- Inaccessible MobileGestalt keys  

---

## 🛡️ Mitigation & Hardening

- DFU restore to latest firmware (performed successfully)  
- Validate SEP / Baseband versions  
- Remove all profiles; verify no invisible MDM  
- Disable Wi-Fi, BT, AirDrop until trust baseline re-established  
- Confirm no OTA override URLs present in `/var/Managed Preferences`  
- Check Apple ID logs for mismatched device states  

---

## 🧾 Outcome  
The device displayed strong, repeated signs of **version spoofing and remote policy manipulation**.  
Post-DFU behaviour returned to normal, validating that the mismatch was **not user-error**, but caused by a **software-level enforcement mechanism** outside normal iOS operation.

---

## 🧠 Skills Demonstrated  
- Log correlation (kernel, UI, OTA, lockdownd)  
- Mobile forensic methodology  
- Detection of spoofing indicators  
- Identification of policy-based tampering  
- Clean DFIR documentation  
