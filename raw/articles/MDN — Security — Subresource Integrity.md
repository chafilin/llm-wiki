# Subresource Integrity (SRI)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Subresource_Integrity

**Subresource Integrity** (SRI) is a security feature that enables browsers to verify that resources they fetch (for example, from a CDN) are delivered without unexpected manipulation. It works by allowing you to provide a cryptographic hash that a fetched resource must match.

## How Subresource Integrity Helps

Websites often rely on third parties such as Content Delivery Networks (CDNs) to host resources. This creates a risk: if an attacker gains control of the third-party host, they can inject malicious content or replace files entirely. This is called a **supply chain attack**.

Subresource Integrity defends against such attacks by ensuring that fetched files have exactly the contents you expect them to have.

## Using Subresource Integrity

You can use SRI with:
- `<script>` elements
- `<link>` elements with `rel` attribute values of `stylesheet`, `preload`, or `modulepreload`

### Setting the `integrity` Attribute

Add the `integrity` attribute to the element. The value is a whitespace-separated list of cryptographic hashes, where each hash is prefixed with an algorithm identifier:

```html
<script
  src="https://cdn.example.com/script.js"
  integrity="sha384-Tk2Yjg3YmYzMWNkZTdhMTFkM2FlNDg4ZjE3MzEzNTk3ZDlh"
  crossorigin="anonymous"></script>
```

**Allowed hash algorithm prefixes:** `sha256`, `sha384`, `sha512`

### How Browsers Handle SRI

When a browser encounters an element with an `integrity` attribute:

1. It selects the **strongest hash function present** (SHA-512 > SHA-384 > SHA-256)
2. It calculates the hash of the downloaded resource using that function
3. It compares the result with the specified values
4. If any value matches, the resource is loaded; otherwise, a network error is returned

## Subresource Integrity and CORS

Cross-origin requests using SRI must use the CORS protocol. The server must send appropriate `Access-Control-Allow-Origin` headers.

You **must** include the `crossorigin` attribute:

```html
<script
  src="https://cdn.example.com"
  integrity="sha512-abcde"
  crossorigin="anonymous"></script>
```

## Tools for Generating SRI Hashes

### Online Tool
- [SRI Hash Generator](https://srihash.org/)

### Using OpenSSL

```bash
cat FILENAME.js | openssl dgst -sha384 -binary | openssl base64 -A
```

### Using shasum

```bash
shasum -b -a 384 FILENAME.js | awk '{ print $1 }' | xxd -r -p | base64
```
