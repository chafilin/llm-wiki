# The Twelve-Factor App: VI. Processes

Source: https://12factor.net/processes

## Execute the app as one or more stateless processes

**Twelve-factor processes maintain statelessness and share-nothing architecture.** Persistent data must be stored in a stateful backing service, typically a database.

## Why Statelessness Matters

The process's memory space or filesystem can serve as a brief, single-transaction cache (e.g., downloading a file, processing it, storing results in a database). But the twelve-factor approach assumes that "anything cached in memory or on disk will be available on a future request" is unreliable — with multiple running processes, subsequent requests likely route to different instances. Even single-process deployments see state wiped during restarts from code updates, configuration changes, or infrastructure relocation.

## Sticky Sessions Violation

Certain web systems use "sticky sessions" — storing user sessions in process memory and routing repeat requests to the same instance. This violates twelve-factor principles and should be avoided. For session data, use time-expiring datastores like Memcached or Redis.

## Asset Packaging

Asset packaging tools that cache compiled assets on disk violate this principle. Twelve-factor apps prefer compiling during the build stage. Tools such as Jammit and the Rails asset pipeline support build-stage packaging.
