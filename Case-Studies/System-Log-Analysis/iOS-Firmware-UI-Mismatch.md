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
