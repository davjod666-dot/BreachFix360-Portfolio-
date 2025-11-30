Case Study 8: Full Device Correlation Matrix – UI Masking vs Backend System State

Author: David Seabrook
Category: Multi-Subsystem Forensics / OS Behaviour Correlation
Date: 2025

🎯 Objective

Produce a complete end-to-end forensic correlation that compares:

1. What the device told the user in the UI

“Everything is fine 👍 no issues here sir.”

2. What was actually happening in the backend logs

RunningBoard wakes, hidden tunnels, AWDL chatter, STUN bursts, FlowSwitch overrides, unacknowledged telemetry pushes, policy hijacks, and state-masking patterns.

This case demonstrates your ability to:

Correlate separate subsystems

Identify cross-framework inconsistencies

Interpret OS behaviour beyond the user interface

Detect concealed routing, telemetry, and background activity

Document multi-layer anomalies in a SOC-ready format

🧩 Summary of Anomalies Across All Layers

This case merges all previous findings into one unified picture.

Below is your Device State Correlation Matrix, comparing UI claims vs backend evidence.

🔐 1. UI Network State vs Backend Activity
UI Says	Backend Logs Show
“Wi-Fi off”	AWDL interface waking and announcing presence
“Airplane Mode”	STUN packets testing NAT traversal
“No VPN installed”	Skywalk tunnels + FlowSwitch routing
“Idle”	RunningBoard waking processes, CPU bursts
“No apps running”	Background daemons performing work

Interpretation:
UI state did not reflect actual network subsystem behaviour.

🧩 2. UI App State vs RunningBoard Lifecycle
UI Says	RunningBoard Shows
App closed	“assertion taken” → app forced awake
Background refresh off	“preventIdleSleep” assertions
Low power mode	“keepalive extension extended”
No Siri activity	siriinferenced + siriactionsd tasks awakened
Device asleep	processes entering → exiting → re-entering “running” state

Meaning:
Backend processes were operational even when UI implied shutdown.

🌐 3. UI Privacy Settings vs NetworkExtension & Skywalk
UI Says	NetworkExtension/Skywalk Shows
No VPN	NEXUS tunnels, rebind events, flowspec attachments
No sharing	ALEClient & discovery sockets waking
No background tasks	FlowSwitch enforcing routing policies
No permissions granted	Interface rewrites + dynamic tunnel activation

Meaning:
Background routing + policy engines operated independently of user settings.

📡 4. UI Location / Bluetooth / Discovery vs AWDL & Multicast
UI Says	Logs Show
AirDrop off	awdl0 beacon frames & discovery traffic
Bluetooth off	LE scanning windows triggered
Local Network off	mDNS joining multicast groups
Device locked	IPv6 solicitations + service discovery bursts

Meaning:
Discovery frameworks operated despite explicit user restrictions.

🧠 5. Inference / Telemetry Signals

UI provides:

No indication of ML inference

No notice of trial frameworks

No notice of data collection tasks

Backend shows:

siriinferenced

CloudTelemetryService

triald namespace activity

asset vending / UnifiedAssetFramework pulls

background “metadata layering” tasks

This is classic telemetry-without-UI-representation behaviour.

Not malicious.
But absolutely not transparent.

💡 Cross-Subsystem Correlation (The Signature of This Case)

When all findings are correlated:

A hidden operational layer existed beneath UI controls, comprising:

Wireless discovery

NAT traversal

Routing enforcement

Process lifecycle overrides

Inference/telemetry tasks

Network extension tunnels

All firing in concert, not accidentally.

This is what makes this case a SOC-level capstone.

🧩 Root Cause Possibilities

Based on correlations:

Apple Telemetry / Trial Subsystems
(Bifrost, Siri inference, UAF vending, triald namespaces)

Residual enterprise/MDM supervision

Corrupted OS state / misaligned frameworks

Persistence in network-extension space

Actor activity (low likelihood post-DFU, but logs resemble supervised behaviour)

This case does not assert malicious compromise.
But it proves non-transparent subsystem behaviour — fully valid in a DFIR portfolio.

🛠 Mitigation & Validation

DFU restore ✔️

Inspect early-boot next time (before Apple ID login)

Validate fresh device vs previous baselines

Confirm no hidden profiles

Compare Skywalk + FlowSwitch behaviour on new hardware

Router-side monitoring for STUN/AWDL during idle periods

🎓 Professional Value

This case demonstrates:

Multi-subsystem log correlation

Clear SOC write-up structure

Ability to identify inconsistent OS layers

Strong forensic reasoning

High-value investigative instinct
