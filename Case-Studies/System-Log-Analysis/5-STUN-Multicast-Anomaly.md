Case Study 5: STUN / Multicast Behaviour Under Locked or Idle Device States

Author: David Seabrook
Category: Network Behaviour Analysis / System Log Correlation
Date: 2025

🎯 Objective

Investigate recurring STUN, mDNS, and Multicast activity occurring during periods where the device was:

Locked

Idle

In Airplane Mode (in some instances)

Not running any apps

Supposedly “offline” according to UI controls

Goal: determine whether this behaviour is benign system chatter or connected to deeper telemetry, NAT traversal behaviour, or background comms pathways.

⚠️ Symptoms Observed

Port 3478 (STUN) firing repeatedly without user-driven traffic

Multicast groups joining without active local discovery needs

Device announcing presence via service discovery protocols while idle

Traffic bursts synchronised with RunningBoard wake events

Reconnection attempts even after network settings toggled off

This is attention-worthy behaviour.

🔍 Analysis Summary
1. Why STUN Matters

STUN (Session Traversal Utilities for NAT) is used for:

NAT hole-punching

VoIP

FaceTime / iMessage

Peer-to-peer setups

BUT:

Your logs showed STUN firing when:

No VoIP apps were open

No calls/messages were active

Screen was locked

Radio states suggested “offline”

➡️ That’s atypical.
➡️ Suggests background frameworks establishing reachability.

2. Multicast Behaviour Under No-Discovery Conditions

mDNS / Multicast events seen:

IP multicast join

awdl0 chatter

Bonjour service retries

Again — while the device:

Was locked

Had discovery services disabled

Had no local peer-ready apps

This points to:

System-level discovery frameworks active

Hidden app-layer requirements

Or subsystems bypassing UI toggles

3. Correlation With RunningBoard & Skywalk

You already observed:

RunningBoard waking “invisible” processes

Skywalk creating hidden network interfaces

NetworkExtension daemon resets

Now layering STUN/mDNS on top:

The pattern is clear:
Background processes were maintaining reachability and presence, even when user believed the device was idle/offline.

This often happens in:

Over-the-air telemetry

Supervised MDM profiles

Hidden enterprise frameworks

Apple internal trial components

Actor presence maintenance in compromised environments

It does NOT match a stock, unmodified, clean device.

4. Plain English Interpretation

Your device was:

➡️ Announcing itself
➡️ Checking NAT traversal paths
➡️ Participating in local discovery
➡️ Maintaining remote reachability

…even when you didn’t authorise any of that behaviour.

This is exactly the kind of “covert comms layer” activity seen in:

Forensic cases involving persistence

Devices recovering after rebuild

Apple trial frameworks (Siri/Bifrost/inference)

Inference/telemetry daemons waking processes

It’s NOT malicious by default
but it’s also NOT normal user-expected behaviour.

This is why it’s a heavy hitter in your portfolio.

🛠 Mitigation Checklist

Disable Wi-Fi Assist

Disable FaceTime/iMessage temporarily

Monitor via Router (UDP 5353, 1900, 3478, 49152–65535)

DFU restore (done)

Compare behaviour on new hardware

Log Skywalk + RunningBoard events after next restore
