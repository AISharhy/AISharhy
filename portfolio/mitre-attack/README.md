# MITRE ATT&CK — Blue Team Study Notes

These are **hypothetical detection questions**, not demonstrated detections. Technique identifiers refer to the MITRE ATT&CK Enterprise knowledge base: https://attack.mitre.org/

| Technique | What to investigate | Potential telemetry | Common pitfalls |
| --- | --- | --- | --- |
| [T1110 — Brute Force](https://attack.mitre.org/techniques/T1110/) | Patterns of repeated authentication attempts | Windows logon failures, identity-provider logs | Password typos and broken services can look similar |
| [T1059.001 — PowerShell](https://attack.mitre.org/techniques/T1059/001/) | Unexpected PowerShell process context | Sysmon process events, command-line logging, PowerShell events | Administrative automation is often legitimate |
| [T1078 — Valid Accounts](https://attack.mitre.org/techniques/T1078/) | Suspicious use of legitimate credentials | Authentication, MFA, device and privilege logs | New device or new location alone is not compromise |

## Study process

1. Read the official technique description and relevant sub-techniques.
2. Identify what **observable behavior** would support that technique.
3. Check that required logs and fields are actually collected.
4. Build an analyst hypothesis, including benign alternatives.
5. Test only in an isolated and authorized lab.
6. Save scrubbed evidence, limitations and false-positive analysis.

**Mapping principle:** Do not label an event as a confirmed ATT&CK technique without adequate evidence.
