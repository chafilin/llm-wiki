# Cross-site scripting (XSS)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS

A cross-site scripting (XSS) attack is one in which an attacker is able to get a target site to execute malicious code as though it was part of the website.

## Overview

A web browser downloads code from many different websites and runs it on the user's computer. The foundation of the browser's security model is the same-origin policy, which keeps sites separate so code from one site cannot access objects or credentials in another site.

In a successful XSS attack, the attacker subverts the same-origin policy by tricking the target site into executing malicious code within its own context. The code can then:

- Access and/or modify all content of the site's loaded pages and local storage
- Make HTTP requests with the user's credentials, enabling impersonation or access to sensitive data

**All XSS attacks depend on a website doing two things:**

1. Accepting input that could have been crafted by an attacker
2. Including this input in a page without sanitizing it—without ensuring it won't be executable as JavaScript

## Two XSS Examples

### Code Injection in the Browser

A bank website displays a personalized welcome message extracted from a URL parameter:

```html
<h1 id="welcome"></h1>
```

```javascript
const params = new URLSearchParams(window.location.search);
const user = params.get("user");
const welcome = document.querySelector("#welcome");

welcome.innerHTML = `Welcome back, ${user}!`;
```

An attacker sends a malicious link:

```html
<a href="https://my-bank.example.com/welcome?user=<img src=x onerror=alert('hello!')>">
  Get a free kitten!
</a>
```

When clicked, the page extracts the URL parameter and assigns it to `innerHTML`, creating an `<img>` element. Since `src=x` generates an error, the `onerror` handler executes the attacker's code.

### Code Injection in the Server

A search page displays results with a title showing the search term:

```javascript
app.get("/results", (req, res) => {
  const searchQuery = req.query.search;
  const results = getResults(searchQuery);
  res.send(`
   <h1>You searched for ${searchQuery}</h1>
   <p>Here are the results: ${results}</p>`);
});
```

An attacker sends a malicious link:

```html
<a href="http://example.org/results?search=<img src=x onerror=alert('hello')">
  Get a free kitten!
</a>
```

The server embeds the malicious code directly in the returned HTML, which executes in the browser.

## Anatomy of an XSS Attack

Both examples are possible because websites:

1. Use input that could be crafted by an attacker
2. Include the input without sanitizing it

Other vectors include:

- **Stored/Persistent XSS**: Attackers submit malicious comments to a blog, which are stored in a database and served to all users. This is particularly severe because the infected content is served every time the page is accessed.

### Client and Server XSS

- **Client-side rendering**: Single-page apps modify pages in the browser using APIs like `document.createElement()` or frameworks like React. XSS injection happens when unsanitized input is assigned to properties like `Element.innerHTML`.

- **Server-side rendering**: Frameworks like Django or Express build pages on the server by inserting values into templates. XSS injection happens during the templating process when unsanitized input is embedded.

The general defense approach is the same for both, but the specific tools differ.

## Defenses Against XSS

### 1. Output Encoding

Output encoding escapes characters that make input dangerous, so they're treated as text instead of executable code.

Most modern templating engines automatically perform output encoding. Django's templating engine, for example, converts:

- `<` → `&lt;`
- `>` → `&gt;`
- `'` → `&#x27;`
- `"` → `&quot;`
- `&` → `&amp;`

**Django template:**
```django
<p>You searched for {{ search_term }}.</p>
```

If you pass `<img src=x onerror=alert('XSS!')>`, it becomes `&lt;img src=x onerror=alert(&#x27;XSS!&#x27;)&gt;`, displayed as plain text.

**React:**
```jsx
import React from "react";

export function App(props) {
  return <div>Hello, {props.name}!</div>;
}
```

Values in JSX are automatically encoded. Passing `<img src=x onerror=alert('XSS!')>` renders as plain text.

#### Document Contexts

The type of encoding needed depends on context:

- **HTML contexts**: Input between HTML element tags (except `<style>` or `<script>`). Template engines mostly handle this.

- **HTML attribute contexts**: Sometimes safe, sometimes not. Event handler attributes (`onblur`) and `src` attributes on `<iframe>` are unsafe. Always quote attribute values:

  ```django
  <!-- Unsafe -->
  <div class={{ my_class }}>...</div>
  
  <!-- Safe -->
  <div class="{{ my_class }}">...</div>
  ```

  An attacker could exploit the unquoted version with input like `some_id onmouseover=alert(1)`.

- **JavaScript and CSS contexts**: Inserting input inside `<script>` or `<style>` tags is almost always unsafe.

### 2. Sanitization

When you need to include input as HTML (not text), sanitize it using a reputable library like [DOMPurify](https://github.com/cure53/DOMPurify), recommended by OWASP.

### 3. Trusted Types

The Trusted Types API ensures input is always sanitized before being passed to unsafe APIs like:

- `Element.innerHTML`
- `Element.outerHTML`
- `Element.insertAdjacentHTML()`
- `Document.write()`
- `eval()`
- `Window.setTimeout()` and `Window.setInterval()`

Enable it with the CSP directive:
```
require-trusted-types-for 'script'
```

### 4. Content Security Policy (CSP)

A strict CSP using nonces or hashes prevents execution of malicious scripts even if they enter a page:

- Disallows inline event handlers
- Disallows `javascript:` URLs
- Disallows APIs like `eval()`
- Requires correct nonce/hash for legitimate scripts

## Defense Summary Checklist

- ✓ When interpolating input into a page (browser or server), use a templating engine that performs output encoding
- ✓ Be aware of the context in which you're interpolating input and ensure appropriate encoding is performed
- ✓ If including input as HTML, sanitize it using a reputable library (DOMPurify)
- ✓ If doing this in the browser, use the trusted types framework to ensure input is processed by your sanitization function
- ✓ Implement a strict CSP
