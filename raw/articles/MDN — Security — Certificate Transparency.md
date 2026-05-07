# Certificate Transparency

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Certificate_Transparency

**Certificate Transparency** is an open framework designed to protect against and monitor for certificate mis-issuances. With certificate transparency, newly-issued certificates are 'logged' to publicly-run, often independent _CT logs_ — which maintain an append-only, cryptographically-assured record of issued TLS certificates.

In this way, certificate authorities (CAs) can be subject to much greater public scrutiny and oversight. Potentially malicious certificates can be detected and revoked much more quickly. Browser vendors and root store maintainers are also empowered to make more informed decisions regarding problematic CAs that they may decide to distrust.

## Background

CT logs are built upon the foundation of the _Merkle tree_ data structure. Nodes are labelled with the _cryptographic hashes_ of their child nodes. Leaf nodes contain hashes of actual pieces of data. The label of the root node therefore depends on all other nodes in the tree.

In the context of certificate transparency, the data hashed by the leaf nodes are the certificates that have been issued by the various different CAs operating today.

## Implementation

When certificates are submitted to a CT log, a _signed certificate timestamp_ (SCT) is generated and returned. This serves as a proof that the certificate has been submitted and will be added to the log.

The specification states that compliant servers _must_ provide a number of these SCTs to TLS clients when they connect. This can be accomplished via a number of different mechanisms:

- **X.509v3 certificate extension** which embeds signed certificate timestamps directly into the leaf certificate
- **A TLS extension** of type `signed_certificate_timestamp` sent during the handshake
- **OCSP stapling** providing a `SignedCertificateTimestampList` with one or more SCTs

## Browser Requirements

**Google Chrome 107 and later** requires CT log inclusion for all certificates issued with a notBefore date of after 30 April 2018. Users will be prevented from visiting sites using non-compliant TLS certificates.

**Apple** requires a varying number of SCTs in order for Safari and other servers to trust server certificates.

**Firefox desktop**, starting from version 135, and **Firefox for Android**, starting from version 145, require CT log inclusion for all certificates issued by certificate authorities in Mozilla's Root CA Program.

## Specifications

Browser implementations are based on [RFC 6962: Certificate Transparency](https://datatracker.ietf.org/doc/html/rfc6962) and the current specification [RFC 9162: Certificate Transparency Version 2.0](https://datatracker.ietf.org/doc/html/rfc9162).
