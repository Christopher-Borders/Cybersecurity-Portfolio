## DNS Beaconing Detection & Investigation

This project demonstrates how DNS log analysis in Splunk can be used to detect command-and-control (C2) beaconing behavior through anomaly detection and pattern analysis.

### Scenario:
An alert indicated abnormal DNS activity originating from an internal host. The objective was to analyze the behavior and determine whether it represented a potential security threat.

### Key Skills Demonstrated:
- SIEM investigation using Splunk.
- Log analysis and query development.
- Detection of anomalous network behavior.
- Identification of beaconing patterns.
- Threat analysis and hypothesis building.

### Tools Used:
- Splunk (SIEM)
- VirusTotal (threat intelligence lookup)

### Investigation Process:
1. Queried DNS logs to identify the most active source IPs.
2. Identified `10.0.5.23` as generating significantly higher DNS traffic than other hosts.
3. Filtered logs to isolate activity from the suspicious host.
4. Analyzed timestamps to identify behavioral patterns.
5. Observed repeated DNS queries at consistent 60-second intervals.
6. Investigated queried domain characteristics.

### Sample Query Output
```
index=main src_ip=10.0.5.23
| stats count by query
```
### Result:
`asdkfj23jds.com` observed repeatedly with high frequency.

### Findings:
- Host `10.0.5.23` generated a disproportionately high volume of DNS requests.
- All queries were directed to a single domain: `asdkfj23jds.com`
- DNS requests occurred at consistent 60-second intervals over a 9-minute period.
- The domain name appears randomized and does not resemble legitimate services.

### Behavioral Indicators:
- Regular interval communication (1 request per minute).
- Repetitive domain queries.
- Lack of normal user browsing patterns.

### Threat Intelligence Check:
The domain `asdkfj23jds.com` was analyzed using VirusTotal.
No security vendors flagged the domain as malicious, and limited reputation data was available.

### Interpretation:
Despite the lack of threat intelligence hits, the observed behavior remains highly suspicious due to:

- Consistent 60-second beaconing pattern.
- Repeated communication with a single domain.
- Randomized domain structure.
  
This suggests the possibility of new or low-reputation command-and-control infrastructure.

### Conclusion:
The observed activity is consistent with command-and-control (C2) beaconing behavior. Although threat intelligence sources did not flag the domain as malicious, the consistent interval communication and domain characteristics strongly indicate automated and potentially malicious activity.

### Recommended Actions:
- Isolate the affected host from the network.
- Block the domain at DNS and firewall levels.
- Perform endpoint forensic analysis.
- Conduct malware and EDR scans.
- Review additional logs for lateral movement.

### Lessons Learned:
- DNS logs can reveal early indicators of compromise.
- Consistent timing patterns are strong indicators of automated behavior.
- Identifying outliers is critical in threat detection.
- SIEM tools enable efficient investigation and correlation of events.

### Real-World Application:
This type of analysis is commonly performed in Security Operations Centers (SOC) to detect compromised hosts communicating with external command-and-control infrastructure. Identifying beaconing patterns early can significantly reduce dwell time and limit potential damage.

### Dataset:
The dataset used in this project consists of simulated DNS log entries representing both normal and suspicious traffic patterns.

### Screenshots:
Below are example query results from Splunk demonstrating the investigation process:
