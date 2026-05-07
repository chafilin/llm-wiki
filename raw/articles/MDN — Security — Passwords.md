# Passwords

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Authentication/Passwords

## Overview

Password-based authentication remains the most common authentication method on the web.

### Registration Flow
1. User supplies a new username and password via a `<form>` element
2. Web page sends credentials to server via `POST` request
3. Server creates a new database record with the username as key and stores the password

### Login Flow
1. User supplies username and password
2. Web page sends credentials to server
3. Server retrieves stored password and compares it with the submitted password
4. If passwords match, user is signed in

## Attacks and Defenses

### Common Attacks

| Attack | Description |
|--------|-------------|
| **Guessing** | Attacker tries many common passwords from word lists |
| **Credential Stuffing** | Attacker uses username/password pairs from previous breaches |
| **Interception** | Attacker intercepts credentials in transit (MITM attacks) |
| **Database Compromise** | Attacker breaks into server and retrieves password database |
| **Phishing** | Attacker tricks user into entering credentials on fake site |

## Registration

### Form Design Best Practices

Use proper HTML form structure to enable password manager integration:

```html
<form>
  <input type="text" name="username" autocomplete="username" placeholder="Username" />
  <input type="email" name="email" autocomplete="email" placeholder="Email" />
  <input type="password" name="password" autocomplete="new-password" placeholder="New password" />
  <input type="password" name="confirm-password" autocomplete="new-password" placeholder="Confirm password" />
  <button type="submit">Register</button>
</form>
```

**Key Points:**
- Correct `autocomplete` attributes: `"username"` for username fields, `"new-password"` for new password creation
- Ask user to enter password twice for confirmation

### Password Validation

When server receives `POST` request:
- Validate username doesn't already exist
- Validate password copies match each other
- Reject weak passwords
- Check against known compromised password lists

## Storing Passwords

### Hashing Requirements

**Never store plaintext passwords.** Instead:

1. Hash the password using a secure algorithm
2. Store the hash in the database
3. On login, hash the submitted password and compare hashes

### Salt and Pepper

**Salt:**
- Random value unique to each password
- Does NOT have to be secret
- Stored alongside the hash
- Prevents rainbow table attacks

**Pepper:**
- Secret value (same for all passwords)
- NOT stored in database (kept in separate HSM/secure location)
- Additional defense layer against database compromise

### Recommended Hashing Algorithms (in order of preference)

1. **Argon2id** ⭐ (preferred)
2. **scrypt**
3. **bcrypt**
4. **PBKDF2**

**Important:** Use functions provided by reputable frameworks rather than implementing your own.

## Login

### Form Design

Use similar structure to registration with correct attributes:

```html
<form>
  <input type="text" name="username" autocomplete="username" placeholder="Username" />
  <input type="password" name="password" autocomplete="current-password" placeholder="Password" />
  <button type="submit">Sign In</button>
</form>
```

**Key difference:** Use `autocomplete="current-password"` for login forms (not `"new-password"`)

### Server-Side Login Logic

```javascript
// When server receives login request:
const storedRecord = database.findByUsername(username);

if (!storedRecord || !hashMatches(password, storedRecord.hash)) {
  // Return same error message in both cases
  return { error: "Invalid username or password" };
}
```

**Critical:** Return the same error message whether username doesn't exist OR password is wrong. This prevents attackers from enumerating valid usernames.

## Password Reset

### Reset Flow

1. **User Request:** Enter email address
2. **Server Response:** Return same message whether email exists or not ("We've sent an email with further instructions") — prevents enumeration of registered emails
3. **If Email Exists:** Generate random reset token, store with expiry, send email with reset link
4. **User Clicks Link:** Verify token exists and hasn't expired, allow user to enter new password
5. **Confirmation:** Send confirmation email that password was changed

## Weaknesses of Password-Based Authentication

Despite best practices, passwords have inherent vulnerabilities:

- **Credential Stuffing:** Even strong passwords don't prevent attacks if user reuses them across sites
- **Guessing:** Can't guarantee users choose truly strong passwords
- **Phishing:** No defense against users voluntarily giving password to attackers

### Recommendations

Consider supplementing or replacing passwords with:
- **One-Time Passwords (OTP)** as second factor
- **Passkeys** (phishing-resistant)
- **Multi-factor authentication (MFA)**
