# The Twelve-Factor App: XI. Logs

Source: https://12factor.net/logs

## Treat logs as event streams

Logs constitute "the stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services." Raw logs typically appear as text with one event per line. Unlike files with defined boundaries, logs flow continuously throughout the application's operation.

## Core Principle

"A twelve-factor app never concerns itself with routing or storage of its output stream." Applications should refrain from managing logfiles directly. Instead, each process writes its event stream **unbuffered to `stdout`**.

During local development, developers observe this stream in their terminal. In staging and production, the execution environment captures all process streams, combines them, and routes them to designated destinations — completely outside the application's control.

## Log Analysis Capabilities

Log streams can be:
- Directed to files or monitored in real-time via `tail -f`
- Sent to indexing systems like Splunk or Elasticsearch
- Routed to data warehousing platforms such as Hadoop/Hive

These systems enable:
- Retrieving specific historical events
- Analyzing trends at scale
- Implementing automated alerts based on custom thresholds
