# Contributing to URA-CC

Thanks for your interest in improving URA-CC.

## Principles

Contributions should preserve these core project rules:

- mobile-first control UX
- thumb-dial input remains a first-class interaction model
- deterministic host-side state transitions
- no silent failure paths
- security gating for control actions
- MVP scope discipline before feature expansion

## Good contribution areas

- Flutter UI polish
- protocol serialization
- Rust host state management
- Windows capture improvements
- Windows input injection hardening
- docs, diagrams, and onboarding improvements
- testing, logging, and diagnostics

## Workflow

1. Fork the repository.
2. Create a focused branch.
3. Keep changes narrow and well-explained.
4. Include notes on user impact and technical tradeoffs.
5. Open a pull request with clear reasoning.

## Pull request guidance

A strong PR explains:

- what changed
- why it changed
- any security implications
- whether it affects protocol compatibility
- whether it changes MVP scope

## Notable anti-patterns

Please avoid:

- adding broad features without architectural fit
- weakening approval or trust flows for convenience
- changing the control metaphor away from the thumb-dial-first design
- introducing hidden state transitions or ambiguous control permissions
