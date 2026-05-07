# A07:2021 – Identification and Authentication Failures

Source: https://owasp.org/Top10/2021/A07_2021-Identification_and_Authentication_Failures/

## Overview

Formerly called "Broken Authentication," this vulnerability category examines weaknesses in user identity confirmation and session handling. It ranked seventh in OWASP's 2021 Top 10 security risks, affecting approximately 2.55% of applications on average.

## Key Vulnerabilities

The category encompasses 22 mapped Common Weakness Enumerations (CWEs). Critical weaknesses include:

- **Credential attacks**: Permits automated attacks such as credential stuffing, where the attacker has a list of valid usernames and passwords
- **Weak password policies**: Allowing default or easily guessable credentials
- **Inadequate credential recovery**: Unreliable password reset mechanisms
- **Weak storage**: Uses plain text, encrypted, or weakly hashed passwords data stores
- **Insufficient MFA**: Missing or ineffective multi-factor authentication
- **Session mismanagement**: Improper session ID handling and insufficient logout procedures

## Prevention Strategies

Organizations should:

- Implement multi-factor authentication to prevent stuffing and brute force attacks
- Eliminate default credentials entirely
- Test new passwords against known weak password lists
- Follow NIST 800-63b guidelines for password policies
- Use identical messaging for all authentication outcomes to prevent account enumeration
- Implement rate limiting on failed login attempts
- Deploy secure server-side session managers that generate high-entropy identifiers and invalidate sessions appropriately

## Common Attack Patterns

Three primary attack scenarios: credential stuffing exploits, continued reliance on passwords alone, and browser session timeout vulnerabilities.
