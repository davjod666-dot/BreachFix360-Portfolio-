# 🧵 Case Study: RunningBoard & Telemetry Process Anomalies  
**Author:** D. Seabrook  
**Category:** System Log Analysis / Process Forensics  
**Date:** 2025  

---

## 🎯 Objective  
Investigate unexpected system-level processes related to Apple’s RunningBoard, Siri inference engines, and Cloud Telemetry services to determine whether the device was influenced by remote policy, profiling frameworks, or unauthorised supervision-level behaviour.

---

## 🧩 Background  
During live log capture and sysdiagnose sessions, multiple subsystems were observed that:

- Launched without user interaction  
- Persisted despite disabled permissions  
- Executed inference and telemetry tasks with “optedIn: false”  
- Contained trial or experiment identifiers not normally exposed on consumer devices  

These behaviours indicate **device-level orchestration beyond normal iOS activity**, potentially enforced via hidden MDM, remote configuration, or leftover trial/telemetry states.

---

## 🔍 Key Symptoms  

### **1. RunningBoard Activity**  
RunningBoard is Apple’s internal process/power assertion manager.  
Observed anomalies included:

- Repeated wake events with no foreground apps  
- Unexpected “assertion renewal” cycles  
- Background tasks attributed to Siri inference and CloudTelemetry  
- High-frequency process spawning without UI trigger  

Example log:  
runningboardd: Acquiring assertion for siriinferenced (power, cpu)
runningboardd: Renewing assertion: <RBAssertion identifier=com.apple.siri.inference>

---

### **2. Siri Inference Engines**  
Even with Siri disabled, multiple inference subsystems executed:

- `siriinferenced`  
- `siriactionsd`  
- `CloudKnowledgeGraph`  

Observed behaviours:

- Queries firing with device locked  
- Inference tasks running while user opt-in was false  
- Frameworks attempting to load unavailable model versions  

Example:  
siriinferenced: optedIn = false but inference_session spawned
siriactionsd: modelVersion mismatch; retrying load

This indicates **background model evaluation attempts** usually linked to:

- User profiling  
- Behavioural prediction  
- Automated system decisioning  

---

### **3. CloudTelemetryService**  

This is the heavy hitter.  
CloudTelemetry is normally opt-in, limited, and controlled.

Your logs showed:

- CloudTelemetry tasks launching without consent  
- Remote configuration pulls  
- Full telemetry harvest cycles while “optedIn:false” was active  
- Network wake events tied to telemetry batches  

Example:  
CloudTelemetryService: starting batch harvest
CloudTelemetryService: userOptIn = false, override = true

The **override flag** alone is an IOC.

---

### **4. triald / Experiment Frameworks**  
Independent trial systems executed:

- Feature gating  
- Experiment rollouts  
- Namespace compatibility checks  
- Behaviour mapping  

Examples:  
triald: applying namespace: siri/actions/v3
triald: running compatibility version mapping

When combined with blocked permissions and mismatched OS versioning, this strongly suggests **ghost trial enrolment** or remote policy.

---

## 🧪 Evidence Summary

### **A. Process Persistence**
- Telemetry and inference processes kept respawning  
- RunningBoard maintained power assertions to keep them alive  

### **B. Permission Bypass Indicators**
- Subsystems running with user disabled (Siri, analytics, telemetry)  
- “Opt-out” values ignored  

### **C. Behavioural Consistency with Remote Policy**
- Wake events  
- GPU/CPU bursts  
- Network polling tied to telemetry tasks  
- Activity unrelated to installed apps  

### **D. Version / Model Mismatch**
- Siri models referencing incorrect iOS version  
- triald pulling incompatible namespaces  

These are textbook indicators of **supervision remnants, hidden config profiles, or unauthorised telemetry frameworks**.

---

## 🧠 Analyst Interpretation  

### **Scenario 1 — Hidden MDM or Supervision**  
MDM can enforce telemetry despite opt-out.  
The patterns match profile-enforced execution.

### **Scenario 2 — Residual Experiment Enrollment**  
Apple uses internal rollout frameworks; your device showed indicators of being incorrectly enrolled without consent.

### **Scenario 3 — Telemetry Override Behaviour**  
CloudTelemetry overriding opt-out suggests remote enforcement.

### **Scenario 4 — Compromised System Policy Store**  
Policy files may have been tampered with or corrupted.

---

## 🛡️ Mitigation & Hardening  

- DFU restore (performed successfully)  
- Validate system policy folders (`/var/db/ConfigurationProfiles` etc.)  
- Revoke all analytics and Siri services  
- Disable Siri, Search, Suggestions  
- Block telemetry endpoints via network until trust baseline re-established  
- Review Apple ID logs for remote configuration triggers  

---

## 🧾 Outcome  
Post-DFU behaviour normalised, and inference/telemetry processes ceased spawning.  
This strongly supports the conclusion that:

**The device was running enforced or orphaned system policies outside normal user control**, likely related to remote supervision, telemetry overrides, or residual experiment enrolment.

---

## 🧠 Skills Demonstrated  
- Advanced iOS process forensics  
- RunningBoard / PowerAssertion analysis  
- Telemetry and inference framework interpretation  
- Identification of policy enforcement patterns  
- Log-driven triage and reporting  
