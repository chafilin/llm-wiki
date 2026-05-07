# A08:2021 – Software and Data Integrity Failures

Source: https://owasp.org/Top10/2021/A08_2021-Software_and_Data_Integrity_Failures/

## Overview

This OWASP Top 10 category addresses vulnerabilities stemming from inadequate integrity verification in software updates, data handling, and development pipelines. The vulnerability encompasses ten mapped Common Weakness Enumerations (CWEs) with a maximum incidence rate of 16.67%.

## Key Vulnerabilities

The category highlights three primary concerns:

1. **Untrusted Dependencies**: Applications relying on plugins, libraries, or modules from unverified sources without integrity validation
2. **Insecure CI/CD Pipelines**: Systems vulnerable to unauthorized access and malicious code injection
3. **Unsafe Auto-Updates**: Software that downloads and applies updates without sufficient verification mechanisms

Additionally, insecure deserialization of untrusted data poses significant risks when objects are encoded in ways attackers can manipulate.

## Prevention Strategies

Organizations should implement:

- Digital signatures or equivalent mechanisms for software and data verification
- Consumption of libraries only from trusted repositories
- Supply chain security tools like OWASP Dependency Check to identify vulnerable components
- Code and configuration review processes before pipeline integration
- Proper segregation, configuration, and access controls in CI/CD environments
- Integrity checks or digital signatures on serialized data sent to untrusted clients

## Real-World Examples

**Unsigned Firmware**: Home routers and device firmware lacking signed update verification remain vulnerable targets.

**SolarWinds Attack**: Nation-states attacking update mechanisms, distributing malicious updates to over 18,000 organizations.

**Java Deserialization**: Applications passing serialized user state between requests can enable remote code execution when attackers exploit Java object signatures.
