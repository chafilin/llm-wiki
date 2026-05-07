# Threat Modeling

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Threat_modeling

## Overview

Threat modeling is a process that helps identify and understand potential security risks in applications and websites. It enables you to understand the specific vulnerabilities of your application, the browser environment, and user interaction with your UI.

## Key Definitions

### What is a Threat?

A **threat** is anything that could potentially harm your website's functionality or the data it holds.

**Related concepts:**
- **Threat Model**: A structured representation of potential threats, including assets (what you're protecting), adversaries (who would attack you), and vulnerabilities (weak spots)
- **Attack**: When a threat is actually carried out against a live system
- **Vulnerability**: System weaknesses (e.g., XSS, JavaScript prototype pollution)
- **Mitigation**: Defensive measures implemented in response to vulnerabilities
- **Risk**: How likely a threat is to occur and how severe its impact would be

## The Threat Modeling Process

Threat modeling should happen **early in development** and be **frequently revisited**. It's not exclusively for security auditors—cross-functional collaboration makes threat models stronger.

### Four Key Questions (Threat Modeling Manifesto)

#### 1. **What are we working on?**

Create a model describing your system's:

- **Components** (C1, C2, C3...): Things that run code or store data
  - Web server, Blog software, User authentication, Third-party scripts
  
- **Assets** (A1, A2, A3...): What attackers want
  - User data and PII, User credentials, Cookies and session information, Private content

- **Data Flows & Trust Boundaries** (F1, F2, F3...): Where data crosses from untrusted to trusted areas
  - Authentication flows, Contact form submissions, Calls to external services

- **External Dependencies** (E1, E2, E3...): Systems outside your control
  - Operating system, Browser and web platform, Browser extensions

- **Stakeholders** (S1, S2, S3...): Who could be impacted
  - Anonymous users, Registered users, Disabled users, Administrators

#### 2. **What can go wrong?**

Identify threats using:
- Threat lists (OWASP Top 10)
- Threat analysis frameworks (STRIDE, LINDDUN)
- Security consideration sections in specifications
- Kill chain analysis (chain of events leading to attack)

#### 3. **What are we going to do about it?**

Respond to threats using the **ERTA** approach:

- **Eliminate**: Remove the asset or threat entirely
- **Reduce**: Make it harder (add controls, mitigations, countermeasures)
- **Transfer**: Shift responsibility to another system/organization
- **Accept**: Accept the threat exists, monitor it, and prepare for consequences

#### 4. **Did we do a good enough job?**

- Document findings in a threat model document
- File issues with your project
- Revisit and revalidate in future iterations
- Continuously improve security awareness

## Best Practices

- **Create a threat model document**: Make it extensible and version-controlled
- **Iterate continuously**: Like software iteration, continuously analyze security
- **Involve diverse participants**: Cross-functional teams strengthen models
- **Use multiple frameworks**: Different frameworks illuminate different problems
- **Tell stories**: Describe threat chains and prioritize important threats
- **Reference existing models**: Maintain lists of threat models for dependencies

## Related Resources

- [Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org)
- [W3C Threat Modeling Guide](https://w3c.github.io/threat-modeling-guide/)
- [OWASP Top 10](https://owasp.org/Top10/2025/)
