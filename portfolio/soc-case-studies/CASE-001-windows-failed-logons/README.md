# CASE-001 — Windows Failed Logons | SOC L1 Investigation

**Type:** Fully fictional tabletop simulation, with synthetic events. **Not executed on a live Wazuh instance.**  
**Role practised:** SOC Analyst L1  
**Status:** Written scenario and analysis; live-lab validation pending.

## Executive summary

An illustrative Wazuh alert signals multiple failed Windows sign-ins (Event ID 4625) for a test account from one lab workstation. The analyst needs to check whether the activity is an ordinary password issue, misconfigured automation, or suspicious password-guessing activity. Synthetic source records appear in [events.csv](events.csv).

### Scenario details (synthetic)

- Host: `WIN-LAB-01`
- Target account: `lab-user`
- Origin: `192.0.2.25` (**TEST-NET-1 documentation address**, not a real observed source)
- Window: 2026-10-15 14:00:00–14:05:00 UTC
- Observed example: 6 failed logons, followed by one successful authentication from the same illustrative source
- Interpretation: requires investigation; not automatically proof of compromise.

## Analyst workflow

1. **Validate ingestion**: check Windows Security logs and whether the Wazuh agent is forwarding relevant events.
2. **Triage**: inspect failed logon details, target username, Logon Type, source address, timestamps and reason codes.
3. **Correlate**: locate subsequent 4624 events, other affected accounts and any account-lockout records where collected.
4. **Contextualize**: confirm whether the user retried a forgotten password or an application used stale credentials.
5. **Assess**: a successful logon following failures is noteworthy, but does **not** prove an attack.
6. **Escalate if indicated**: request review by an authorized senior analyst when account criticality, origin, frequency, other telemetry or playbook thresholds warrant it.
7. **Document**: use [incident-report.md](incident-report.md).

## Wazuh investigation guide

In the Wazuh dashboard, inspect the events for the relevant Windows agent and timeframe. Depending on installed version, data view and mappings, fields may include:

- `agent.name`
- `data.win.system.eventID` (4625 / 4624)
- `data.win.eventdata.targetUserName`
- `data.win.eventdata.ipAddress`

These are **example mappings** and require confirmation against your indexed documents. Avoid assuming that one specific Wazuh rule ID is universal or that every 4625 event automatically creates a high-severity alert. If data is missing, validate Windows Event Channel configuration and collection before troubleshooting detections.

## Decision in this simulated case

**Disposition:** Suspicious authentication pattern — **unconfirmed**, requires context and authorized follow-up.  
**Escalation:** Conditional, not automatic. If target is sensitive, source unexpected, or linked to additional indicators, escalate under the organization's policy.  
**MITRE ATT&CK mapping:** [T1110 Brute Force](https://attack.mitre.org/techniques/T1110/) is a **hypothesis**, not a confirmed technique.

## Reproduce safely in your own lab

1. Use a disposable Windows VM and a dedicated non-privileged local test account.
2. Ensure Security auditing and Wazuh event collection are configured.
3. On the VM only, manually attempt a few wrong passwords for the test account; keep below lockout thresholds and record what occurred.
4. Sign in successfully with the correct password (only if appropriate) and inspect the corresponding events.
5. Record exact timestamps, fields, screenshots with sensitive data redacted, and differences between expected and actual behavior.
6. Replace the **synthetic evidence** with your **own anonymized results**, clearly marked with testing date and environment.

Do not perform these tests on employer/customer systems without authorization.

## Files

- [events.csv](events.csv) — *synthetic* example events, not a Wazuh export.
- [incident-report.md](incident-report.md) — sample analyst report with uncertainty and next steps.

**Sources:** [Microsoft Event 4625](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625) · [Microsoft Event 4624](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624) · [Wazuh Documentation](https://documentation.wazuh.com/current/) · [MITRE ATT&CK T1110](https://attack.mitre.org/techniques/T1110/)
