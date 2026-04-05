## Endpoint Investigation: Living-off-the-Land Attack (Sysmon)

### Objective
To analyze endpoint telemetry using Sysmon logs to identify suspicious process activity and potential malicious behavior.

---

### Data Source
Sysmon EventCode 1 (Process Creation logs)

### Dataset

The dataset used in this investigation contains simulated Sysmon process creation logs designed to reflect realistic endpoint activity, including both normal and malicious behavior.


---

### Scenario
A workstation generated alerts indicating suspicious command execution. Sysmon logs were analyzed to determine whether malicious activity occurred.

---

### Investigation Process
Sysmon logs were reviewed to identify abnormal process execution, command-line usage, and parent-child relationships.

---

### Key Findings

- Repeated execution of PowerShell commands using `Invoke-WebRequest`
- External connection to `http://malicious-site.com`
- Download of an executable file (`payload.exe`)
- PowerShell processes spawned by `cmd.exe`, indicating suspicious process chaining

---

### Analysis

The observed behavior suggests the use of PowerShell as a Living-off-the-Land Binary (LOLBins) to download a malicious payload. The use of `Invoke-WebRequest` to retrieve an executable file from an external domain is a strong indicator of compromise.

The parent-child relationship of `cmd.exe` spawning PowerShell indicates potential script-based execution, commonly seen in attacker activity.

---

### Impact

If successful, the downloaded payload could result in malware execution, system compromise, or further lateral movement within the environment.

---

### Severity

High

---

### MITRE ATT&CK Mapping

- T1059.001 – PowerShell
- T1105 – Ingress Tool Transfer

---

### Recommended Actions

- Block outbound connections to suspicious domains
- Investigate affected host for malware
- Restrict PowerShell usage and enforce execution policies
- Monitor for similar command-line activity
