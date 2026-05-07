# The Twelve-Factor App: IV. Backing Services

Source: https://12factor.net/backing-services

## Treat backing services as attached resources

A backing service refers to any external service consumed over the network during normal application operation. These include datastores like MySQL or CouchDB, messaging systems such as RabbitMQ, email services like Postfix, and caching systems such as Memcached.

## Local vs. Third-Party Services

While traditionally managed locally by system administrators, applications may also depend on third-party services: SMTP providers like Postmark, monitoring tools such as New Relic, cloud storage like Amazon S3, and API services including Twitter and Google Maps.

## Key Principle

"The code for a twelve-factor app makes no distinction between local and third party services." Both types function as attached resources, with configuration details stored in the app's config. This abstraction enables swapping implementations without code changes — for instance, replacing a local MySQL database with Amazon RDS or substituting a local SMTP server with Postmark.

## Resource Management

Each distinct backing service qualifies as a separate resource. Multiple databases serving sharding purposes count as two distinct resources. These services demonstrate loose coupling to their deployment, allowing administrators to attach and detach resources dynamically. A malfunctioning database can be replaced with a restored backup without any code modifications.
