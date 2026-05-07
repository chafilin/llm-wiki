# Transport Layer Security (TLS) Configuration

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Practical_implementation_guides/TLS

Transport Layer Security (TLS) provides assurances about the confidentiality, authenticity, and integrity of all communications, and should be used for all inbound and outbound website communications.

## TLS Configuration

### Problem
If data is sent over the web unencrypted, it can be intercepted by third parties in a MITM attack.

### Solution
Set up your server software to use a secure configuration that enforces HTTPS with safe TLS settings. The Mozilla [SSL Configuration Generator](https://ssl-config.mozilla.org/) provides several options based on Mozilla's TLS guidelines.

## Resource Loading

### Problem
Secure websites that load active resources (like JavaScript) over HTTP will be blocked by browsers and cause mixed content warnings.

### Solution
Verify that all resources are loaded over HTTPS prior to deployment.

**Correct:**
```html
<script src="https://code.jquery.com/jquery-1.12.0.min.js"></script>
```

## HTTP Redirection

### Solution
Sites that listen on port 80 should redirect to the same resource on HTTPS.

**NGINX Example:**
```nginx
server {
  listen 80;
  return 301 https://$host$request_uri;
}
```

**Apache Example:**
```apacheconf
<VirtualHost *:80>
  ServerName site.example.org
  Redirect permanent / https://site.example.org/
</VirtualHost>
```

## HTTP Strict Transport Security (HSTS)

### Problem
To prevent MITM attacks, browsers should only connect to sites via HTTPS.

### Solution
HTTP `Strict-Transport-Security` (HSTS) header notifies browsers to connect to a given site only over HTTPS.

**Supported Directives:**
- **`max-age`** - Duration (in seconds) for HTTPS redirects
- **`includeSubDomains`** (optional) - Upgrade requests on all subdomains
- **`preload`** (optional) - Include site in HSTS preload list

### Implementation Steps
1. Set `max-age` to at least 6 months (`15768000`); 2 years (`63072000`) recommended
2. If possible, set `includeSubDomains` to improve security on all subdomains
3. If possible, set `preload` for inclusion in the HSTS preload list at [https://hstspreload.org/](https://hstspreload.org/)

**Examples:**

Basic HSTS for 2 years:
```http
Strict-Transport-Security: max-age=63072000
```

With subdomains and preload:
```http
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

Also set `upgrade-insecure-requests` CSP:
```http
Content-Security-Policy: upgrade-insecure-requests;
```
