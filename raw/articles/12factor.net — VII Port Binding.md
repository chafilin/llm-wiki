# The Twelve-Factor App: VII. Port Binding

Source: https://12factor.net/port-binding

## Export services via port binding

Traditional web applications often run within a webserver container — PHP modules in Apache HTTPD or Java apps in Tomcat. The twelve-factor methodology rejects this pattern. Instead, applications should be "completely self-contained" and handle their own HTTP serving by binding to a port and listening for incoming requests.

## How It Works

During local development, developers access services through URLs like `http://localhost:5000/`. In production, a routing layer directs public requests to the port-bound processes.

This is achieved by including webserver libraries directly in the application code using dependency management tools. Examples include Tornado (Python), Thin (Ruby), and Jetty (Java). The entire responsibility sits within the application itself.

## Beyond HTTP

Port binding extends beyond HTTP services. Nearly any server software can operate this way, including ejabberd (XMPP protocol) and Redis (Redis protocol).

## Composability

This approach enables applications to become backing services for other applications by sharing their port binding URLs through configuration, creating flexible service dependencies.
