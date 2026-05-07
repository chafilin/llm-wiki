# Same-origin Policy

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Same-origin_policy

The **same-origin policy** is a critical security mechanism that restricts how a document or script loaded by one origin can interact with a resource from another origin.

It helps isolate potentially malicious documents, reducing possible attack vectors. For example, it prevents a malicious website on the Internet from running JS in a browser to read data from a third-party webmail service (which the user is signed into) or a company intranet.

## Definition of an origin

Two URLs have the _same origin_ if the protocol, port (if specified), and host are the same for both. You may see this referenced as the "scheme/host/port tuple".

The following table gives examples of origin comparisons with the URL `http://store.company.com/dir/page.html`:

| URL | Outcome | Reason |
|-----|---------|--------|
| `http://store.company.com/dir2/other.html` | Same origin | Only the path differs |
| `http://store.company.com/dir/inner/another.html` | Same origin | Only the path differs |
| `https://store.company.com/page.html` | Failure | Different protocol |
| `http://store.company.com:81/dir/page.html` | Failure | Different port |
| `http://news.company.com/dir/page.html` | Failure | Different host |

## Cross-origin network access

The same-origin policy controls interactions between two different origins. These interactions are typically placed into three categories:

- Cross-origin _writes_ are typically allowed. Examples are links, redirects, and form submissions.
- Cross-origin _embedding_ is typically allowed.
- Cross-origin _reads_ are typically disallowed, but read access is often leaked by embedding.

Here are some examples of resources which may be embedded cross-origin:

- JavaScript with `<script src="…"></script>`
- CSS applied with `<link rel="stylesheet" href="…">`
- Images displayed by `<img>`
- Media played by `<video>` and `<audio>`
- External resources embedded with `<object>` and `<embed>`
- Fonts applied with `@font-face`
- Anything embedded by `<iframe>`

### How to allow cross-origin access

Use CORS to allow cross-origin access. CORS is a part of HTTP that lets servers specify any other hosts from which a browser should permit loading of content.

### How to block cross-origin access

- To prevent cross-origin writes, check an unguessable token in the request — known as a CSRF token.
- To prevent cross-origin reads of a resource, ensure that it is not embeddable.
- To prevent cross-origin embeds, ensure that your resource cannot be interpreted as one of the embeddable formats listed above.

## Cross-origin script API access

JavaScript APIs like `iframe.contentWindow`, `window.parent`, `window.open`, and `window.opener` allow documents to directly reference each other. When two documents do not have the same origin, these references provide very limited access to `Window` and `Location` objects.

To communicate between documents from different origins, use `window.postMessage`.

## Cross-origin data storage access

Access to data stored in the browser such as Web Storage and IndexedDB are separated by origin. Each origin gets its own separate storage, and JavaScript in one origin cannot read from or write to the storage belonging to another origin.

Cookies use a separate definition of origins. A page can set a cookie for its own domain or any parent domain, as long as the parent domain is not a public suffix.
