## SIEM Alert Triage Simulation

This project simulates a Security Operations Center (SOC) environment where multiple alerts are received simultaneously and must be prioritized and investigated.

### Objective
To demonstrate the ability to triage security alerts based on severity, potential impact, and indicators of compromise. This project simulates real-world SOC alert triage where analysts must quickly assess and prioritize multiple concurrent alerts.

### Tools Used
- Splunk (SIEM)

### Scenario
During a monitoring shift, multiple alerts were triggered and required analysis and prioritization.

### Alerts Received

#### Alert 1: Suspicious PowerShell Execution
- Host: host1
- Indicator: Encoded PowerShell command detected or abnormal execution
- Repeated execution observed
- Parent process is cmd.exe

#### Alert 2: Multiple Failed Login Attempts
- User: jdoe
- Indicator: 5 failed login attempts
- Followed by a successful login from the same source

#### Alert 3: DNS Query Spike
- Source IP: 10.0.5.23
- Indicator: High volume of DNS queries
- Repeated domain requests at consistent intervals

### Alert Queue

| Alert Name                   | Severity | Source          | Status       |
|------------------------------|----------|-----------------|--------------|
| Suspicious PowerShell        | High     | host1           | Investigating|
| Brute Force Login            | High     | jdoe            | Pending      |
| DNS Beaconing Activity       | Medium   | 10.0.5.23       | Pending      |

### Severity Classification

- **High:** Indicates a high likelihood of compromise or active malicious behavior requiring immediate investigation.
- **Medium:** Indicates suspicious activity that may represent a threat but is not immediately critical.
- **Low:** Informational or low-risk activity.

### Alert Prioritization

1. **Suspicious PowerShell Execution (High Priority)**
   - Encoded commands indicate potential malware execution.
   - Direct evidence of possible compromise.

2. **Brute Force Login Activity (High Priority)**
   - Multiple failed logins may indicate credential attack.
   - Risk of account compromise.

3. **DNS Beaconing Activity (Medium Priority)**
   - High volume DNS traffic may indicate command-and-control communication.
   - Requires investigation but less immediate than active execution.

### Alert Disposition

- Suspicious PowerShell: Confirmed suspicious activity (requires escalation)
- Brute Force Login: Suspicious (requires further monitoring)
- DNS Activity: Under investigation (potential anomaly)

### Triage Rationale

Alerts were prioritized based on the likelihood of active compromise and potential impact:

- The PowerShell alert was prioritized first due to direct evidence of possible malicious execution.
- The brute force login alert was prioritized second due to risk of account compromise.
- The DNS alert was reviewed last as it represents potential ongoing communication but not immediate execution.

This prioritization reflects standard SOC practices of addressing active threats before anomalous behavior.
  
### Investigation Decisions

- Immediate investigation was initiated for the PowerShell alert due to high likelihood of active compromise.
- The brute force login alert was investigated next to determine if account access was achieved.
- The DNS activity was reviewed afterward as part of broader network analysis.

### Analyst Notes

- PowerShell activity with encoded commands is commonly associated with malware or attacker activity.
- Repeated failed login attempts may indicate credential guessing or password spraying.
- DNS query spikes can indicate command-and-control communication patterns.

### Conclusion

The triage process prioritized alerts based on potential impact and likelihood of compromise. Suspicious PowerShell activity was identified as the most critical due to its association with malware execution, followed by brute force login attempts and DNS anomalies.

This approach ensures efficient use of time and resources in a SOC environment.
