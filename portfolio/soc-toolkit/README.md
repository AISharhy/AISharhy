# SOC Analyst L1 — Practical Toolkit

**Status:** Analyst study material. Commands are examples and have not been run on a live customer or production environment.

This toolkit provides repeatable, evidence-focused steps for first-line SOC triage.

## Contents

- [Alert triage checklist](triage-checklist.md) — prioritize, investigate, decide, escalate.
- [Detection and search queries](queries.md) — Windows logon investigations with Wazuh field hints and Splunk SPL.
- [Case report template](../soc-case-studies/incident-report-template.md) — document what is confirmed, uncertain and next.

## How to use

1. Start with an alert from an **authorized** lab or approved working environment.
2. Record timestamps in UTC, asset/account identifiers, alert context and evidence references.
3. Follow the checklist and adapt example queries to **your actual index mapping**.
4. Assess benign alternatives. Do not confuse a rule match with a confirmed attack.
5. Record the outcome and escalation reason.
6. Share only redacted screenshots and synthetic data publicly.

## Operational boundaries

Lab exercises and study notes do not constitute production incident handling. Isolation, credential resets, account disablement and blocking require appropriate authorization and playbooks.
