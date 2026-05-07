# Passkeys

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Authentication/Passkeys

Passkeys enable websites to authenticate users without passwords or secret codes entered on the site. They use public-key cryptography instead of shared secrets.

## Overview

A passkey is a **public/private key pair** bound to a specific user's account on a particular website:

- **Private key**: Stored in an authenticator (built into the device, hardware key like YubiKey, or credential manager app)
- **Public key**: Stored on the website's server

When signing in, the authenticator uses the private key to digitally sign a challenge value from the server, creating an _assertion_. The server verifies the assertion's signature using the public key.

## Web Authentication API (WebAuthn)

Websites use the Web Authentication API to interact with authenticators. The two main functions are:

- **`CredentialsContainer.create()`** - Create a new passkey during registration
- **`CredentialsContainer.get()`** - Generate an assertion to sign in

## Registration Flow

1. User asks to register on the site
2. RP's frontend requests a **challenge** from the server
3. Frontend calls `CredentialsContainer.create()` with challenge value, website info, and user info
4. Authenticator creates the passkey and stores the private key
5. Frontend sends the public key to the server, which creates the user account and stores the public key

## Sign-In Flow

1. User tries to sign in
2. Frontend requests a challenge from the server
3. Frontend calls `CredentialsContainer.get()` with challenge and website ID
4. Browser finds matching passkeys for the site's origin
5. Authenticator creates a digitally signed assertion
6. Server verifies signature using the stored public key

## Key Features

### Platform vs. Roaming Authenticators

- **Platform authenticators**: Built into device (Touch ID, Windows Hello) - convenient but tied to one device
- **Roaming authenticators**: Removable/portable (USB keys like YubiKey) - can be used with multiple devices

### Discoverable Credentials

Passkeys must always be discoverable — set `residentKey: "required"` and `requireResidentKey: true`.

This enables autofill UI for passkeys (like password autofill).

### User Verification

Authenticator asks user to authorize the operation (PIN, biometric). Provides multi-factor authentication when combined with the authenticator itself.

### Passkey Scope

By default, a passkey can only be used by pages from the same origin as the page that created it. Because the passkey is specific to the site's origin, if a passkey was created for the user's account at `my-bank.example.com`, the user will not be able to use it on `my-bank.examp1e.com`. **This makes passkeys an effective defense against phishing.**

## Security Properties

Passkeys address major password weaknesses:

- **No weak user-chosen values** - Users don't invent passkeys; generation is delegated to authenticators
- **Site-specific** - Never reused across sites; not vulnerable to credential stuffing
- **Server doesn't store secrets** - Only stores public key; private key compromises don't happen at the server
- **Phishing resistant** - Browser only looks for passkeys matching the requesting site's scope

## Migrating from Passwords

### Step 1: Create Passkeys Alongside Passwords

Offer passkey creation after successful password sign-in.

Use `CredentialsContainer.create()` with `mediation: "conditional"`:

```javascript
try {
  const publicKeyCredential = await navigator.credentials.create({
    publicKey: options,
    mediation: "conditional",
  });
  // handle new passkey creation
} catch (e) {
  // passkey was not created
}
```

### Step 2: Use Passkeys Alongside Passwords

Add `autocomplete="username webauthn"` to the username field:

```html
<input type="text" name="username" autocomplete="username webauthn" autofocus />
```

Call `CredentialsContainer.get()` with `mediation: "conditional"`.

### Step 3: Retire Passwords

As a final step, offer users the option to delete their password entirely, verifying they have multiple passkeys or backed-up passkeys first.

## See Also

- [The Web Authentication API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API)
- [passkeys.dev](https://passkeys.dev/)
