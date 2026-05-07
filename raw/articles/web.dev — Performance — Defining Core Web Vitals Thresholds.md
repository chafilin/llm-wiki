# How the Core Web Vitals Metrics Thresholds Were Defined

Source: https://web.dev/articles/defining-core-web-vitals-thresholds

Authors: Bryan McQuade, Barry Pollard

## Overview

The three Core Web Vitals metrics each have established performance thresholds based on research methodology balancing quality of experience, achievability, and device considerations.

## The Three Core Web Vitals Metrics

| Metric | Purpose | Good | Poor | Percentile |
|--------|---------|------|------|-----------|
| **LCP** | Perceived load speed | ≤2500 ms | >4000 ms | 75th |
| **INP** | Responsiveness | ≤200 ms | >500 ms | 75th |
| **CLS** | Visual stability | ≤0.1 | >0.25 | 75th |

Sites are classified as "good" when at least 75% of page views meet the threshold; classified as "poor" when 25%+ meet the poor threshold.

## Threshold Selection Criteria

### High-Quality User Experience

Thresholds align with human perception research and HCI principles. The researchers acknowledge "perception thresholds vary depending on user and context."

### Achievability for Existing Content

A minimum of **10% of origins must meet "good" thresholds** to ensure they're practical, not aspirational. The "poor" threshold typically affects 10-30% of origins.

### Device Considerations

The same thresholds apply to both mobile and desktop. Mobile is often the majority of traffic for most sites.

## Why the 75th Percentile?

The 75th percentile balances ensuring "a majority of visits" experience target performance while minimizing outlier impact.

## Largest Contentful Paint (LCP)

Research on user attention spans informed the LCP threshold. Card and Miller describe response time expectations as "roughly from ~0.3sec to ~3sec."

### Achievability Data (April 2020)

| Threshold | Phone | Desktop |
|-----------|-------|---------|
| 1 second | 3.5% | 6.9% |
| 2 seconds | 27% | 36% |
| 2.5 seconds | 42% | 51% |
| 3 seconds | 55% | 64% |

The 2.5-second threshold was "consistently achievable" while meeting the 10% minimum pass rate.

**Final LCP Thresholds:** Good ≤2500 ms | Poor >4000 ms

## Interaction to Next Paint (INP)

Research demonstrates "delays in visual feedback of up to around 100 ms are perceived as being caused by an associated source." Delays over 200 ms break the perceived causal link between action and response.

### Achievability Considerations

| Threshold | Top 10K Phone | Top 10K Desktop |
|-----------|---------------|-----------------|
| 200 ms | 77% | 17% |
| 300 ms | 55% | 8% |
| 500 ms | 24% | 2% |

The 500 ms poor threshold better accommodates popular sites (which tend to be more complex) while maintaining the 10-30% poor classification range.

**Final INP Thresholds:** Good ≤200 ms | Poor >500 ms

## Cumulative Layout Shift (CLS)

Since CLS was a novel metric without existing research foundation, the team evaluated real-world pages. "Levels of shift from 0.15 and higher were consistently perceived as disruptive, while shifts of 0.1 and lower were noticeable but not excessively disruptive."

The 0.1 threshold "strikes a better balance between quality of experience and achievability," with practical constraints from third-party embedded content that causes unavoidable layout shifts.

### Poor Threshold Data (April 2020)

At 0.25, approximately 20% would be classified as poor — fitting the target 10-30% range.

**Final CLS Thresholds:** Good ≤0.1 | Poor >0.25

## Key Methodological Insights

The authors acknowledge that "the criteria were sometimes in conflict with one another" and that "there is often no single 'correct' threshold." Their approach prioritized asking "which candidate threshold best achieves our criteria?" rather than seeking perfect precision.

"Many sites would benefit from optimizing even beyond the 'good' thresholds and should seek to correlate with their individual business metrics."
