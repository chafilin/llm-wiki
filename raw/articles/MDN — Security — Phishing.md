# Phishing

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Phishing

Phishing is a social engineering attack in which a user is tricked into believing that they are interacting with a site with which they have an account, when in reality they are interacting with the attacker. The attacker convinces the user to enter their credentials on the fake site, and thereby steals the user's credentials.

## Overview

In a basic form:

1. The attacker registers a domain name that resembles the target site. For example, if the user's banking website is `my-bank.example.com`, the attacker could register `my-bank.examp1e.com`.
2. The attacker creates a site at that address that resembles the real site.
3. The attacker sends the user an email, purporting to be from `my-bank.example.com`, giving some reason to ask the user to visit the site, and containing a link to the fake site `my-bank.examp1e.com`.
4. The user clicks the link and is asked to sign in. They enter their username and password, and the attacker now has their credentials.

In _spear-phishing_ attacks, attackers research specific victims, gathering personal information about them to make the lure more convincing.

Phishing attacks are not dependent on naive or inexperienced users: decades of experience has shown that even highly experienced and knowledgeable users can be vulnerable.

## Defenses

### DNS Configuration

Three DNS records help email servers detect email forgeries, which helps ensure that phishing emails are marked as spam or blocked entirely.

- **Security Policy Framework (SPF)**: The SPF record lists addresses that are allowed to send an email from the domain.

- **DomainKeys Identified Mail (DKIM)**: The DKIM record enables the sender to digitally sign emails.

- **Domain-based Message Authentication Reporting and Conformance (DMARC)**: DMARC tells the recipient how to handle SPF and DKIM failures: whether to quarantine them as spam, reject them, or allow them.

You should set these DNS records for your domains, to help email servers recognize forged messages.

### Password Managers

Password managers can provide some degree of protection against phishing attacks by:

- **Password generation**: Creating strong passwords when users sign up.
- **Password storage**: Storing a user's passwords securely.
- **Password entry**: Automatically entering the user's password for a site, when the user visits the site's login page — the password manager will recognize the fake domain and not autofill.

### Multi-Factor Authentication

Using MFA makes phishing more difficult but, depending on the specific method used, does not prevent it.

In particular, SMS-based OTP and TOTP-based OTP are still vulnerable to real-time phishing attacks where the attacker's fake site acts as a manipulator in the middle.

### Passkeys

The strongest technical defense against phishing is to authenticate users using passkeys.

A passkey is created when the user registers on the site, and is specific to the origin for which it was originally created. When a website asks the user to authenticate using Web Authentication, the browser asks the authenticator for a passkey that matches the site's origin. If a passkey was created for the user's account at `my-bank.example.com`, the user will not be able to use it on `my-bank.examp1e.com`. The browser just won't consider it applicable to the fake site.

This makes passkeys an effective defense against phishing.

## Defense Summary Checklist

- Set `SPF`, `DKIM`, and `DMARC` DNS records for your domains.
- Consider using passkeys to authenticate users.
- If you use passwords, consider using MFA, and ensure that password managers can work with your site.
