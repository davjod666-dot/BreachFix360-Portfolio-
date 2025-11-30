Case Study 2: RunningBoard Telemetry & Process State Anomalies

Author: David Seabrook
Category: System Log Analysis / Process Behaviour
Date: 2025

🎯 Objective

Investigate anomalous RunningBoard (“RB”) events where process states, assertions, and background task lifecycles did not align with visible UI behaviour — indicating hidden subsystem activity, unexpected resource assertions, or concealed background processes.

🧩 Symptoms Observed

RunningBoard spawning or monitoring processes not visible in the UI

Repeated “assertion taken” events for apps not opened

Unexpected “jetsam pressure” and lifecycle warnings with no user interaction

Resource usage wake-ups during idle periods

Telemetry-style task exits firing even when system settings indicated tracking was disabled

🔍 Analysis Summary
1. RunningBoard Delivering Background Telemetry Events

RunningBoard generated multiple sequences such as:

Take assertion — reason: system task

Remove assertion — reason: no longer needed

Process state: suspended → running → suspended (with no user input)

This pattern is not normal for an idle, untouched system.

Indicates:

Backend telemetry hooks

System tasks waking processes without UI visibility

Potential masking of active components

2. Inconsistent Process Lifecycles

RB logs revealed:

Daemons reawakening despite energy-saving restrictions

Idle apps receiving “CPU wake” or “watchdog extension” calls

Hidden pushes to components associated with state syncing

This contradicts:

User-configured settings

Expected behaviour for suspended apps

Normal mobile OS throttling

3. Effects and Risk

Hidden processes can impact battery, heat, and system integrity

Loss of transparency over which processes actually run

Indicators of manipulation if RB is forced to hide real process state

Suggests deeper telemetry, inference, or concealed OS components operating

🛠 Mitigation & Hardening

Cross-correlate RB events with system daemons (e.g., networkd, locationd)

Disable unnecessary background refresh

Full sysdiagnose review for mismatched lifecycle events

Rebuild OS if RB assertions show non-user-driven wakes

Check for persistent entitlements bypassing UI controls

✔️ Status

Completed and validated.
Part of the core BreachFix360 DFIR set for process-level behavioural anomalies.
