# One-time passwords (OTP)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Authentication/OTP

A _one-time password_ (OTP), also known as _one-time PIN_, or _one-time authorization code_ (OTAC) is a generated code that is specific to a single login attempt. The website either sends the code to the user in a separate channel, such as an email, or the user's device independently generates the code.

## Overview

Authentication flows with one-time passwords are based on something the user has (a phone, an email address, a secret stored in an authenticator app) rather than something they know (a password).

OTPs can either be used in addition to traditional passwords, or they can replace them. Often they are used to confirm the user's intentions, for example when making a payment.

Many OTPs are 6 digits long with a 1-in-a-million chance to guess correctly. OTPs are usually only valid once for a defined timeframe and invalidated after use. OTPs have a short expiration time (ideally ≤5 minutes; 30–120 seconds for stronger protection).

## Email OTP

Two common approaches:

1. **Personalized one-time link**: The website sends a personalized one-time link to the user's email address. When the user clicks the link, the website authenticates the user. The link is only valid for a few minutes. Highly convenient but requires completing the process on the same device and browser, and makes users more vulnerable to phishing attacks.

2. **Personalized one-time code**: The website sends a personalized one-time code to the user's email address. The user types the code into the website on their desired device. This is more flexible and more secure than using links.

## SMS OTP

In SMS OTP, the user provides their cellphone number during registration, and at sign-in the website sends the one-time code to the phone in an SMS message.

### Weaknesses of SMS OTP

- SMS messages can be decrypted within minutes or seconds.
- Known flaws in SMS routing protocols (SS7) allow attackers to redirect text messages.
- In SIM swap scams, attackers abuse mobile number portability to impersonate the victim.
- Carriers can recycle phone numbers to new users after an account is closed.

**Recommendation**: Do not use SMS OTP on its own to establish new sessions or for general authentication. Only use it as a second factor.

### Autocompleting SMS Codes

Format the SMS message like this:

```
Your verification code is 123456.

@www.example.com #123456
```

Then in your site's login form, provide an `<input>` element with the `autocomplete=one-time-code` attribute:

```html
<form action="/verify-otp" method="POST">
  <input
    required
    type="text"
    autocomplete="one-time-code"
    inputmode="numeric"
    maxlength="6"
    pattern="\d{6}" />
  <input type="submit" />
</form>
```

The browser will automatically extract the code from the SMS, and if the origin matches, it will autofill the input element.

## TOTP (Time-Based One-Time Password)

With time-based one-time passwords, the website does not send the sign-in code to the user. Instead, both the website and user generate the same code independently based on the current time and a shared secret using an _authenticator app_.

### TOTP Algorithm

The TOTP algorithm is specified in RFC 6238.

Key characteristics:
- Creates 6-digit one-time codes
- Valid for a limited time (usually 30 seconds)
- Implements time-based validity and automatic invalidation by design
- Secret key should be at least 160 bits long

Use a well-regarded third-party package like [pyotp](https://pyauth.github.io/pyotp/) (Python) or [otpauth](https://www.npmjs.com/package/otpauth) (Node.js).

### The `otpauth` URI Format

```
otpauth://totp/LABEL?secret=MQCHJLS6FJXT2BGQJ6QMG3WCAVUC2HJZ&issuer=My_Website
```

Key parameters:
- **`LABEL`**: Identifies the user (e.g., username)
- **`secret`**: The shared secret encoded in Base32
- **`issuer`**: The name of the provider or service (strongly recommended)

## Strengths and Weaknesses

### Strengths

Compared to passwords, OTP's biggest strength is that users are not involved in creating or remembering secrets, making OTP not vulnerable to guessing or credential stuffing attacks.

### Weaknesses

- SMS and email-based OTP risk interception; SMS is much weaker in this respect.
- TOTP is not vulnerable to interception but risks an attacker accessing the shared secret.
- All forms of OTP are vulnerable to phishing attacks.
- For TOTP, requiring an authenticator app installation is a significant barrier to sign-up.

## OTP Recommendations

OTP, particularly TOTP, is useful as an additional authentication factor and for confirming user intentions (like payments). For general authentication, use **passkeys** instead—they're more resistant to phishing attacks.

If you implement OTP:

- **Prefer TOTP** to email-based or SMS-based OTP
- **Avoid SMS-based OTP** for general authentication
- If using TOTP: Use a reputable library, store the secret securely on the server
