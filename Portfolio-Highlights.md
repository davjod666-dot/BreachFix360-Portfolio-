📌 Portfolio Highlights — BreachFix360 (D. Seabrook)

Early-career SOC Analyst • Digital Forensics • Network Defence • Incident Response

🔎 Summary

I’m an emerging SOC analyst with a background in emergency services, risk management, and front-line decision-making.
Rather than spend months reading theory before touching real tools, I’ve taken a hands-on-first approach — building, breaking, analysing and documenting real systems.

This portfolio contains practical case studies based on actual log files, packet captures, router events, system behaviours, and forensic workflows I have analysed.

Everything here is written the way a SOC analyst thinks:
evidence → timeline → hypothesis → verification → conclusion.

📁 Portfolio Contents
🗂️ 1. System Log Analysis — Case Studies

Deep-dive investigations correlating iOS/macOS logs, network behaviour, and system processes.
Each case demonstrates detection logic, triage approach, and structured reasoning.

Case 1 — iOS TCC Events & Permission Mapping
Tracks system permission calls, TCC prompts, and process behaviour.

Case 2 — AWDL & Peer Services Analysis
Identifies legitimate vs suspicious AWDL/Wi-Fi Direct traffic — a common false-positive area.

Case 3 — NAT / STUN Bursts & Multicast Traffic
A breakdown of STUN, NAT rebinding misconceptions, and how to recognise benign vs malicious patterns.

Case 4 — RunningBoard & Background Task Behaviour
Shows how macOS manages power, CPU cycles, assertions and why this often gets mistaken for compromise.

Case 5 — Lockdown Mode vs Standard iOS Hardening
Compares behavioural differences and helps identify when iOS is simply enforcing stricter rules.

Case 6 — NetworkExtension & UUID Cache Interpretation
Analyses tunnels, VPN extents, flows, and explains what’s normal in Apple’s NE subsystem.

Case 7 — Full Correlation: UI vs Backend Logs
End-to-end case correlating:

what the device displayed

what the system actually did
Perfect for demonstrating SOC triage logic.

🗂️ 2. Network Analysis — Case Studies

Real-world packet captures and router logs analysed using Wireshark and DumaOS/Telstra modem logs.

Case 1 — Telstra Router (Cobra/DumaOS) Log Review
Includes traceroutes, conntrack events, BBLOAT tests, QoS analysis, NAT reflections, and MAC movement.
A strong showcase of network fundamentals and practical triage.

🗂️ 3. Forensic Playbooks

Step-by-step playbooks I built while learning to triage logs and system events:

AWDL Analysis Playbook

NAT / STUN Triage Playbook

System Log Correlation Playbook

iOS/macOS Hardening Notes

Network Triage Quick Reference

🗂️ 4. SOC-Ready Documents

Professional SOC/IR CV (D. Seabrook)

Portfolio Highlights (this file)

README.md — repo overview + roadmap

🎯 Why This Portfolio Matters

I’m early in my cyber journey — but I bring:

real world emergency-service decision making

high-pressure triage experience

procedural discipline

a “learn fast / hands on, curious” mindset

and genuine curiosity for how systems break and behave

Every case in this repo shows my capability to:

✅ interpret noisy logs
✅ recognise false positives
✅ think like a defender
✅ document clearly
✅ correlate multi-source evidence
✅ explain complex things simply

Exactly what a SOC analyst needs.

🚧 Roadmap (In Progress)

CS50X Harvard's Introduction to Cybersecurity - Completed November 2025
Security Blue Team Junior Analyst - In Progress
Linux Foundation Introduction to Linux - In Progress

Short-Term

Add packet capture walkthroughs (PCAP → findings → summary)

Add Linux hardening notes

Add detection rules for common noise patterns (STUN, AWDL, NE, etc.)

Long-Term

Build a small home SOC lab

SIEM parsing simulations (Elastic / Wazuh / LimaCharlie)

IR playbook expansions

Threat-hunting exercises

👤 Author

David Seabrook
Emerging SOC Analyst — BreachFix360
Newcastle NSW, Australia
