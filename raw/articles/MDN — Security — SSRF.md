# Server Side Request Forgery (SSRF)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/SSRF

**Server‑Side Request Forgery (SSRF)** is a vulnerability that allows an attacker to make network requests to arbitrary destinations. SSRF makes these requests originate from within a server itself, which typically has broader access than an external client.

## Example Scenario

Suppose your application has an endpoint that fetches images from a provided URL:

```http
GET /fetch-image?url=https://example.com/image.png
```

The server has access to the company's intranet.

If the server does not validate the URL parameter, then the client can extract sensitive data by passing intranet URLs to the API:

```javascript
fetch("https://example.org/fetch-image?url=http://localhost:443/admin/org.png");
```

Although the client could not access `http://localhost:443/` directly, the server can, and the server relays the response to the client.

The client doesn't have to make HTTP requests: it might be able to use the `file://` protocol:

```javascript
fetch("https://example.org/fetch-image?url=file:///etc/passwd");
```

In these cases the attacker could get access to sensitive data. Sometimes the attacker does not get the response body, but it can still cause problems:

* By forcing the server to make many requests an attacker can execute a Denial of Service (DoS) attack.
* By examining the status code returned by the server or the time taken to execute requests, the attacker may infer sensitive information about the target.

Attackers may use redirects or redirect chains to evade validation.

## Defenses Against SSRF

### Input Validation and Allow-listing

Restrict the URLs that the server API will use. For example, the `fetch-image` service discussed above could specify an allow list containing the expected domains:

```javascript
const ALLOWED_DOMAINS = ["https://api.example.com", "https://cdn.example.com"];
```

### Blocking Protocols and URL Schemes

Ensure only specific URL schemes are allowed. Most likely only allowing `https://` is enough for regular web applications.

### Redirect Validation

Do not follow redirects automatically and also enforce input validation and/or allow-listing to redirected URLs. Limit redirect chains.

### Least Privilege and Isolation

Ensure the service making outbound requests does not run with any more privileges than it needs, and avoid co-locating request-capable services with sensitive internal services.

## Defense Summary Checklist

* Review all features that fetch resources and validate or allow-list user inputs.
* Block all protocols except for HTTPS.
* Beware of URL redirections and limit redirect chains.
* Apply the principle of least privilege for server network permissions: ideally servers should not have unrestricted access to internal networks unless required.
* Log and monitor requests.
