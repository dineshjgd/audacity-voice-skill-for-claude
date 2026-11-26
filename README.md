# YouTube Audacity Enhancer

A Claude skill that turns a raw voice recording into a YouTube-ready WAV in **Audacity 4**, using a tested processing chain built for voiceovers recorded with the **GRENARO S12** wireless mic.

## What it does

| # | Effect | Settings |
|---|---|---|
| 1 | High-pass filter | 80 Hz, 12 dB/octave (removes rumble) |
| 2 | Compressor | -24 dB threshold, 2:1, 10 ms attack, 150 ms release, 0 dB make-up |
| 3 | Low-shelf filter | 200 Hz, +4 dB (warmth / bass) |
| 4 | Loudness Normalisation | -14 LUFS (YouTube's playback standard) |
| 5 | Limiter | -1 dB ceiling (no clipping after YouTube re-encodes) |

Export: WAV, mono, 48 kHz, 16-bit PCM, saved as `<original name>_youtube_bass.wav` (the original is never overwritten).

Deliberately **not** used: noise reduction (the mic already does it; stacking it made the voice thin) and Clip fix (only if the recording really clips).

## Targets

- Integrated loudness: **-14 LUFS**
- Peaks: **≤ -1 dB**
- Noise in pauses: **below -60 dB**

## Install

Copy the `youtube-voice-audacity/` folder into your Claude skills directory (for Claude Code: `~/.claude/skills/`), or upload it as a skill in Claude settings.

## Use

Ask Claude something like:

> Process `D:\...\voice\My recording 1.m4a` with my YouTube voice settings.

Claude opens the file in Audacity (via computer use), checks it is an unprocessed original, applies the chain, and exports the WAV next to the source or into `D:/audio_samples`.

## Structure

```
YouTube-Audacity-Enhancer/
├── README.md
└── youtube-voice-audacity/
    └── SKILL.md
```
