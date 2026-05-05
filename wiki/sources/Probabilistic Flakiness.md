---
title: Probabilistic Flakiness
type: source
raw: raw/articles/Probabilistic Flakiness.md
date_ingested: 2026-05-04
tags: [flaky-tests, meta, bayesian, probabilistic, ci, measurement]
---

## Summary
Meta's reframing of flaky test detection: instead of asking "is this test flaky?" (binary), ask "how flaky is it?" (spectrum). They compute a Probabilistic Flakiness Score (PFS) using Bayesian inference on existing CI execution data — no extra test runs required. The score is used both as a dashboard metric and as an enforcement gate: flaky tests lose eligibility for predictive test selection.

## Key takeaways
- Binary flakiness detection is wrong. Flakiness is a spectrum; you need a score to prioritize and track trends.
- Asymmetry observation: developers retry failing tests on the same code, creating a natural signal — "fail then pass" sequences are flakiness, not regression.
- Two-parameter Bayesian model: probability of "bad state" (real failure) + probability of failure in "good state" (the flakiness signal). Uses Stan for inference.
- No extra CI runs needed — the model works entirely from existing execution telemetry.
- Consequence-driven improvement: losing eligibility for predictive test selection is a meaningful cost that drives teams to fix flakiness.

## Connections
[[Flaky Tests]] [[Testing Philosophy]] [[Software Development]]

## Quotes
> "Rather than asking whether tests are flaky, Meta's approach answers: how flaky are they?"
