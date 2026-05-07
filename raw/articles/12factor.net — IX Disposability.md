# The Twelve-Factor App: IX. Disposability

Source: https://12factor.net/disposability

## Maximize robustness with fast startup and graceful shutdown

The twelve-factor app's processes are *disposable* — capable of being initiated or terminated instantly. This enables rapid elastic scaling, swift deployment of code or configuration updates, and improved resilience in production environments.

## Fast Startup

Processes should become operational within seconds of executing the launch command, ready to handle requests or work assignments. Quick initialization improves deployment agility, scaling responsiveness, and system reliability.

## Graceful Shutdown

When receiving a SIGTERM signal from the process manager, processes must shut down gracefully:

**For web processes:**
1. Stop accepting new requests at the service port
2. Allow existing requests to complete
3. Then terminate

The model assumes HTTP requests are brief (seconds or less). Long-polling clients should seamlessly reconnect upon disconnection.

**For worker processes:**
- Return the current job to the work queue
- RabbitMQ: send a NACK
- Beanstalkd: automatic queue return upon disconnect
- Lock-based systems: release job locks

All jobs must be **reentrant** — typically achieved through transaction wrapping or idempotent operations.

## Robustness Against Sudden Failure

Processes should withstand abrupt termination from hardware failures. Robust queueing backends (like Beanstalkd) that return jobs upon client disconnection or timeout provide practical solutions. Twelve-factor apps embody **crash-only design** principles.
