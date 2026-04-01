# URA-CC — CouchController
### Universal Remote Access

Turn your phone into a couch-friendly remote for your computer with live desktop view, thumb-dial mouse control, left/right click, and on-demand keyboard input.

URA-CC is a mobile-first remote control system for relaxed-distance desktop use. Instead of forcing users into awkward touchpad gestures, URA-CC uses a one-handed controller-style interface built around a thumb movement dial, fast clicks, and keyboard access.

## Why this repo exists

Most mobile desktop remotes are optimized for either:

- enterprise remote support
- full workstation replacement
- touchpad-first control on small screens

URA-CC is optimized first for:

- couch control
- TV-connected PC control
- media-center navigation
- one-handed desktop interaction
- second-room computer access
- casual productivity from a phone

**URA-CC is not trying to be a bloated enterprise suite first. It is trying to be the cleanest couch-friendly phone-to-PC control system possible.**

---

## Core product idea

URA-CC has two main components.

### Desktop host
The host runs on the computer and is responsible for:

- capturing the desktop
- encoding and streaming video to the phone
- receiving input packets from the phone
- injecting mouse and keyboard events into the operating system
- managing pairing, trust, and session state

### Mobile client
The phone app is responsible for:

- rendering the live desktop feed
- exposing the thumb-dial mouse control
- sending left and right click input
- opening the keyboard panel
- supporting scroll mode, drag lock, and precision mode later

---

## Main differentiator: thumb-dial mouse control

The signature feature is the **movement dial**.

Instead of pretending the phone is a laptop trackpad, URA-CC treats it more like a controller:

- center = no movement
- farther from center = faster cursor movement
- angle = cursor direction
- deadzone = anti-jitter protection
- precision mode = slower and more accurate control

```text
radius = clamp(distance_from_center / max_radius, 0..1)
if radius < deadzone -> no movement

speed = (radius ^ curve_power) * max_speed
dx = cos(angle) * speed
dy = sin(angle) * speed
```

Suggested defaults:

- deadzone: `0.12`
- curve power: `1.8`
- input tick target: `60 Hz`
- precision multiplier: `0.45`

This makes one-handed use dramatically better for couch, studio, bed, and TV workflows.

---

## MVP scope

The strongest first version is intentionally narrow.

### In scope
- Windows desktop host
- Android client
- LAN-only connection for v1
- real-time desktop video stream
- thumb-dial mouse movement
- left click
- right click
- keyboard text input
- trusted-device approval flow
- disconnect / reconnect path

### Out of scope for v1
- internet relay support
- iPhone client
- macOS host
- Linux host
- audio streaming
- file transfer
- clipboard sync
- multi-monitor support
- account system

This keeps the first release focused on becoming a real usable product quickly instead of collapsing under feature creep.

---

## Product positioning

URA-CC should be positioned as:

**A couch-friendly universal remote for your computer**

Not as:

- a generic remote desktop clone
- an IT admin suite
- an AnyDesk replacement on day one

### Best positioning angles
- one-handed desktop control
- local-first privacy
- couch / TV / media-center control
- low-friction casual remoting
- thumb-dial cursor control instead of awkward gesture-only input

### Short pitch
**Control your PC from the couch with live view, a thumb-dial mouse, left/right click, and keyboard input.**

---

## Recommended architecture

### Desktop host
- Rust
- native Windows capture path
- native Windows input injection layer
- WebRTC transport

### Mobile client
- Flutter
- WebRTC bindings/package
- custom controller-style overlay

### Signaling
- lightweight Rust or Node signaling service
- LAN-first session setup for MVP
- relay and NAT traversal later

### Why this stack
- Rust gives strong performance and deterministic host-side behavior
- Flutter gives fast mobile UI iteration and cross-platform runway
- WebRTC is the cleanest v1 answer for low-latency video + input transport

---

## System model

```text
[Desktop Host]
  Capture Engine
  Encoder / Stream Sender
  Input Receiver
  Input Injector
  Pairing + Trust Store
  Session State Machine

[Signaling Service]
  Session creation
  Offer/answer exchange
  ICE candidate exchange

[Phone Client]
  Video Renderer
  Dial + Click + Keyboard UI
  Session Controller
  Input Packet Sender
  Connection State Manager
```

---

## Security baseline

Even as a LAN-first product, URA-CC should not ship without:

- encrypted transport
- first-use host approval
- trusted device storage
- packet validation
- host-side control-state gating
- explicit disconnect handling
- revoke-all-devices support

That keeps the MVP from turning into a throwaway toy that has to be rebuilt later.

---

## Repository structure

```text
ura-cc/
  .github/
    ISSUE_TEMPLATE/
    workflows/
  assets/
  apps/
    host-windows/
    mobile-client/
    signaling/
  crates/
    protocol/
    host-core/
    capture-windows/
    input-windows/
    auth-core/
    transport-webrtc/
  docs/
    architecture.md
    product-spec.md
    protocol.md
    roadmap.md
    security.md
    seo-keywords.md
  README.md
  CONTRIBUTING.md
  SECURITY.md
  CODE_OF_CONDUCT.md
  LICENSE
  CHANGELOG.md
```

---

## Build phases

### Phase 1 — MVP
- protocol definitions
- host state machine
- Flutter mobile shell
- dial UI
- basic signaling
- live stream session
- Windows capture
- Windows input injection
- trusted-device pairing

### Phase 2 — platform expansion
- iPhone client
- macOS host
- reconnect polish
- cleaner pairing flow

### Phase 3 — internet access
- NAT traversal
- TURN relay fallback
- stronger auth model
- better session management

### Phase 4 — premium expansion
- drag lock
- scroll mode
- quality profiles
- shortcut/macros
- clipboard sync
- file transfer
- multi-monitor support

---

## Monetization direction

URA-CC is strongest as a convenience product, not an enterprise admin product.

### Free
- LAN discovery
- mouse dial
- left/right click
- basic keyboard input
- single host profile

### Pro
- live desktop video stream
- drag lock
- precision mode
- scroll mode
- multiple host profiles
- reconnect history
- shortcut/macros
- future clipboard and file transfer tools

### Pricing tests
- one-time unlock: `$4.99–$9.99`
- or subscription: `$1.99–$3.99/month`

The best wedge is couch control, media-center control, and local-first convenience.

---

## SEO / discoverability direction

This repo is written to be discoverable for searches around:

- remote mouse for PC
- phone mouse for Windows
- couch controller PC
- remote keyboard phone to desktop
- local remote desktop control
- WebRTC remote desktop
- Rust remote desktop host
- Flutter remote desktop client
- universal remote access app

See [`docs/seo-keywords.md`](docs/seo-keywords.md) for keyword clusters, title ideas, and metadata copy.

---

## Current status

Current repo state:

- product direction locked
- architecture direction locked
- docs package ready for GitHub publishing
- implementation scaffolding planned

Next correct move:

- wire protocol crate
- bring up the host state machine
- stand up the Flutter session shell
- establish LAN session flow
- replace placeholders with real transport/capture/input

---

## Final statement

**URA-CC — CouchController — Universal Remote Access**

URA-CC turns your phone into a couch-friendly universal remote for your computer, combining live screen streaming with joystick-style mouse control, fast clicks, and on-demand keyboard entry.

It is built local-first, one-handed, and aimed at making casual desktop control feel natural instead of awkward.
