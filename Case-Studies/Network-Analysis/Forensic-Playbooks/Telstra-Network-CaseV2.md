📘 Case Study: Telstra Network Behaviour & QoS Anomaly Investigation

Author: David Seabrook
Category: Network Analysis / Home Network / Forensics
Date: November 2025
Tools Used: Wireshark, Cobra Router Logs, BBLOAT, macOS netstat, tcpdump

⸻

🎯 Objective

Determine whether anomalous router behaviour (RTNETLINK messages, conntrack fluctuations, QoS bufferbloat spikes, and MAC inconsistencies) indicated an external intrusion or internal misconfiguration.

⸻

🧩 Symptoms Observed
	•	Repeated RTNETLINK and kernel: nf_conntrack log entries
	•	Conntrack table counts fluctuating rapidly
	•	QoS bufferbloat warnings during stress tests
	•	One mismatched Wi-Fi MAC address observed briefly
	•	Perceived latency spikes and inconsistent throughput
	•	STUN and multicast traffic surfacing in packet captures
	•	Unresolved hostname/DNS delays
	•	Router intermittently failing to resolve internal services

⸻

🗂️ Evidence Collected

1. Raw Router Logs (Annotated)

🔸 RTNETLINK & Conntrack Events

daemon.info kernel: [NF_CONNTRACK] table full, dropping packet
daemon.info net_ratelimit: RTNETLINK answers: Network is down
daemon.notice kernel: RTNETLINK: file exists

Interpretation:
	•	RTNETLINK messages typically surface during interface resets or WAN link renegotiation.
	•	Conntrack table saturation is common on consumer ISP routers during heavy local scanning, streaming, or NAT bursts — not by itself a sign of compromise.

2. Wi-Fi MAC Mismatch Event

[Wireless] STA MAC changed 3A:4B:22:AC:XX:XX → 3A:4B:22:AC:YY:YY

Interpretation:
	•	This pattern matches Apple Wi-Fi randomisation, especially during:
	•	roaming
	•	interface sleep/wake
	•	AWDL negotiation
	•	hotspot/continuity transitions

Nothing indicates impersonation or rogue AP behaviour.

3. BBLOAT / Latency Results

Upload: 31ms → 495ms under load  
Download: 25ms → 380ms under load  
Bufferbloat: Grade C/D  

Interpretation:
	•	Clear QoS saturation event.
	•	Typical on Telstra Cobra/DumaOS units with high LAN chatter or when WAN link renegotiates.
	•	Not an attacker behaviour.

4. Netstat / System Network Snapshot

udp4       0      0  *.mdns
udp4       0      0  *.netbios-ns
udp4       0      0  *.netbios-dgm
udp4       0      0  *.60663
udp4       0      0  *.5353
tcp46      0      0 127.0.0.1:8118       LISTEN   (privoxy)

Interpretation:
	•	mdns / netbios traffic: normal LAN discovery
	•	port 5353: Apple multicast DNS (normal)
	•	127.0.0.1 listeners: safe (local proxy, system services)
	•	No established foreign connections or suspicious ports

5. Packet Capture Highlights

STUN binding requests: <192.168.0.12 → stun.l.google.com>
Multicast: ff02::fb (mDNS)
ARP refresh: Who-has 192.168.0.1?

Interpretation:
	•	All legitimate, expected LAN/Wi-Fi operations.
	•	No C2 traffic, no tunnelling, no suspicious repeated SYN/ACK patterns.

🧵 Timeline Reconstruction
	•	14:22 – WAN link renegotiates following local congestion
	•	14:23 – RTNETLINK + conntrack warnings triggered
	•	14:25 – Bufferbloat test started → QoS overwhelmed
	•	14:30 – Wi-Fi MAC randomisation event captured
	•	14:33 – DNS delays observed (router clock drift)
	•	14:45 – Router time provider switched → issue resolved

⸻

🩻 Root Cause Determination

The abnormalities were not indicators of compromise.

They stemmed from a combination of:
	•	Normal NAT churn on a Telstra Cobra router
	•	Bufferbloat during load
	•	Wi-Fi MAC randomisation by Apple devices
	•	Router time drift causing DNS delay
	•	ISP equipment behaviour during peak conditions

No evidence of:
	•	External attacker presence
	•	Rogue DHCP
	•	MiTM
	•	Remote access or tunnelling
	•	Persistent implants
	•	Port redirection or NAT hijack

⸻

🛡️ Defensive Recommendations
	•	Enable QoS with conservative upload/downlink limits
	•	Set router time provider manually (Telstra’s is flaky)
	•	Disable UPnP unless required
	•	Update router firmware when available
	•	Use isolated IoT network if possible
	•	Run periodic BBLOAT/AUDIT tests

⸻

🏁 Outcome

After adjusting the router’s time provider and rebooting the WAN interface, all symptoms ceased.
QoS returned to normal, NAT/conntrack stopped flooding, and Wi-Fi MAC behaviour was confirmed legitimate.

This case demonstrates strong network triage, log interpretation, and the ability to separate noise from real security events — crucial Blue Team skill.
