# Techno Tunnel XR

A single-file browser app that combines a randomized Web Audio techno generator, a Three.js tunnel visualizer, desktop rhythm/shooter gameplay, and WebXR support.

The whole project runs from one HTML file. Audio, visuals, controls, storage, and gameplay all live in the same page.

## What it does

This app generates a looping old-school techno sketch and turns every scheduled sound event into moving geometry inside a cylindrical tunnel.

Current instrument set:

- Kick
- Snare
- Hi-hat
- Bass 1
- Bass 2
- Lead 1
- Lead 2

Each bar is generated from pattern pools and mutations, so the groove keeps evolving instead of repeating exactly.

## Main feature set

### Audio engine

- Web Audio based synth/drum engine
- Randomized bar generation
- 7 instrument lanes
- Live BPM changes
- Per-instrument mute and volume
- Per-instrument solo
- Per-instrument oscillator selection
- Per-instrument base-frequency and tone controls
- Per-instrument preview play/stop
- Optional per-instrument preview looping for tuning while the main transport is stopped

### Extra music layers

- Two bass voices
- Two lead voices
- Sparse lead patterns that follow the harmonic family of the bass movement

### Master FX / output shaping

Global mastering-style controls are exposed in the GUI, including:

- master volume
- drive / saturation
- high-pass filter
- low-pass filter
- low shelf EQ
- mid EQ
- high shelf EQ
- compressor
- convolver reverb / wet-dry style processing

## Visual system

### Tunnel view

The old flat lane view evolved into a tunnel / pipe layout.

- open-ended cylinder tunnel
- instrument lanes distributed around the inside wall
- configurable tunnel radius, height, radial segments, theta start, and theta length
- configurable lane inset and lane-marker dimensions
- incoming cues travel through the tunnel toward the viewer

### Cue geometry

Each instrument can use different incoming geometry types.

Supported visual shapes include solid and line-style forms such as:

- box
- capsule
- circle
- cone
- cylinder
- dodecahedron
- extrude
- icosahedron
- lathe
- octahedron
- plane
- polyhedron
- ring
- shape
- sphere
- tetrahedron
- torus
- torus knot
- tube
- edges
- wireframe

Muted instruments render as edge-only / outline-like visuals instead of solid filled shapes.

### Star field

The environment includes a moving star field.

- flying stars
- configurable count, spread, speed, size, and colors
- optional trails
- stars move through the scene instead of being static background dots

### Environment controls

There is a dedicated environment folder for scene styling.

- background color
- fog color / density
- ambient light color / intensity
- key light color / intensity
- rim light controls
- tunnel colors
- wire / marker / ring / star colors

### Camera controls

Desktop/mobile camera settings are adjustable and persist in the saved config.

- orbit controls toggle
- camera distance from tunnel end
- camera position / target tuning
- FOV control
- store current view
- reset view

## Desktop gameplay

The visualizer is also playable as a simple rhythm/shooter game.

### Collector mode

A collector ring sits on the active lane near the front of the tunnel.

- left/right arrow keys move the collector between instrument lanes
- ring rotation is configurable
- lane-based scoring
- per-instrument score breakdown

### Shooting mode

The collector can fire projectiles.

- shoot from the collector toward incoming cues
- bullet shape can be fixed or random simple geometry
- cue hit creates an explosion effect
- hits add score
- separate shoot and hit sound effects

## WebXR / VR mode

The app can run in a WebXR-capable browser such as Quest Browser.

### XR support

- VRButton integration
- XR controllers support
- XR hand model support when available
- head-aim mode
- controller-aim mode
- controller laser aiming lines
- reticles / aim rings in XR
- trigger-based shooting

### XR movement

There is an “invisible lift” style movement system for VR.

- thumbstick forward/backward travel along tunnel depth only
- inertia / acceleration / damping
- adjustable movement range
- movement reset

### XR HUD and score

The app includes an XR score display and score breakdown.

Current state:

- score is available in XR
- world/follow HUD placement exists
- controller/hand wearable HUD anchoring has been actively worked on, but should still be treated as experimental until fully verified in-headset

## Score system

The app tracks gameplay score and per-instrument contribution.

- total score
- kick/snare/hat/bass1/bass2/lead1/lead2 breakdown
- centered score panel on desktop
- XR score display path
- LED-style digit presentation work has been added for XR score rendering

## GUI structure

The project uses lil-gui and has grown into a multi-folder control surface.

Main sections include:

- Transport
- Instruments
  - Kick
  - Snare
  - Hi-hat
  - Bass 1
  - Bass 2
  - Lead 1
  - Lead 2
- Master FX
- Tunnel / Visuals
- Environment
- Camera
- Collector / Game
- XR / VR
- Storage

Folders are intended to start closed by default so the UI is easier to navigate.

## Storage, autosave, and presets

The app protects settings aggressively so a refresh does not wipe the setup.

### Autosave

- changes are saved automatically
- current settings are restored on reload

### Browser storage

- IndexedDB primary save
- localStorage fallback / backup

### Presets

- save now
- export JSON
- import JSON
- clear saved data

Exported JSON includes timestamped preset data.

## How to run

Open the HTML file in a modern browser with internet access.

Why internet access is needed:

- Three.js is loaded as an ES module from a CDN
- lil-gui is loaded from a CDN

Recommended browsers:

- Chrome / Edge on desktop
- modern Chromium-based mobile browsers
- Meta Quest Browser for WebXR testing

## Controls summary

### Desktop / non-XR

- Play / Pause / Stop / Restart in lil-gui
- left/right arrows move collector lane
- space shoots when shooting mode is enabled

### XR

- headset mode can use head aiming
- controller mode can use controller aiming and triggers
- thumbstick moves the player forward/backward along the tunnel depth

## Technical notes

- single-file architecture
- HTML, CSS, and JavaScript in one page
- Three.js module imports
- lil-gui module imports
- Web Audio API synthesis
- IndexedDB + localStorage persistence
- WebXR integration

## Performance note

The app is still a prototype and can become heavy in standalone VR if several expensive settings are pushed at once, especially:

- very long tunnel height
- high star counts
- complex cue geometry
- high pixel ratio in XR

Recent work has tried to reduce the cost of long tunnels, but Quest performance still depends heavily on the chosen visual settings.

## Current caveats

A few areas are still experimental and should be treated as work in progress:

- wearable XR HUD anchoring to hand/controller
- some XR-specific alignment tuning
- performance tuning for large tunnels in standalone headsets
- collision is currently proximity-based 3D collision, not exact mesh-against-mesh physics

## Summary

This project is now a hybrid of:

- generative techno sketchpad
- tunnel music visualizer
- desktop rhythm/shooter toy
- WebXR prototype for headset play
- persistent preset-based browser instrument playground
