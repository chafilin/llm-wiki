# Secure Contexts

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Secure_Contexts

A **secure context** is a `Window` or `Worker` for which certain minimum standards of authentication and confidentiality are met. Many Web APIs and features are accessible only in a secure context. The primary goal of secure contexts is to prevent MITM attackers from accessing powerful APIs that could further compromise the victim of an attack.

## Why Should Some Features Be Restricted?

Some APIs on the web are very powerful, giving an attacker the ability to:

- Invade a user's privacy.
- Get low-level access to a user's computer.
- Get access to data such as user credentials.

## When Is a Context Considered Secure?

A context is considered secure when it meets certain minimum standards of authentication and confidentiality defined in the Secure Contexts specification. A particular document is considered to be in a secure context when it is the active document of a top-level browsing context that is a secure context.

For example, even for a document delivered over TLS within an `<iframe>`, its context is **not** considered secure if it has an ancestor that was not also delivered over TLS.

Resources that are not local, to be considered secure, must meet the following criteria:

- They must be served over `https://` URLs.
- The security properties of the network channel used to deliver the resource must not be considered deprecated.

## Potentially Trustworthy Origins

A **potentially trustworthy origin** is one that the browser can generally trust to deliver data security.

Locally-delivered resources such as those with `http://127.0.0.1`, `http://localhost`, and `http://*.localhost` URLs are not delivered using HTTPS, but they can be considered to have been delivered securely because they are on the same device as the browser.

The same is generally true for `file://` URLs.

Secure WebSocket (`"wss://"`) URLs are also considered potentially trustworthy.

## Feature Detection

Pages can use feature detection to check whether they are in a secure context or not by using the `Window.isSecureContext` boolean:

```javascript
if (window.isSecureContext) {
  // Page is a secure context so service workers are now available
  navigator.serviceWorker.register("/offline-worker.js").then(() => {
    // …
  });
}
```

## See Also

- `Window.isSecureContext` and `WorkerGlobalScope.isSecureContext`
- [Strict-Transport-Security](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Strict-Transport-Security) HTTP header
