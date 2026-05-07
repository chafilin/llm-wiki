# How to Make Web Videos Smaller in 2025 Using the AV1 Codec

Source: https://evilmartians.com/chronicles/better-web-video-with-av1-codec

## Overview

The AV1 video codec offers substantial file size reduction for web videos — files "twenty to forty times smaller" when replacing GIFs with modern video formats, while maintaining quality comparable to or better than H.264.

## Key Technical Concepts

### Codecs vs. Containers

File extensions like `.mp4` indicate only the container format. Each video file actually contains three distinct components:

1. **Video codecs** (H.264, HEVC, VP9, AV1) — compress video data
2. **Audio codecs** (MP3, Opus, AAC) — compress audio data
3. **Containers** (MP4, MOV, WebM) — package both streams together

### Why AV1?

The AV1 codec, released in March 2018, generates files "up to 30–50% smaller than H.264" while maintaining superior quality at low bitrates. Major platforms including YouTube and Netflix have adopted it.

**Trade-offs:**
- Slower encoding due to complex algorithms
- Limited device support (primarily newer iPhones 15+, M3 Macs, and modern desktop browsers)
- Requires fallback H.264 versions for older devices

## Implementation Strategy

For optimal cross-browser compatibility, create two video versions:

1. **Primary format:** AV1 video + Opus audio in MP4 container (modern browsers)
2. **Fallback format:** H.264 video + AAC audio in MP4 container (legacy support)

## FFmpeg Commands

### H.264 Conversion

```shell
ffmpeg -i SOURCE.mov -map_metadata -1 -c:a aac -c:v libx264 -crf 24 -preset veryslow -profile:v main -pix_fmt yuv420p -movflags +faststart -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" video.h264.mp4
```

### AV1 Conversion

```shell
ffmpeg -i SOURCE.mov -map_metadata -1 -c:a libopus -c:v libsvtav1 -qp 30 -tile-columns 2 -tile-rows 2 -pix_fmt yuv420p -movflags +faststart -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" video.av1.mp4
```

## Parameter Explanations

| Parameter | Purpose |
|-----------|---------|
| `-crf` / `-qp` | Quality slider (lower = better quality, larger file) |
| `-preset veryslow` | Prioritizes file size reduction over encoding speed |
| `-profile:v main` | H.264 profile required for Safari compatibility |
| `-pix_fmt yuv420p` | Reduces file size via color resolution reduction |
| `-movflags +faststart` | Enables streaming before complete download |
| `-tile-columns 2 -tile-rows 2` | Speed optimization for AV1 encoding |
| `-vf "scale=..."` | Ensures even pixel dimensions for codec compatibility |

## HTML Implementation

```html
<video controls width="600" height="400">
  <source
    src="video.av1.mp4"
    type="video/mp4; codecs=av01.0.05M.08,opus"
  >
  <source
    src="video.h264.mp4"
    type="video/mp4; codecs=avc1.4D401E,mp4a.40.2"
  >
</video>
```

Browsers read source tags sequentially, playing the first supported format.

## Converting GIFs to Video

Replace GIF animations with video equivalents. GIFs consume "20–40 times more space" than modern video codecs while draining more device battery.

### GIF to H.264

```shell
ffmpeg -i IMAGE.gif -map_metadata -1 -an -c:v libx264 -crf 24 -preset veryslow -profile:v main -pix_fmt yuv420p -movflags +faststart -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" animation.h264.mp4
```

### GIF to AV1

```shell
ffmpeg -i IMAGE.gif -map_metadata -1 -an -c:v libsvtav1 -qp 30 -tile-columns 2 -tile-rows 2 -pix_fmt yuv420p -movflags +faststart -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" animation.av1.mp4
```

### HTML for GIF Replacement

```html
<video autoplay loop muted playsinline width="300" height="200">
  <source src="animation.av1.mp4" type="video/mp4; codecs=av01.0.05M.08">
  <source src="animation.h264.mp4" type="video/mp4">
</video>
```

The `autoplay`, `loop`, and `muted` attributes replicate GIF behavior without requiring JavaScript.

## Recent Updates

Updated February 2025 to recommend SVT-AV1 as a faster encoding alternative, and to acknowledge that modern devices no longer require separate HEVC versions.
