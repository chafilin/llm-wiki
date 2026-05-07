# A06:2021 – Vulnerable and Outdated Components

Source: https://owasp.org/Top10/2021/A06_2021-Vulnerable_and_Outdated_Components/

## Overview

This OWASP Top 10 category addresses risks from using software components with known vulnerabilities or inadequate maintenance. It ranked #2 in the community survey and earned its position through significant incident data.

## Key Vulnerability Factors

The category encompasses 3 mapped CWEs with concerning statistics:
- **Max Incidence Rate:** 27.96%
- **Average Incidence Rate:** 8.77%
- **Total Occurrences:** 30,457 instances

Notable CWEs include "Use of Unmaintained Third-Party Components".

## When You're Vulnerable

Organizations face risk when they:

- Lack visibility into component versions across their entire technology stack, including nested dependencies
- Deploy unsupported or outdated software affecting operating systems, frameworks, databases, and runtime environments
- Neglect regular vulnerability scanning and security bulletin monitoring
- Defer patching cycles, creating extended exposure windows
- Skip compatibility testing after applying updates
- Fail to properly secure component configurations

## Prevention Strategies

Effective mitigation requires establishing a comprehensive patch management process that:

- Eliminates unused dependencies and unnecessary features
- Maintains continuous inventory of all components using automated tools like "OWASP Dependency Check" and "retire.js"
- Monitors CVE and NVD databases for newly discovered vulnerabilities
- Obtains components exclusively from official, secure sources with verified signatures
- Tracks unmaintained libraries and implements virtual patches when updates aren't feasible
- Sustains ongoing monitoring and update plans throughout each application's lifecycle

## Real-World Example

The "CVE-2017-5638 Struts 2 vulnerability enabling remote code execution" demonstrates how component flaws can facilitate severe breaches when components operate with application-level privileges.
