## Phishing Email Investigation

This project demonstrates how suspicious email activity can be analyzed to identify phishing attempts through examination of message content, sender characteristics, and embedded links.

### Scenario
A user reported a suspicious email claiming to be from a trusted service provider requesting urgent account verification. The objective was to analyze the email and determine whether it was a phishing attempt.

### Tools Used
- Email analysis techniques
- Browser-based link inspection
- Threat intelligence sources (e.g., VirusTotal)

### Investigation Process
Details of the investigation will be documented below.

### Suspicious Email

**From:** security-update@paypaI-verification.com  
**To:** user@example.com  
**Subject:** Urgent: Account Verification Required  

Dear Customer,

We detected unusual activity on your account. To ensure your account remains secure, you must verify your information immediately.

Failure to verify your account within 24 hours will result in account suspension.

Please click the link below to verify your account:

http://paypaI-verification-secure.com/login

Thank you,  
Security Team

### Initial Observations

- The sender domain appears suspicious and does not match the legitimate PayPal domain.
- The email creates a sense of urgency to prompt immediate action.
- The link provided does not point to an official PayPal domain.
- The use of HTTP instead of HTTPS is a security concern.

### Link Analysis

The URL `http://paypaI-verification-secure.com/login` was analyzed.

- The domain is not associated with the legitimate PayPal service.
- The spelling of "paypaI" uses a capital "I" instead of a lowercase "l", indicating possible impersonation.
- The domain structure is designed to appear trustworthy but is misleading.

This strongly suggests the link is part of a phishing attempt designed to capture user credentials.

### Conclusion

The email exhibits multiple strong indicators of phishing, including domain impersonation, deceptive URL structure, and urgency-based social engineering tactics. These characteristics are consistent with credential harvesting campaigns designed to deceive users and capture sensitive information.

The email should be classified as malicious and treated as a high-risk security threat.

### Impact

If a user were to click the link and enter credentials, the attacker could gain unauthorized access to the user’s account, potentially leading to account takeover, data exposure, or further phishing attacks.

### Severity
High

### Recommended Actions

- Do not click any links or provide any information.
- Report the email to the security team.
- Block the sender domain.
- Educate users on recognizing phishing attempts.
- -Reset affected user credentials if interaction occurred.

### Email Header Analysis

A review of the email headers revealed discrepancies between the sender domain and the originating mail server.

- The "From" address does not match the sending infrastructure.
- The domain lacks proper authentication records such as SPF, DKIM, or DMARC (simulated scenario).
- The email appears to originate from an untrusted source.

These inconsistencies are common indicators of email spoofing and phishing activity.

#### Email Authentication Results

The following illustrates the lack of proper email authentication in this simulated scenario:

![Email Authentication](../email_authentication_results.png)

### Social Engineering Indicators

- Use of urgent language ("verify immediately", "account suspension").
- Impersonation of a trusted brand (PayPal).
- Fear-based messaging to prompt user action.
- Lack of personalization (generic greeting).

These tactics are commonly used in phishing campaigns to manipulate users into taking action without verification.

### Related Techniques

MITRE ATT&CK:  
- T1566.002 – Phishing: Spearphishing Link

### Screenshots

#### Phishing Email Example
(Add screenshot here if available)
