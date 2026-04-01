# Protocol

## Header
Each packet should include:

- packet type
- sequence number
- timestamp

## Core packet types
- MouseMoveRelative
- MouseButton
- MouseWheel
- KeyboardText
- KeyboardKey
- ModifierState
- Ping
- HostState
- SessionAck
- ErrorState

## Reliability model
### Low-latency / drop-tolerant
- MouseMoveRelative
- Ping

### Reliable / ordered
- MouseButton
- KeyboardText
- KeyboardKey
- ModifierState
- SessionAck
- ErrorState

## Packet philosophy
Mouse movement should be coalescible.
Clicks and keyboard input should not be coalesced.

## Validation
The host must reject packets that:
- are malformed
- do not match protocol expectations
- arrive in invalid control states
- attempt unauthorized actions before control is enabled
