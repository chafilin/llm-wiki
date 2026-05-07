# A10:2021 – Server-Side Request Forgery (SSRF)

Source: https://owasp.org/Top10/2021/A10_2021-Server-Side_Request_Forgery_(SSRF)/

## Overview

SSRF was added to the OWASP Top 10 based on community survey feedback. It represents a relatively low incidence rate but carries above-average testing coverage and exploit potential.

## Description

SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. This vulnerability allows attackers to manipulate applications into sending requests to unintended destinations, bypassing network protections like firewalls and VPNs.

The prevalence of SSRF is increasing as web applications commonly fetch URLs for user convenience, and its severity is amplified by cloud infrastructure complexity.

## Prevention Strategies

### Network Layer Controls
- Isolate remote resource access functionality to separate networks
- Implement "deny by default" firewall policies blocking non-essential traffic
- Log all accepted and blocked network flows

### Application Layer Controls
- Validate all client-supplied input data
- Use positive allow lists for URL schemas, ports, and destinations
- Avoid sending raw responses to clients
- Disable HTTP redirections
- Monitor for DNS rebinding and race condition attacks

**Important caveat**: Deny lists and regex patterns are insufficient. Attackers possess tools and techniques to circumvent such protections.

## Attack Scenarios

Four primary attack vectors:

1. **Internal network reconnaissance** through port scanning
2. **Sensitive data exposure** via local file access (`file:///etc/passwd`)
3. **Cloud metadata extraction** targeting services like `http://169.254.169.254/`
4. **Internal service compromise** enabling RCE or DoS attacks
