# Cross-Origin Resource Policy (CORP)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Practical_implementation_guides/CORP

Cross-Origin Resource Policy (CORP) is set by the `Cross-Origin-Resource-Policy` response header, which lets websites and applications opt-in to protection against certain cross-origin requests.

## Problem

Some side-channel hardware vulnerabilities (also known as Cross-site leaks, or XS-Leaks), such as [Meltdown](https://en.wikipedia.org/wiki/Meltdown_(security_vulnerability)) and [Spectre](https://en.wikipedia.org/wiki/Spectre_(security_vulnerability)), exploit a race condition arising as part of speculative execution functionality of modern processors. This functionality is designed to improve performance but can be manipulated to disclose sensitive data.

## Solution

Use `Cross-Origin-Resource-Policy` to block `no-cors` cross-origin requests to given resources. As this policy is expressed via a response header, the actual request is not prevented. Instead, the browser prevents the result from being leaked by stripping out the response body.

### Possible Values

| Value | Description |
|-------|-------------|
| **`same-origin`** | Limits resource access to requests coming from the same origin. Recommended for URLs that reply with sensitive user information or private APIs. |
| **`same-site`** | Limits resource access to requests coming from the same site. Recommended for responses from origins whose functionality is shared across several other same-site origins (e.g., company CDN, single sign-on apps). |
| **`cross-origin`** | Allows resources to be accessed by cross-origin requests. Recommended only for responses from widely-used origins, such as public CDNs or widgets. This is the default value if `Cross-Origin-Resource-Policy` is not set. |

**Best practice:** Set the most restrictive value possible for your site.

## Examples

### Disallow Cross-Origin Requests

```http
Cross-Origin-Resource-Policy: same-origin
```

Instructs browsers to disallow cross-origin requests made in `no-cors` mode.

### Allow Cross-Origin Access with Enhanced Protection

```http
Cross-Origin-Resource-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp
```

Instructs browsers to allow cross-origin resource access, including access to features with unthrottled timers (such as `SharedArrayBuffer` objects or `Performance.now()`).

## See Also

- [Consider deploying Cross-Origin Resource Policy](https://resourcepolicy.fyi/)
- [XS-Leaks Wiki](https://xsleaks.dev/)
- `Cross-Origin-Embedder-Policy`
- `Cross-Origin-Opener-Policy`
