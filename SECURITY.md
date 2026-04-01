# Security Policy

## Supported security direction

URA-CC is intended to follow these baseline security rules:

- encrypted session transport
- explicit host approval on first device trust
- trusted-device storage
- host-side permission gating before control is enabled
- packet validation and version checks
- session timeout and disconnect handling
- device revocation support

## Reporting a vulnerability

Please report vulnerabilities privately before public disclosure.

Include:

- issue summary
- affected component
- reproduction steps
- impact assessment
- suggested mitigation if known

## Scope notes

The most sensitive areas for this project are:

- input injection paths
- device pairing and trust storage
- signaling/session negotiation
- transport security
- permission escalation and unintended control enablement
