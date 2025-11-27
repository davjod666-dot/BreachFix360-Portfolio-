# 🔐 Case Study: Suspicious Port 443 Loopback Activity

**Author:** David Seabrook  
**Category:** Network Analysis / TLS Behaviour  
**Date:** 2025  

---

## 🎯 Objective
Investigate repetitive loopback (127.0.0.1) traffic over port 443 and determine whether it is legitimate application behaviour or indicative of localhost interception.

---

## 🧪 Observed Behaviour
- Repeated `tcp4 127.0.0.1:443 → *` listener behaviour  
- System processes using TLS-like connections locally  
- Netstat showing persistent 443 binds without corresponding user applications  
- Instances where self-signed certs appeared in TLS handshake logs  

---

## 🧩 Key Findings

### 🔹 Localhost TLS Tunnels
Several macOS services create secure local tunnels:
- `systemstats`  
- `nsurlsessiond`  
- Cloud-related daemons  

This can appear suspicious but is **not inherently malicious**.

### 🔹 Self-Signed Certificates
Self-signed certs observed were:
- Machine-generated  
- Internal  
- Used for local IPC (inter-process communication)

### 🔹 When It *Would* Be Suspicious
- Proxy/MDM interception tools  
- Browser hijackers  
- Localhost MITM tunnels  
- Developer test servers hidden in apps  

No such indicators were found.

---

## 🛡️ Mitigation
- Full malware scan  
- Validate root certificate trust store  
- Confirm SIP and TCC integrity on macOS  
- Review LaunchDaemons for unknown processes  

---

## 📌 Outcome
Loopback 443 traffic was determined to be **safe system behaviour**.

However, combined with other anomalies, it should always be logged and baselined when investigating advanced compromise.
