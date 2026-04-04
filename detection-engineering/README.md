## Detection Engineering Project

This project demonstrates how detection logic can be developed in Splunk to identify malicious behavior across network, authentication, and endpoint activity.

### Objective
To design and implement detection rules capable of identifying common attack patterns such as command-and-control beaconing, brute force login attempts, and suspicious PowerShell execution. These detections are designed to simulate real-world SOC alerting scenarios.

### Tools Used
- Splunk (SIEM)

### What is Detection Engineering?
Detection engineering involves creating rules and logic that identify suspicious or malicious activity within logs. These rules are used by SIEM platforms to generate alerts for security analysts.

### Detection Rules
The following detection rules were developed based on previously analyzed attack scenarios.

### Detection Rule 1: Encoded PowerShell Execution

#### Description
Detects PowerShell processes executing encoded commands, a technique commonly used by attackers to obfuscate malicious scripts.

#### Severity
High

#### Detection Logic

`index=main process_name=powershell.exe command_line="*-enc*"`

This query returns events that match the defined suspicious pattern.

#### Rationale

The use of the -enc flag indicates encoded command execution, which is frequently associated with malicious activity. This detection rule identifies potential abuse of PowerShell for malware execution.

#### Related Technique

MITRE ATT&CK: T1059.001 (PowerShell)

#### False Positives 

Legitimate administrative or automated activity may trigger this detection and should be reviewed.


### Detection Rule 2: Brute Force Login Activity

#### Description
Detects multiple failed login attempts followed by a successful authentication, which may indicate a brute-force attack or credential compromise.

#### Severity
High

#### Detection Logic

`index=main status=FAIL OR status=SUCCESS
| stats count(eval(status="FAIL")) as failed_attempts, count(eval(status="SUCCESS")) as successful_attempts by username
| where failed_attempts > 3 AND successful_attempts > 0`

This query returns events that match the defined suspicious pattern.

#### Rationale

A high number of failed login attempts followed by a successful login is a strong indicator of brute-force or password spraying activity. This pattern suggests that an attacker may have successfully guessed valid credentials after multiple attempts.

#### Related Technique

MITRE ATT&CK: T1110 (Brute Force)

#### False Positives 

Legitimate administrative or automated activity may trigger this detection and should be reviewed.


### Detection Rule 3: DNS Beaconing Activity

#### Description
Detects repeated DNS queries from a single host to the same domain, which may indicate command-and-control (C2) beaconing behavior.

#### Severity
Medium or High if consisent interval is implied.

#### Detection Logic

`index=main
| stats count by src_ip, query
| where count > 10
| sort -count`

This query returns events that match the defined suspicious pattern.

#### Rationale

A high volume of DNS queries from a single source to the same domain may indicate automated beaconing activity. Malware often uses DNS to communicate with command-and-control infrastructure at regular intervals.

#### Related Technique

MITRE ATT&CK: T1071.004 (Application Layer Protocol: DNS)

#### False Positives 

Legitimate administrative or automated activity may trigger this detection and should be reviewed.

### Alert Implementation

These detection rules can be operationalized in Splunk by configuring them as scheduled alerts. Alerts can be triggered based on defined thresholds and integrated with incident response workflows.


