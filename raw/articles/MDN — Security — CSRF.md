# Cross-site request forgery (CSRF)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/CSRF

## Overview

In a cross-site request forgery (CSRF) attack, an attacker tricks the user or the browser into making an HTTP request to the target site from a malicious site. The request includes the user's credentials and causes the server to carry out some harmful action, thinking that the user intended it.

### How CSRF Attacks Work

In a CSRF attack, the attacker creates a website containing a form. The form's `action` attribute is set to the bank's website, and the form contains hidden input fields mimicking the bank's fields:

```html
<form action="https://my-bank.example.org/transfer" method="POST">
  <input type="hidden" name="recipient" value="attacker" />
  <input type="hidden" name="amount" value="1000" />
</form>
```

The page also contains JavaScript that submits the form on page load:

```javascript
const form = document.querySelector("form");
form.submit();
```

When the user visits the page, the browser submits the form to the bank's website. Because the user is signed into their bank, the request may include the user's real cookie, so the bank's server successfully validates the request, and transfers the funds.

### Vulnerability Requirements

In general, a CSRF attack is possible if your website:

- Uses HTTP requests to change some state on the server.
- Uses only cookies to validate that the request came from an authenticated user.
- Uses only parameters in the request that an attacker can predict.

## Defenses Against CSRF

### 1. CSRF Tokens

In this defense, when the server serves a page, it embeds an unpredictable value in the page, called the CSRF token. When the legitimate page sends the state-changing request to the server, it includes the CSRF token in the HTTP request. The server can then check the token value and carries out the request only if it matches.

Because an attacker can't guess the token value, they can't issue a successful forgery. Even if the attacker discovers a token after it has been used, the request can't be replayed if the token changes every time.

Modern web frameworks usually have built-in support for CSRF tokens. For example, Django enables you to protect forms using the `csrf_token` tag.

### 2. Fetch Metadata

Fetch metadata is a collection of HTTP request headers, added by the browser, that provide extra information about the context of an HTTP request. The server can use these headers to decide whether to allow a request or not.

Most relevant for CSRF is the `Sec-Fetch-Site` header, which tells the server whether this request is same-origin, same-site, cross-site, or initiated directly by the user.

Example Express code:

```javascript
app.post("/transfer", (req, res) => {
  const secFetchSite = req.headers["sec-fetch-site"];
  if (secFetchSite === "same-origin" || secFetchSite === "same-site") {
    console.log("allowed");
    // Update state
  } else {
    console.log("denied");
    // Don't update state
  }
});
```

### 3. Avoiding Simple Requests

Web browsers distinguish two sorts of HTTP requests: simple requests and other requests. Simple requests, which result from a `<form>` element submission, can be made cross-origin without being blocked.

However, JavaScript APIs like `fetch()` and `XMLHttpRequest` can make different sorts of requests that are by default not allowed cross-origin, so a CSRF attack would not succeed.

A website that uses `fetch()` or `XMLHttpRequest` can defend against CSRF by ensuring that state-changing requests are never simple requests.

For example, setting the request's `Content-Type` to `"application/json"` will prevent it from being treated as a simple request:

```javascript
fetch("https://my-bank.example.org/transfer", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ recipient: "joe", amount: "100" }),
});
```

Similarly, setting a custom header on the request will prevent it being treated as a simple request:

```javascript
fetch("https://my-bank.example.org/transfer", {
  method: "POST",
  headers: {
    "X-MY-BANK-ANTI-CSRF": 1,
  },
  body: JSON.stringify({ recipient: "joe", amount: "100" }),
});
```

#### CORS Consideration

The Cross-Origin Resource Sharing (CORS) protocol allows a website to relax restrictions on non-simple requests. Your website will be vulnerable to a CSRF attack from a particular origin if its response to a state-changing request includes:

- The `Access-Control-Allow-Origin` response header, and the header lists the sender's origin
- The `Access-Control-Allow-Credentials` response header

### 4. Defense in Depth: SameSite Cookies

The `SameSite` cookie attribute provides some protection against CSRF attacks. It's not a complete defense, and is best considered as an addition to one of the other defenses, providing defense in depth.

This attribute controls when a browser is allowed to include the cookie in a cross-site request. It has three possible values: `None`, `Lax`, and `Strict`.

**Strict**: The browser will not include the cookie in any cross-site request. However, this creates a usability issue: if the user is logged into your site and follows a link to your site from a different site, then your cookies will not be included.

**Lax**: Cookies are included in cross-site requests if both the following conditions apply:
- The request was a navigation of the top-level browsing context.
- The request used a safe method: notably, `GET` is safe but `POST` is not.

**Recommendation**: Use `Lax` for cookies used to decide if a logged-in user should be shown a page, and `Strict` for cookies used for state-changing requests.

**Limitation**: The `SameSite` attribute protects you from requests from a different site, not a different origin. For example, `https://foo.example.org` and `https://bar.example.org` are considered the same site, although they are different origins.

## Defense Summary Checklist

- Understand where in your website you are implementing state-changing requests that use session cookies to check which user issued the request.
- Implement at least one of the primary defenses:
  - If you are using `<form>` elements to issue these requests, ensure you are using a web framework with support for CSRF tokens, and use it.
  - If you are using JavaScript APIs like `fetch()` or `XMLHttpRequest` to issue state-changing requests, ensure that they are not simple requests.
  - Whichever mechanism you use to issue requests, consider using Fetch metadata to disallow cross-site requests.
- Avoid using the `GET` method to issue state-changing requests.
- Set the `SameSite` attribute for session cookies to `Strict` if you can, or `Lax` if you have to.
