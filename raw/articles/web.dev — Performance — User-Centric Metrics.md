# User-Centric Performance Metrics

Source: https://web.dev/articles/user-centric-performance-metrics

## Overview

Performance measurement requires precision and relevant metrics. As Philip Walton explains, "performance is relative" depending on user circumstances like network speed and device capability.

## Key Framework Questions

Performance evaluation centers on four essential inquiries:

- **Is it happening?** Navigation started and server responded
- **Is it useful?** Sufficient content rendered for user engagement
- **Is it usable?** Page responds to interaction without delays
- **Is it delightful?** Interactions remain smooth and lag-free

## Measurement Approaches

**Laboratory Testing**: Controlled environments simulate page loads before production release, preventing performance regressions during development.

**Field Measurement**: Real User Monitoring (RUM) captures actual performance data from genuine users with varied devices and network conditions, revealing variations that lab testing cannot detect.

## Performance Metric Categories

The article identifies five distinct metric types:

1. **Perceived load speed** – visual content rendering velocity
2. **Load responsiveness** – JavaScript execution for component interaction
3. **Runtime responsiveness** – post-load interaction speed
4. **Visual stability** – unexpected element shifting prevention
5. **Smoothness** – consistent animation frame rates

## Core Metrics to Monitor

| Metric | Measurement | Application |
|--------|-------------|-------------|
| **First Contentful Paint (FCP)** | Initial content render time | Lab, Field |
| **Largest Contentful Paint (LCP)** | Main content element render | Lab, Field |
| **Interaction to Next Paint (INP)** | User interaction latency | Lab, Field |
| **Total Blocking Time (TBT)** | Main thread blocking duration | Lab |
| **Cumulative Layout Shift (CLS)** | Unexpected layout changes | Lab, Field |
| **Time to First Byte (TTFB)** | Network response initiation | Lab, Field |

## Custom Metrics Development

For site-specific performance requirements, standardized lower-level APIs enable tailored measurement:

- User Timing API
- Long Tasks API
- Long Animation Frames API
- Element Timing API
- Navigation Timing API
- Resource Timing API
- Server Timing

The article emphasizes that "no single metric is sufficient" for comprehensive performance evaluation.
