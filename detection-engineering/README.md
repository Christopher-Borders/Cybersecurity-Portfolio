## Detection Engineering Project

This project demonstrates how detection logic can be developed in Splunk to identify malicious behavior across network, authentication, and endpoint activity.

### Objective
To design and implement detection rules capable of identifying common attack patterns such as command-and-control beaconing, brute force login attempts, and suspicious PowerShell execution.

### Tools Used
- Splunk (SIEM)

### What is Detection Engineering?
Detection engineering involves creating rules and logic that identify suspicious or malicious activity within logs. These rules are used by SIEM platforms to generate alerts for security analysts.

### Detection Rules
The following detection rules were developed based on previously analyzed attack scenarios.

### Detection Rule 1: Encoded PowerShell Execution

#### Description
Detects PowerShell processes executing encoded commands, a technique commonly used by attackers to obfuscate malicious scripts.

#### Detection Logic

`index=main process_name=powershell.exe command_line="*-enc*"`

#### Rationale

The use of the -enc flag indicates encoded command execution, which is frequently associated with malicious activity. This detection rule identifies potential abuse of PowerShell for malware execution.

#### Related Technique

MITRE ATT&CK: T1059.001 (PowerShell)

### Detection Rule 2: Brute Force Login Activity

#### Description
Detects multiple failed login attempts followed by a successful authentication, which may indicate a brute-force attack or credential compromise.

#### Detection Logic

`index=main status=FAIL OR status=SUCCESS
| stats count(eval(status="FAIL")) as failed_attempts, count(eval(status="SUCCESS")) as successful_attempts by username
| where failed_attempts > 3 AND successful_attempts > 0`

###### Rationale

A high number of failed login attempts followed by a successful login is a strong indicator of brute-force or password spraying activity. This pattern suggests that an attacker may have successfully guessed valid credentials after multiple attempts.

#### Related Technique

MITRE ATT&CK: T1110 (Brute Force)
