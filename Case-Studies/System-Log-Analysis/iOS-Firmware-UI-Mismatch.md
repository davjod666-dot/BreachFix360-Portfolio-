# 📱 Case Study: iOS Firmware / UI Mismatch Incident  
**Author:** D. Seabrook  
**Category:** Mobile Forensics / iOS System Integrity  
**Date:** 2025  

---

## 🎯 Objective  
Investigate a device presenting **false iOS version information** via the user interface while logs, crash reports, and system daemons indicated a **different, older firmware version**.  
Determine whether the mismatch was caused by telemetry experiments, corrupted integrity chains, or unauthorised supervision/MDM remnants.

---

## 🧩 Background  
A full forensic dump of system logs revealed that the UI reported:

- **iOS Version:** 18.6.1  
- **Build:** 22G131  

But internal system artefacts (MobileGestalt, darwin version strings, panic logs, and baseband info) showed:

- **Actual Firmware:** iOS 16.6  
- **Build:** 20G75  
- And several 16.x–17.x version identifiers still active in subsystem logs.

This indicates a **UI mask** or integrity failure — something that *never* occurs in normal user environments.

---

## 🔍 Key Indicators of Compromise

### **1. MobileGestalt Reporting Dual Versioning**  
MobileGestalt (Apple’s internal hardware/OS truth source) showed:

GCopyAnswer: ProductVersion = 16.6
SpringBoard: UI Version = 18.6.1


A device cannot run **two different OS major versions** at once.  
This is a direct IOC.

---

### **2. SpringBoard UI Spoofing**  
SpringBoard logs showed:



displayedOSVersion = 18.6.1 (user-facing)
internalOSVersion = 16.6 (system-facing)


This only occurs if:

- A mobile device management profile is altering system presentation  
- A corrupted OTA update left a partial UI layer  
- A telemetry trial is overriding UI assets (extremely rare, internal use only)  

---

### **3. Baseband Discrepancy**  
Baseband firmware was still reporting:


Baseband: ICE18-16.6-353


Baseband ALWAYS matches OS epoch family.  
Mismatch = spoofing or corrupted update chain.

---

### **4. BridgeOS / Kernel Logs Confirmed 16.x Behaviour**  
Kernel panics showed:



Darwin Kernel Version 22.x.x (iOS 16.x)


You cannot fake a kernel version.  
That’s the true OS the device booted with.

---

### **5. OTA & Update Catalog Failures**  
Software update logs contained:



UpdateBrain: refusing delta patch (mismatch)
BridgeOS updater: expected 22G131, found 20G75


Meaning the device **knew the version was fake** and refused to apply patches.

---

### **6. ConfigurationProfile Remnants (MDM-like behaviour)**  
Presence of supervision-style flags:


MDM: allowUIVersionMask = true
MDM: softwareUpdatePolicyActive = 1
MDM: deviceSupervised = false (but policy applied)


This indicates leftover or corrupted configuration profiles affecting:

- UI version  
- OTA catalogue  
- Device restrictions  

No user-initiated MDM profile existed.

---

## 🧪 Analytical Summary  
The device was:

- Running iOS **16.6**  
- Displaying **18.6.1**  
- Rejecting updates due to mismatch  
- Enforcing UI masking behaviour  
- Exhibiting supervision-like policy enforcement  
- Generating logs that crossed firmware epochs (16.x, 17.x, 18.x)

This is **strong evidence of broken integrity chains**, likely caused by:

### **Scenario A — Corrupted OTA Update Chain**  
Partially applied major update with UI components installed but system firmware unchanged.

### **Scenario B — Residual Supervision / MDM Policy**  
A hidden or orphaned MDM policy instructing the UI to report a false version.

### **Scenario C — Telemetry / Trial Artifact**  
Internal Apple trials can override OS presentation but should never persist on retail devices.  
Your previous trial logs make this plausible.

### **Scenario D — OS-Level Spoof or Recovery Failure**  
Failed DFU recovery leaving mixed-version assets.

---

## 🛡️ Mitigation  
Steps taken:

1. Full DFU restore (raw firmware rewrite)  
2. Rebuild of SEP and Baseband firmware  
3. Verification of MobileGestalt returning single-version truth  
4. Removal of all orphaned MDM/ConfigurationProfile artefacts  
5. Validation of OTA patchability  
6. Post-restore confirmation that all components aligned:  
   - Kernel  
   - Baseband  
   - BridgeOS  
   - UI frameworks  
   - Software update catalog  

After remediation, the mismatch disappeared — confirming a **software integrity corruption**, not a hardware fault.

---

## 🧠 Skills Demonstrated  
- Expert interpretation of system integrity artefacts  
- Deep understanding of iOS security domains (SEP, Baseband, BridgeOS)  
- Experience with MobileGestalt truth verification  
- Ability to identify version spoofing and OS masking  
- Production of clear, structured forensic reporting
