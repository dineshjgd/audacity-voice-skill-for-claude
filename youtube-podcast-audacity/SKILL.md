---
name: youtube-podcast-audacity
description: Process a voice recording in Audacity 4 into a podcast-style YouTube WAV - clearer, more present and evenly levelled, with soft warmth (-14 LUFS, -1 dB limiter). Use when the user asks for the "podcast" voice settings.
---

# Podcast voice processing in Audacity

Use this when the user asks for the podcast / premium / "Option B" voice, or "use my podcast voice settings". For the original bass-heavy chain, use the `youtube-voice-audacity` skill instead.

How it differs from the original chain: less boom at 100-200 Hz, more presence (2-5 kHz) and a little air, and a second, faster compressor so every word sits at nearly the same level. At the same loudness it sounds clearer and slightly louder than the original chain.

## Prerequisite
- Voice recorded with an **external microphone with built-in noise cancellation**. No software noise reduction is used.
- Audacity 4 on the user's computer, driven with computer use (resolve and request access to "Audacity 4.0").
- Judge on earphones or a phone speaker, not laptop speakers.

## Do NOT use
- **No noise reduction** (thins the voice on top of the mic's noise cancellation).
- **No Clip fix** unless the original really clips.
- **No Graphic EQ / Filter Curve EQ** - their sliders can't be set to exact values reliably. Every tone change below uses Shelf filter, which takes typed numbers.

## Step 0 - start from the untouched original
1. File > Open (Ctrl+O) the original recording, not a project that may already have effects.
2. Ctrl+A, then Analyse > Measure RMS. An unprocessed take reads roughly -18 to -28 dB. If it reads much hotter (around -11 dB) or the waveform is flat against the top, effects were already applied - find the original first.

## The chain (whole track selected, in this order)
| # | Effect (Effect menu) | Settings |
|---|---|---|
| 1 | EQ and filters > High-pass filter | **80 Hz**, roll-off **12 dB** |
| 2 | EQ and filters > Shelf filter | **Low-shelf**, **300 Hz**, **+2 dB** (body/warmth) |
| 3 | EQ and filters > Shelf filter | **High-shelf**, **2500 Hz**, **+3 dB** (presence/clarity) |
| 4 | EQ and filters > Shelf filter | **High-shelf**, **8000 Hz**, **+1 dB** (air) |
| 5 | Volume and compression > Compressor | Threshold **-24 dB**, ratio **2**, attack **10 ms**, release **150 ms**, lookahead 3 ms, knee **6 dB**, make-up **0 dB** |
| 6 | Volume and compression > Compressor | Threshold **-18 dB**, ratio **3**, attack **3 ms**, release **60 ms**, lookahead 3 ms, knee **4 dB**, make-up **0 dB** |
| 7 | Volume and compression > Loudness Normalisation | Perceived loudness to **-14 LUFS**, "Treat mono as dual mono" ticked |
| 8 | Volume and compression > Limiter | Threshold **-1 dB**, output **-1 dB**, lookahead 1 ms, knee 2 dB, release 20 ms |

Notes:
- Shelf filter's Amount box takes **whole dB only** - typing "1.5" becomes 15. Type integers, then check the box before Apply.
- The Compressor dialog remembers the last values: after step 6 it opens at -18 dB / 3:1, so reset to step-5 values on the next file.
- Adjustments: "more clarity" -> step 3 to +4 dB. "warmer / more bass" -> step 2 to +3 dB (no more; it gets boomy). "too sharp / hissy s sounds" -> step 4 to 0 dB (skip) and step 3 to +2 dB. After any change, re-run steps 7 and 8.

## Export
- Ctrl+Shift+E: **WAV (Microsoft)**, **Mono**, **48000 Hz**, **Signed 16-bit PCM**.
- Folder: same as the source file (the Folder box accepts a typed path).
- File name: original name + `_podcast` (never overwrite the original).
- Tell the user the full path.

## Targets to report
- Integrated loudness -14 LUFS as Audacity measures it (dual mono). A plain mono meter (e.g. ffmpeg) will read about -17 LUFS for the same file - that's expected, not an error.
- Peaks no higher than -1 dB. Noise in pauses below -60 dB.

## Audacity 4 quirks (computer use)
- Effect submenus: click Effect, hover the category row, move the mouse right into the submenu, hover the item, then click it. Positions shift by one row after the first effect, because a "Repeat <effect>" item appears near the top of the menu - zoom on the menu before clicking. Pressing Enter in a submenu may run the first item, not the highlighted one.
- Volume and compression submenu order: Amplify, Compressor, Limiter, Loudness Normalisation, Normalise, Remove DC offset. Limiter sits above Loudness Normalisation; don't open the wrong one.
- Pressing Escape on menus can clear the selection: check the Selection bar shows the full length before each effect, and re-select (click track area, Ctrl+A) if not.
- After each Apply, confirm Edit menu shows "Undo '<effect>'".
- If Audacity is minimised or off-screen and won't come forward, ask the user to bring it to the front and maximise it.
- In the Windows Open dialog, type the full path in the File name box and press Enter.
- Release the computer-use lock at the end of the turn.
