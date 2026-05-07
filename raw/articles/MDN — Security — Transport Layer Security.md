# Transport Layer Security (TLS)

Source: https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Transport_Layer_Security

Transport Layer Security (TLS) is a protocol which enables a client to communicate securely with a server across an untrusted network. Most notably it's used to secure HTTP connections on the web: the resulting protocol is called HTTPS.

## How TLS Secures Connections

TLS secures a network connection in three ways:

- **Encryption**: the data exchanged between client and server is encrypted while in transit, so it can't be read by any attackers.
- **Integrity**: an attacker can't secretly modify data (without detection) while it is in transit between client and server.
- **Authentication**: client and server are each able to prove to the other party that they are the entity they claim to be. On the web, servers usually authenticate themselves to clients, but clients don't usually authenticate themselves to servers.

In particular, HTTPS is the defense against a Manipulator in the Middle (MITM) attack.

**All websites should serve all their pages and subresources over HTTPS, and implement server authentication.**

## TLS Handshake

When a client connects to a server using TLS, an initial _handshake_ sets the security parameters for the protocol:

- Client and server agree on which version of TLS to use. The current version of TLS is 1.3, and this is the most widely-used version. TLS 1.2 is still used by some websites, and TLS 1.1 and 1.0 should no longer be used.
- Client and server agree on the cipher suite that they will use: this defines the algorithms that they will use for key agreement, authentication, encryption, and message authentication.
- Client and server authenticate each other (optionally).
- Client and server agree on a secret key that they will use to encrypt and decrypt messages.

## Configuring TLS

Choosing the right TLS server configuration has a big impact on the security of the connection. In particular, it determines the TLS version and cryptographic algorithms that will be used. If you need to configure your own server, consult a resource such as Mozilla's [TLS Recommended Configurations](https://wiki.mozilla.org/Security/Server_Side_TLS#Recommended_configurations).

Mozilla also provides a [TLS configuration generator](https://ssl-config.mozilla.org/) that will generate configuration files for a wide range of web servers.

## Server Authentication

To support server authentication, your website must have a **digital certificate**, which contains a digitally signed copy of the public key. This binds the website's keys to their domain name, so the browser knows that it really is connecting to, for example, `https://example.com`.

[Let's Encrypt](https://letsencrypt.org/) is a widely used nonprofit Certification Authority which issues free TLS certificates.

## Mixed Content

A website should use HTTPS not only for the main document, but also for all subresources that it loads, such as scripts, stylesheets, images, and fonts.

## Upgrading HTTP Connections

Even if a site is only served over HTTPS, users may still request it over HTTP: for example, by typing `http://example.org` into the address bar. To enable the site to work in cases like this, listen for HTTP requests and use a **301 Moved Permanently** response to redirect to the HTTPS version.

To reduce the risk of SSL stripping attacks, the server should also send the `Strict-Transport-Security` HTTP response header (HSTS): this informs clients that the site wishes them to use HTTPS, and will cause the browser to connect using HTTPS directly for any subsequent visits.

With HSTS, SSL stripping is prevented except for the first time the browser tries to connect to your site. Chrome maintains a list of domains called the [HSTS preload list](https://hstspreload.org/) to protect even first-time connections.

## See Also

- [Mozilla HTTP Observatory](https://observatory.mozilla.org/)
- [SSL Labs](https://www.ssllabs.com/ssltest/)
- [Mozilla recommended TLS configurations](https://ssl-config.mozilla.org/)
