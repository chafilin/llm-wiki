# Getting Started with Measuring Web Vitals

Source: https://web.dev/articles/vitals-measurement-getting-started

Author: Katie Hempenius

## Overview

Establishing a Web Vitals measurement strategy requires data collection from both real-world and lab environments.

## Measuring Web Vitals with Real User Monitoring (RUM)

### Initial Steps

RUM data (field data) reflects actual user experiences. Google uses RUM data to evaluate whether sites meet Core Web Vitals thresholds.

**Recommended starting tools:**

- **Chrome DevTools**: Performance panel integrates Chrome User Experience Report (CrUX) data for comparison between local and real-user experiences
- **PageSpeed Insights (PSI)**: Reports aggregate performance metrics over 28 days at page and origin levels
- **Search Console**: Per-page performance data with historical tracking; requires site ownership verification
- **CrUX Vis**: Dashboard displaying CrUX historical data with additional details like navigation types and LCP subparts

**Important note**: CrUX-based sources report monthly granularity data. PSI and Search Console show past 28-day performance.

### The web-vitals JavaScript Library

For DIY RUM implementation, the `web-vitals` library (~2KB) provides convenient APIs without requiring manual implementation of underlying browser APIs.

### Data Interpretation

Performance distributions often reveal wide variation among users. Web Vitals evaluation focuses on the 75th percentile — requiring **75% of page visits** to meet "good" thresholds.

## Measuring Web Vitals with Lab Data

Lab (synthetic) data comes from controlled environments, enabling pre-production testing and CI/CD integration.

### Key Considerations

**Largest Contentful Paint (LCP)**: Lab measurements differ from field measurements due to loading delays, varying content across screen sizes, and factors like cookie banners.

**Cumulative Layout Shift (CLS)**: Lab environments typically measure only initial page load, producing artificially lower CLS than field data.

**Interaction to Next Paint (INP)**: Cannot be measured in labs because it requires actual user interactions. Total Blocking Time (TBT) serves as the recommended lab proxy.

### Lab Testing Tools

- **Chrome DevTools Performance panel**: Real-time Core Web Vitals feedback during development
- **Lighthouse**: Reports LCP, CLS, and TBT with optimization recommendations; available in DevTools, as npm package, and via Lighthouse CI
- **WebPageTest**: Web Vitals reporting under specific device and network conditions
