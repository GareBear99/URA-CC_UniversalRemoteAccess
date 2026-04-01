# Architecture

## High-level model

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

## Host responsibilities
- initialize safely
- manage session state transitions
- capture desktop frames
- stream video
- receive and validate control packets
- inject allowed input into the OS
- reject input when control is not active

## Mobile responsibilities
- connect to hosts
- render session video
- provide the control overlay
- send low-latency movement packets
- send reliable click and keyboard packets

## Signaling responsibilities
- session negotiation bootstrap
- offer/answer exchange
- candidate exchange
- no unnecessary product logic in signaling layer

## Doctrine
- keep the host deterministic
- separate view rendering from control authorization
- keep the control plane observable
- no silent state transitions
