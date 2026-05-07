---
title: Better Web Video with AV1 Codec
type: source
raw: raw/articles/Evil Martians — Better Web Video with AV1 Codec.md
date_ingested: 2026-05-07
tags: []
---

## Summary

Practical guide to replacing H.264 video and GIF animations with AV1-encoded video on the web. AV1 files are 30–50% smaller than H.264 at equivalent quality, and 20–40× smaller than GIF. The strategy is a two-source `<video>` element: AV1 first for modern browsers, H.264 fallback for everything else. Includes exact ffmpeg commands and parameter explanations. Updated February 2025 to recommend SVT-AV1 encoder.

## Key takeaways

- **AV1 vs H.264**: 30–50% smaller files at comparable quality; YouTube and Netflix have adopted it; hardware decode requires iPhone 15+, M3 Mac, or modern desktop — older devices fall back gracefully
- **Two-version strategy**: `<source src="video.av1.mp4" type="video/mp4; codecs=av01.0.05M.08,opus">` first, then H.264 fallback — browsers pick the first supported source
- **GIF replacement**: `<video autoplay loop muted playsinline>` replicates GIF behavior; no JS needed; 20–40× size reduction
- **Recommended encoder**: `libsvtav1` (SVT-AV1) — faster than `libaom-av1`, the previous recommendation
- **Key ffmpeg flags**: `-qp 30` (quality), `-movflags +faststart` (streaming before full download), `-pix_fmt yuv420p` (compatibility), `-tile-columns 2 -tile-rows 2` (AV1 encoding speed)
- **Codec ≠ container**: `.mp4` is just the wrapper; the actual compression is determined by the codec (`libx264`, `libsvtav1`, etc.)

## Connections

[[Web Performance]] [[Web Security]]

## Quotes

> "Twenty to forty times smaller" when replacing GIFs with modern video formats.
