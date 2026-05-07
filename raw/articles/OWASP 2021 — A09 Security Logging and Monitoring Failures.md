# A09:2021 – Security Logging and Monitoring Failures

Source: https://owasp.org/Top10/2021/A09_2021-Security_Logging_and_Monitoring_Failures/

## Overview

Security logging and monitoring ranked third in the OWASP Top 10 community survey and moved up from tenth position in the 2017 edition. This category helps organizations detect, escalate, and respond to active security breaches through proper logging infrastructure and monitoring practices.

## Key Statistics

| Metric | Value |
|--------|-------|
| CWEs Mapped | 4 |
| Max Incidence Rate | 19.23% |
| Avg Incidence Rate | 6.51% |
| Total Occurrences | 53,615 |
| Total CVEs | 242 |

## What Constitutes a Failure

Organizations experience insufficient logging and monitoring when:

- Important security events like logins, failed authentication attempts, and high-value transactions lack logging
- Warnings and errors produce no logs or unclear log messages
- Application logs aren't reviewed for suspicious patterns
- Logs remain only stored locally without centralized management
- Alert thresholds and escalation procedures are absent or ineffective
- Security scanning tools fail to trigger detection systems
- Real-time or near-real-time threat detection is unavailable
- Logging systems themselves become vulnerable to injection attacks or unauthorized access

## Prevention Strategies

Development teams should implement controls such as:

- Logging all authentication events with sufficient context to identify suspicious accounts
- Generating logs in formats compatible with log management solutions
- Properly encoding log data to prevent injection vulnerabilities
- Creating append-only audit trails for high-value transactions
- Establishing DevSecOps monitoring and alerting procedures
- Adopting incident response frameworks like NIST 800-61r2

Organizations can leverage tools including ModSecurity Core Rule Set and the ELK stack for enhanced visibility.

## Real-World Impact Examples

- A children's health plan suffering seven years of undetected breach exposure
- An airline experiencing compromise of millions of passenger records
- Another airline facing €20 million in GDPR penalties following payment system exploitation affecting 400,000+ customers

## Related CWE Categories

- CWE-117: Improper Output Neutralization for Logs
- CWE-223: Omission of Security-relevant Information
- CWE-532: Insertion of Sensitive Information into Log File
- CWE-778: Insufficient Logging
