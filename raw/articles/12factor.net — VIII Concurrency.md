# The Twelve-Factor App: VIII. Concurrency

Source: https://12factor.net/concurrency

## Scale out via the process model

Twelve-factor applications adopt the Unix daemon service model, allowing developers to organize work by assigning different tasks to specific process types:

- **Web processes** handle HTTP requests
- **Worker processes** manage long-running background jobs

"In the twelve-factor app, processes are a first class citizen."

## Process Execution Models Comparison

Different frameworks handle processes distinctly. PHP typically runs child processes under Apache, spawned on-demand based on traffic. Java takes the opposite approach, with a single JVM reserving substantial resources upfront and managing concurrency internally through threads.

Individual processes may still use internal multiplexing through runtime threads or async patterns (EventMachine, Twisted, Node.js), but applications must ultimately span multiple processes across machines for true scalability.

## Scaling and Process Formation

The share-nothing architecture enables straightforward horizontal scaling. The collection of process types and their respective counts comprises the **process formation**.

## Process Management

Twelve-factor applications should avoid daemonizing or creating PID files. Instead, rely on external process managers like systemd, cloud platform tools, or Foreman to handle output streams, restart crashed processes, and manage shutdowns.
