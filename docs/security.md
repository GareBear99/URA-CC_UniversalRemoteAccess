# Security Notes

## Minimum baseline
URA-CC should not enable control unless:
- session transport is active
- host approval requirements are satisfied
- the device is trusted or newly approved
- control state is explicitly enabled on the host

## Key risks
- unauthorized device trust
- spoofed or malformed control packets
- accidental control enablement
- insecure signaling assumptions
- privilege/permission issues in input injection

## Host rules
- reject input outside control-active state
- log state transitions clearly
- make trust decisions explicit
- provide revoke-all-devices support
