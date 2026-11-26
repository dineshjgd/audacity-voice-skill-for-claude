---
name: youtube-voice-audacity
description: Process a voice recording in Audacity 4 into a YouTube-ready WAV with a tested voiceover chain (warm bass, -14 LUFS, -1 dB limiter).
---

# YouTube voice processing in Audacity

Use this when the user asks to clean up, polish or "make perfect for YouTube" a voice recording, or says "use my YouTube voice settings".

## Prerequisite
- The voice should be recorded with an **external microphone that has built-in noise cancellation**. This chain does no software noise reduction, because the mic already handles it.
- Audacity 4 runs on the user's computer; drive it with computer use (resolve and request access to "Audacity 4.0").
- Judge results on earphones or a phone speaker. Laptop speakers will always sound thinner, so don't EQ for them.

## Do NOT use
- **No Audacity noise reduction.** Stacking a second noise reduction on top of the mic's noise cancellation makes the voice sound thin and processed.
- **No Clip fix** unless the original file really clips.

## Step 0 - start from the untouched original
1. Open the original recording directly (File > Open), not a project that may already have effects applied.
2. Select all (Ctrl+A) and run Analyse > Measure RMS. An unprocessed voice take usually reads about **-18 to -20 dB**. If it reads much hotter (e.g. -11 dB) or the waveform is flat against the top, effects were already applied - find the original file first.

## The chain (apply to the whole track, in this order)
| # | Effect (Effect menu) | Settings |
|---|---|---|
| 1 | EQ and filters > High-pass filter | Frequency **80 Hz**, roll-off **12 dB/octave** |
| 2 | Volume and compression > Compressor | Threshold **-24 dB**, ratio **2:1**, attack **10 ms**, release **150 ms**, lookahead 3 ms, knee 6 dB, make-up gain **0 dB** |
| 3 | EQ and filters > Shelf filter | **Low-shelf**, frequency **200 Hz**, amount **+4 dB** (bass/warmth) |
| 4 | Volume and compression > Loudness Normalisation | Perceived loudness to **-14 LUFS**, "Treat mono as dual mono" ticked |
| 5 | Volume and compression > Limiter | Threshold **-1 dB**, output **-1 dB**, lookahead 1 ms, knee 2 dB, release 20 ms |

Adjustments the user may ask for:
- "more bass" -> low-shelf +6 dB (no higher; voice gets boomy). "less bass" -> +2 to 3 dB.
- After changing the shelf, always re-run steps 4 and 5 so loudness stays at -14 LUFS.

## Export
- Ctrl+Shift+E (File > Export audio): **WAV (Microsoft)**, **Mono**, **48000 Hz**, **Signed 16-bit PCM**.
- Folder: the same folder as the source file, unless the user names another.
- File name: original name + `_youtube_bass` (never overwrite the original).
- Tell the user the full path so they can listen and compare against the original.

## Targets to report
- Integrated loudness: -14 LUFS
- Peaks: no higher than -1 dB
- Noise in pauses: below -60 dB

## Audacity 4 quirks (computer use)
- The first click on **Apply** often only focuses the dialog. Click Apply, wait, take a screenshot; if the dialog is still open, click Apply once more. Then confirm via the Edit menu that "Undo '<effect>'" names the effect, so nothing is applied twice.
- Hovering sometimes fails to open Effect submenus. Use the keyboard instead: open Effect, use the arrow keys to reach the submenu row, press Right, arrow down to the effect, press Enter.
- In the Windows Open dialog, typing is only allowed in the "File name" box and double-clicks or drags may be blocked. Type the full file path (or a folder name) in the File name box and press Enter.
- Opening a file can create a second Audacity window; make sure the right project window is in front before applying effects.
- Release the computer-use lock at the end of the turn.
