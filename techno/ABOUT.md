# Techno Track Visualizer

A single-file browser techno sketch that combines a randomized Web Audio sequencer with a Three.js road-style visualizer and a lil-gui control panel.

The app runs entirely from `index.html`. It generates kick, snare, hi-hat, and bass arpeggiator patterns, visualizes them as incoming cubes on a central track, and lets you tune sound design live while the sequence is running.

## What this is

This project is a browser-based audiovisual toy / prototype for making rough old-school techno patterns.

It includes:

- **Web Audio sequencer** for kick, snare, hi-hat, and bass arp
- **Random bar generation** so patterns keep changing over time
- **Three.js “incoming road” visualizer** inspired by rhythm-game lanes
- **lil-gui controls** for transport, BPM, frequencies, decay, oscillator types, mute, volume, and preview playback
- **Per-instrument preview mode** so each sound can be auditioned while the transport is stopped
- **Looped preview mode** synced to the current BPM for tuning
- **Persistent settings** saved to both `localStorage` and `IndexedDB`
- **JSON import/export** for presets and backups
- **Muted visual state** where muted instruments show as edge-only geometry instead of solid filled cubes

## Main idea

The screen shows a stylized track or road moving toward the viewer. Each scheduled sound event becomes a cube traveling down one of four lanes:

- **Kick**
- **Snare**
- **Hi-hat**
- **Bass**

The cube:

- **color** reflects the oscillator type / instrument palette
- **height** reflects frequency
- **lane** reflects the instrument
- **wireframe / edges-only look** indicates that instrument is muted

## Controls

### Global

- **Play** — starts the sequencer and audio engine
- **Pause** — pauses playback
- **Stop** — stops playback and resets bars / cues
- **Restart** — resets and starts again
- **BPM** — changes tempo
- **Master Volume** — overall output level
- **Visual Horizon** — how far ahead the visual scheduler looks
- **Track Speed** — speed of incoming visual cubes

### Per instrument

Each instrument folder has its own controls.

#### Kick
- Mute
- Volume
- Loop
- Play
- Stop
- Base Freq
- Decay
- Osc Type

#### Snare
- Mute
- Volume
- Loop
- Play
- Stop
- Tone Freq
- Noise HPF
- Decay
- Osc Type

#### Hi-Hat
- Mute
- Volume
- Loop
- Play
- Stop
- Filter Freq
- Tone Freq
- Decay
- Osc Type

#### Bass Arp
- Mute
- Volume
- Loop
- Play
- Stop
- Base Freq
- Filter Base
- Decay
- Osc 1 Type
- Osc 2 Type

## Preview workflow

When the transport is stopped, each instrument can be tested individually:

- press **Play** in that instrument folder to hear one hit / note
- enable **Loop** to keep previewing it repeatedly in time with the current BPM
- adjust frequency, decay, oscillator type, and volume while it is looping
- press **Stop** in the folder to stop that preview

Starting the main transport stops preview loops so they do not stack on top of the full sequence.

## Pattern generation

The sequencer uses predefined pattern pools for:

- kick
- snare
- hi-hat
- bass gate / arp rhythm

Those patterns are then randomly mutated and switched over time to keep the track moving.

The bass line also changes according to simple progression and arpeggiator rules, so it follows the drum pattern changes instead of staying static.

## Storage and presets

The app tries to protect work from accidental refreshes.

### Autosave

Settings are automatically saved when GUI values change.

### Persistent storage

The latest settings are stored in:

- **IndexedDB** (primary)
- **localStorage** (fallback / backup)

When the page reloads, the app restores the most recent saved settings automatically.

### Manual preset tools

Inside the **Storage** folder:

- **Save Now** — saves immediately
- **Export JSON** — downloads a preset JSON file with timestamp metadata
- **Import JSON** — loads a previously exported preset
- **Clear Saved** — clears browser-stored settings

## How to run

Open `index.html` in a modern browser.

Because the page imports **Three.js** and **lil-gui** as ES modules from a CDN, it should be opened in a browser session with internet access.

For best results:

1. open the page in Chrome, Edge, or another modern Chromium-based browser
2. press **Play** once to unlock audio
3. tweak BPM and instrument folders live
4. use **Export JSON** to save presets you want to keep

## Technical notes

- Everything is contained in **one file**: HTML, CSS, and JavaScript in `index.html`
- Rendering uses **Three.js module imports**
- GUI uses **lil-gui module imports**
- Sound generation uses the **Web Audio API**
- Storage uses **IndexedDB** and **localStorage**
- The app attaches itself to `window.technoApp`

## Good next steps

Possible future upgrades:

- preset browser with multiple saved slots
- record to WAV / WebM
- camera controls and alternative visual themes
- pattern lock / manual step sequencer mode
- swing, shuffle, and accent controls
- acid slides / resonance automation for bass
- drum sample loading instead of pure synthesis
- MIDI input / clock sync

## File structure

- `index.html` — the entire app

## Summary

This is a **single-file Web Audio + Three.js techno generator / visualizer** with live sound design controls, per-instrument previews, persistent settings, and JSON preset import/export.
