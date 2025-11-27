📌 Portfolio Highlights — BreachFix360 Digital Forensics Portfolio

Curated investigations, case studies, and hands-on technical analysis by David Seabrook.

⸻

🚀 1. Telstra Network Case — Behaviour & Anomaly Investigation

Category: Network Analysis / Home Network
Tools: Wireshark • Router CLI • Log Triage • Threat Hunting
Key Skills Demonstrated: Firewall triage, packet flow reconstruction, WAN anomaly detection

🔍 Summary

Investigated abnormal home network behaviour including RTNETLINK messages, fluctuating conntrack entries, and unexpected multicast events.
Findings showed misconfigurations, instability in the consumer router, and malformed traffic bursts.

🧩 Evidence Included
	•	WAN event logs
	•	STUN connectivity checks
	•	Port 443 loopback anomalies
	•	MAC fluctuation tracking
	•	Wi-Fi abnormal beacon patterns

🎯 Outcome

Identified root causes, ruled out external footholds, and documented remediation steps.

⸻

🚨 2. iOS Firmware/UI Mismatch Forensic Case

Category: Mobile Forensics / iOS Security
Tools: iOS Logs • Analytics Engine • Build Number Verification
Key Skills Demonstrated: Mobile forensics, triage, chain-of-trust validation

🔍 Summary

Detected a critical mismatch between reported UI firmware (iOS 18.x) and actual build-level firmware (16.x) on the device. This type of discrepancy is a strong indicator of spoofing, failed updates, UI misreporting, or forced-update glitching.

🧩 Evidence Included
	•	iOS build manifest logs
	•	Software update analytics
	•	Security policy checks (MDM supervision indicators)
	•	Connected domain behaviour
	•	System version cross-checks

🎯 Outcome

Documented full triage, confirmed mismatch origin, and mapped likely update corruption causes.

⸻

🧠 3. System Log Analysis Case Group

Category: Multi-System Forensics
Tools: RunningBoard • Skywalk • NetIf • iOS/macOS System Logs
Key Skills Demonstrated: Cross-OS correlation, anomaly detection, process-level analysis

🔍 Summary

Deep-dive correlation of multiple logs from macOS, iOS, and network devices. Focus on background processes, event-based anomalies, and unusual telemetry patterns.

📌 Cases Included
	•	iOS Firmware/UI Mismatch Timeline
	•	macOS RunningBoard anomalies
	•	transparency.log review
	•	Router STUN/multicast correlation
	•	Cross-device forensic mapping

🧩 Evidence Included
	•	Process trees
	•	Launchd behaviour
	•	iOS AWDL activity
	•	Network extension events
	•	Telemetry deltas across systems

⸻

🧬 4. AWDL Wi-Fi Analysis

Category: Wireless Forensics
Tools: Wireshark • Frame Capture • AWDL Inspector
Key Skills Demonstrated: Wireless protocol analysis, 802.11 frame interpretation

🔍 Summary

Captured and analysed Apple Wireless Direct Link (AWDL) behaviour — the Bluetooth/Wi-Fi hybrid used for AirDrop, Continuity, and peer-to-peer operations.

🧩 Evidence Included
	•	AWDL channel hopping
	•	Synchronisation frames
	•	Device discovery traffic
	•	Multicast behaviour
	•	Peer negotiation bursts

🎯 Outcome

Confirmed benign AWDL activity consistent with Apple peer-to-peer services.

⸻

🌐 5. Port 443 Loopback Case

Category: Network Analysis / Localhost Forensics
Tools: Wireshark • Router Logs • Localhost Tracking

🔍 Summary

Observed repeated 443 loopback calls and malformed TLS initiation patterns.
Investigated potential misroutes, update services, or local software agents.

🧩 Evidence Included
	•	TLS handshake attempts
	•	Localhost loopback logs
	•	Process-correlation table
	•	Router event parity

🎯 Outcome

Likely benign system process misrouting combined with connection retries — documented cleanly and verified.

⸻

📡 6. STUN Multicast Event Analysis

Category: VoIP / NAT / Router Behaviour
Tools: Router logs • UDP packet analysis

🔍 Summary

Captured unexpected STUN behaviour (UDP 3478) which often appears during NAT discovery or VoIP platform negotiations.

🎯 Outcome

Determined STUN traffic was triggered by network instability and consumer-grade router design rather than external misuse.

⸻

🧰 7. RunningBoard / Background Task Forensics

Category: macOS & iOS Process Analysis
Tools: RunningBoard logs • taskinfo dumps • transparency.log

🔍 Summary

Investigated background task scheduling, system watchdog behaviour, and process snapshots across macOS and iOS.

🧩 Key Artifacts
	•	RunningBoard delta logs
	•	Process state transitions
	•	Power assertion anomalies
	•	Network task scheduling

⸻

🏁 Summary Snapshot (Recruiter-Friendly)

Skills Demonstrated Across Portfolio:
	•	🔐 Mobile & desktop forensic analysis
	•	📡 Network behaviour investigation (WAN/LAN/Wi-Fi)
	•	🧪 Log triage & anomaly detection
	•	🛠️ Router + OS-level troubleshooting
	•	🔍 Protocol analysis (AWDL, STUN, TLS, multicast)
	•	📊 Documentation and reporting for blue team/IR environments

Perfect for roles in:
	•	Cybersecurity Analyst (Blue Team)
	•	SOC Level 1–2
	•	Digital Forensics & Incident Response (DFIR)
	•	Threat Hunting Junior
	•	Network Security Operations
