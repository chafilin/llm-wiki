# The Twelve-Factor App

Source: https://12factor.net/

Author: Adam Wiggins (Last updated 2017)

## Introduction

The Twelve-Factor App is a methodology for building software-as-a-service applications that:

- Use **declarative** formats for setup automation, to minimize time and cost
- Maintain a clean contract with the operating system for maximum portability
- Deploy easily on modern cloud platforms
- Minimize differences between development and production environments
- Scale effectively without major architectural changes

The methodology applies to apps in any programming language using various backing services.

## The Twelve Factors

| # | Factor | Description |
|---|--------|-------------|
| I | Codebase | One codebase tracked in revision control, many deploys |
| II | Dependencies | Explicitly declare and isolate dependencies |
| III | Config | Store config in the environment |
| IV | Backing Services | Treat backing services as attached resources |
| V | Build, Release, Run | Strictly separate build and run stages |
| VI | Processes | Execute the app as one or more stateless processes |
| VII | Port Binding | Export services via port binding |
| VIII | Concurrency | Scale out via the process model |
| IX | Disposability | Maximize robustness with fast startup and graceful shutdown |
| X | Dev/Prod Parity | Keep development, staging, and production as similar as possible |
| XI | Logs | Treat logs as event streams |
| XII | Admin Processes | Run admin/management tasks as one-off processes |
