## Suspicious Process Investigation

This project demonstrates how endpoint process log analysis in Splunk can be used to detect suspicious PowerShell activity and potential malware execution through behavioral analysis.

### Scenario
An alert indicated unusual PowerShell execution on an endpoint. The objective was to investigate process activity and determine whether it represented malicious behavior.

### Key Skills Demonstrated
- SIEM investigation using Splunk.
- Endpoint process analysis.
- Detection of suspicious PowerShell usage.
- Identification of encoded command execution.
- Behavioral analysis of process activity.

### Tools Used
- Splunk (SIEM)

### Investigation Process
1. Queried process logs to identify the most frequently executed processes.
2. Identified `powershell.exe` as exhibiting elevated activity.
3. Filtered logs to isolate PowerShell execution events.
4. Analyzed command-line arguments for suspicious indicators.
5. Observed repeated use of encoded command execution flags.
6. Investigated parent-child process relationships.
7. Compared normal versus suspicious PowerShell activity.

### Sample Queries

#### PowerShell Execution Timeline

`index=main process_name=powershell.exe
| table _time, parent_process, command_line
| sort _time`

This query was used to analyze the sequence of PowerShell execution events, identify parent-child relationships, and observe repeated suspicious command patterns.

PowerShell Command Frequency

`index=main process_name=powershell.exe
| stats count by command_line
| sort -count`

This query was used to quantify repeated command execution and identify the most frequently executed PowerShell commands.

Findings
Multiple instances of PowerShell execution were observed.
The command powershell.exe -nop -enc SQBFAFgA was executed repeatedly.
Encoded command execution (-enc) was used to obfuscate activity.
The -nop flag was used to bypass PowerShell profile loading.
PowerShell was frequently launched by cmd.exe, indicating potential scripted execution.
PowerShell spawned additional PowerShell processes, suggesting chained execution.
A single instance of normal PowerShell usage (Get-Process) was observed, contrasting with suspicious activity.
Behavioral Indicators
Repeated execution of identical encoded commands.
Use of obfuscation techniques (-enc flag).
Execution patterns consistent with automation.
Suspicious parent-child process relationships.
Presence of both normal and malicious PowerShell activity.
Interpretation

The repeated execution of encoded PowerShell commands using -nop -enc flags strongly indicates obfuscated script execution. This technique is commonly used by attackers to conceal malicious payloads and evade detection.

The consistent repetition of the same encoded command suggests automated or scripted activity rather than manual user interaction. Additionally, the presence of suspicious parent-child relationships, such as cmd.exe launching PowerShell and PowerShell spawning itself, further supports the likelihood of malicious behavior.

Conclusion

The investigation identified suspicious PowerShell activity consistent with potential malware execution or attacker-driven script activity. The combination of encoded command usage, repeated execution, and abnormal process relationships strongly indicates malicious behavior on the endpoint.

Recommended Actions
1. Isolate the affected host from the network.
2. Investigate the system for malware or unauthorized scripts.
3. Block or monitor suspicious PowerShell activity.
4. Implement endpoint detection and response (EDR) tools.
5. Enforce PowerShell logging and monitoring policies.
6. 
Lessons Learned
PowerShell is a powerful administrative tool frequently abused by attackers.
Encoded commands are a strong indicator of obfuscation and malicious intent.
Parent-child process relationships provide critical context in investigations.
Behavioral analysis is essential for detecting endpoint threats.
Real-World Application

This type of analysis is commonly performed in Security Operations Centers (SOC) to detect malware execution and suspicious endpoint activity. Identifying abnormal PowerShell usage is a critical skill for detecting advanced threats and living-off-the-land attacks.

Dataset

process_logs.csv

This dataset contains simulated endpoint process logs representing both normal and suspicious activity for analysis in Splunk.

Screenshots
PowerShell Execution Timeline

PowerShell Command Frequency
