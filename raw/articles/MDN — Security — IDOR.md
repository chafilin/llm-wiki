# Insecure Direct Object Reference (IDOR)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/IDOR

**Insecure Direct Object Reference (IDOR)** is a vulnerability that allows an attacker to exploit insufficient access control and insecure exposure of object identifiers, such as database keys or file paths.

## Overview

Websites often serve different content to different users. While websites can identify users through authentication (passwords, passkeys, etc.) and session cookies, they must also implement access control to verify that each user can only access their own resources.

If a server doesn't implement proper access control, an authenticated attacker may access resources belonging to other users. This is an IDOR attack.

## Example Scenarios

### URL Tampering

A common IDOR attack involves modifying user/resource identifiers in URLs.

**Vulnerable Code (Express):**
```javascript
app.get("/user/id/:id", (req, res) => {
  const user = db.users.find(req.params.id);
  if (req.isAuthenticated()) {
    // Authentication is not enough!
    res.render("user", { user });
  }
});
```

**Secure Code:**
```javascript
app.get("/user/id/:id", (req, res) => {
  const user = db.users.find(req.params.id);
  if (req.isAuthenticated() && req.session.userId === req.params.id) {
    res.render("user", { user });
  } else {
    return res.status(401).json({ message: "Unauthorized" });
  }
});
```

### Document Manipulation

Attackers can modify form elements in the browser's developer tools, including hidden input fields:

```html
<form action="updateUser" method="POST">
  <input type="hidden" name="user_id" value="1234" />
  <button type="submit">Update profile</button>
</form>
```

Without server-side access control, an attacker can change the `user_id` to modify another user's profile.

### File Access

If files are named sequentially without access control, attackers can guess and download them:

```
https://example.org/static/pdfs/1.pdf
https://example.org/static/pdfs/2.pdf
```

## Defenses Against IDOR

### Access Control for Each Object

The most important mitigation is implementing server-side access control checks for each object. Always verify that the authenticated user has the right to access or perform actions on the targeted object.

### Identifier Complexity

- Don't expose personally identifiable information (PII) like usernames or email addresses in URLs
- Use unique non-guessable tokens to represent users
- Use complex IDs such as UUIDs instead of sequential numbers
- Note: Complex IDs reduce guessing likelihood but don't replace proper access control

## Defense Summary Checklist

- ✓ Always verify that the authenticated user is authorized to access or modify the object
- ✓ Avoid exposing predictable, sequential, or sensitive object identifiers
- ✓ Use more complex IDs that are harder to predict (e.g., UUIDs)
