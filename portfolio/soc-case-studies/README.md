# SOC Analyst L1 — Simulated Case Studies

**All cases below are fictional training scenarios, not completed investigations.** The purpose is to practise disciplined triage and escalation.

## Standard alert-triage workflow

1. **Validate:** alert source, time range, affected host, user, rule and telemetry quality.
2. **Contextualize:** asset criticality, known maintenance, account type and earlier related events.
3. **Correlate:** look for adjacent endpoint, identity and network indicators.
4. **Assess:** separate what is observed from hypotheses; decide false positive, benign true positive, or suspicious activity.
5. **Respond / escalate:** follow playbook and permissions; preserve evidence, explain impact and next action.
6. **Document:** timeline, supporting log references, uncertainty and rationale.

## Case A — Repeated Windows logon failures (simulated)

**Scenario:** A test host records several failed authentications in a short window.

- **Potential telemetry:** Windows Security Event ID 4625; compare with 4624 and account lockout events when available.
- **Questions:** One user or many? One source or multiple? Expected service task? A successful login afterwards?
- **Possible explanations:** mistyped password, stale credentials, automated retries or password guessing.
- **Disposition:** Cannot conclude brute force from a count alone; escalate if the pattern, context and policy thresholds support it.
- **MITRE reference:** T1110 (Brute Force) *if attack behavior is supported by evidence*.

## Case B — Unusual PowerShell execution (simulated)

**Scenario:** An endpoint alert reports PowerShell launched with an unexpected command line.

- **Potential telemetry:** process ancestry, command line if collected, Sysmon Event ID 1; PowerShell logs where enabled.
- **Questions:** Who initiated it? Is it part of endpoint administration? Signed script? Network connection? Child processes?
- **Disposition:** Investigate before treating PowerShell itself as malicious; escalate confirmed or materially suspicious behavior.
- **MITRE reference:** T1059.001 (PowerShell) when the observed technique fits.

## Case C — Valid-account activity anomaly (simulated)

**Scenario:** An account signs in from an unfamiliar machine outside its normal operating pattern.

- **Potential telemetry:** authentication logs, originating host, device identity, MFA events, recent account changes.
- **Questions:** Was travel or shift work expected? Is the device managed? Are privileged actions present?
- **Disposition:** Risk depends on correlated evidence, not solely on a new device.
- **MITRE reference:** T1078 (Valid Accounts) only if supported.

## Blank investigation report

See [incident-report-template.md](incident-report-template.md) for a reusable evidence-focused template.
