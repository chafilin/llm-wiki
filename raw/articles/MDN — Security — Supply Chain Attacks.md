# Supply Chain Attacks

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Supply_chain_attacks

## Overview

A **software supply chain** consists of all the software and tools used to create and maintain a software product, including third-party dependencies, build tools, version control systems, and development environments.

In a supply chain attack, attackers target part of the product's supply chain to compromise the final product itself.

## Key Vulnerability Areas

1. **Third-party libraries** (e.g., npm packages) - can be compromised deliberately or accidentally
2. **Development tools** - code editors, editor plugins, version control systems, build tools
3. **External scripts** - scripts served from CDNs that can be replaced with malicious versions

## Defense Strategies

### 1. Securing Your Development Environment

#### Implementing Access Control
- Require **multi-factor authentication** for team members
- Follow the **principle of least privilege** - only grant necessary permissions
- Minimize the number of team members with powerful permissions

#### Securing Configuration
- Ensure pull requests go through **code review and explicit approval**
- Require PRs to pass **continuous integration checks** before merging
- Require **signed commits**

### 2. Managing Third-Party Dependencies

#### Evaluating New Dependencies
Before adding a dependency:
- Verify it's actively maintained
- Check for a security vulnerability reporting and response process
- Weigh the risk against the cost of implementing the feature yourself

#### Using Lockfiles

Without a lockfile, `npm install` automatically fetches the latest version matching a range. If an attacker compromises the package author's account and releases a malicious version, it gets installed automatically.

The solution - Use a lockfile:
- Create a lockfile (e.g., `package-lock.json`) that specifies exact versions
- Commit the lockfile to source control
- Use `npm ci` instead of `npm install` during builds
- This forces pull requests for any dependency updates, allowing review before acceptance

#### Reviewing Updates

- Read the changelog to understand what changed
- Check for new dependencies introduced
- Review source code changes if possible
- Consider waiting a brief period - supply chain attacks are often quickly discovered

#### Maintaining a Software Bill of Materials (SBOM)

An SBOM is a detailed inventory of dependencies in a standard format.

**Common Standards:**
- **CycloneDX** - developed by OWASP, focused on supply chain security
- **SPDX** - maintained by Linux Foundation, focused on licenses and security

**Creating an SBOM:**
- Use tools like [cdxgen](https://cdxgen.github.io/cdxgen/#/) or `npm sbom`
- Generate as part of the build process

**SBOM Uses:**
1. **Vulnerability management** - automate scanning for known vulnerabilities using tools like [Dependency-Track](https://dependencytrack.org/)
2. **Integrity verification** - verify components haven't been modified using hashes
3. **Supplier risk management** - identify unreliable suppliers

#### Using Subresource Integrity (SRI)

For externally hosted scripts (especially from CDNs):

**Without SRI (Vulnerable):**
```html
<script src="https://cdn.example.org/library.js"></script>
```

If the CDN is compromised, a malicious script could replace the legitimate one.

**With SRI (Protected):**
```html
<script
  src="https://cdn.example.org/library.js"
  integrity="sha256-d5f450f7ce715d827de27ca569e183f819d33c1e7601875fd61eccbc98f56c5b"></script>
```

If the script is modified, the browser refuses to load it.

## Defense Summary Checklist

- ✅ Require multi-factor authentication for team members and minimize permissions
- ✅ Assess tools involved in build, test, and deployment processes
- ✅ Ensure pull requests go through review and continuous integration checks
- ✅ Minimize dependencies and evaluate new ones carefully
- ✅ Use a lockfile to control updates and follow a review process
- ✅ Maintain an SBOM and use it for vulnerability checking
- ✅ Use Subresource Integrity for external scripts and stylesheets
