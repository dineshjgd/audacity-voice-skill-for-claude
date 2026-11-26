# YouTube Audacity Enhancer

A Claude skill that turns a raw voice recording into a YouTube-ready WAV in **Audacity 4**, using a tested processing chain for spoken voiceovers.

## Prerequisite

Record your voice with an **external microphone that has built-in noise cancellation** (for example, a wireless lavalier or USB mic with an on-board noise-cancellation setting). The chain below deliberately skips software noise reduction because the mic already handles it; using a phone's built-in mic or a mic without noise cancellation will give weaker results.

## What it does

| # | Effect | Settings |
|---|---|---|
| 1 | High-pass filter | 80 Hz, 12 dB/octave (removes rumble) |
| 2 | Compressor | -24 dB threshold, 2:1, 10 ms attack, 150 ms release, 0 dB make-up |
| 3 | Low-shelf filter | 200 Hz, +4 dB (warmth / bass) |
| 4 | Loudness Normalisation | -14 LUFS (YouTube's playback standard) |
| 5 | Limiter | -1 dB ceiling (no clipping after YouTube re-encodes) |

Export: WAV, mono, 48 kHz, 16-bit PCM, saved as `<original name>_youtube_bass.wav` (the original is never overwritten).

Deliberately **not** used: software noise reduction (stacking it on top of the mic's noise cancellation makes the voice thin) and Clip fix (only if the recording really clips).

## Targets

- Integrated loudness: **-14 LUFS**
- Peaks: **≤ -1 dB**
- Noise in pauses: **below -60 dB**

## Requirements

- Audacity 4 installed on the computer
- Claude with computer use enabled (Claude desktop app), so Claude can operate Audacity

## Install

Copy the `youtube-voice-audacity/` folder into your Claude skills directory (for Claude Code: `~/.claude/skills/`), or upload it as a skill in Claude settings.

## Use

Ask Claude something like:

> Process `path/to/my-recording.m4a` with my YouTube voice settings.

Claude opens the file in Audacity, checks it is an unprocessed original, applies the chain, and exports the WAV next to the source file.

## Structure

```
YouTube-Audacity-Enhancer/
├── README.md
└── youtube-voice-audacity/
    └── SKILL.md
```
