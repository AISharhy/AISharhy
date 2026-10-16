# SOC L1 Alert Triage Checklist

> Template for learning / authorized investigations; use organizational procedures in real environments.

## Intake
- [ ] Assign case ID, UTC timestamp and detection name.
- [ ] Capture source product, rule, severity and analyst queue.
- [ ] Determine affected host, account and available network context.
- [ ] Verify alert and log ingestion quality (missing fields, clock skew, duplicates).

## Enrichment
- [ ] Identify asset criticality and whether the account has elevated permissions.
- [ ] Confirm event timeline and related logs.
- [ ] Review endpoint process tree and network connections **if available**.
- [ ] Check for legitimate maintenance, user activity or expected automation.
- [ ] Separate confirmed evidence from untested hypotheses.

## Decision
- [ ] Determine if information is sufficient for classification.
- [ ] Identify likely benign alternatives or false-positive causes.
- [ ] Add ATT&CK technique mapping **only if defensible**.
- [ ] Evaluate escalation under applicable policy and SLAs.
- [ ] Avoid disruptive response actions without authorization.

## Handoff
- [ ] Concise summary: who, what, when, where, observed impact.
- [ ] Include evidence references and field values (sanitized if public).
- [ ] State confidence, missing data and recommended next steps.
- [ ] Document case status and next owner.

## Example analyst handoff

**Case:** LAB-001 (fictional)  
**Observed:** Multiple Windows 4625 failed logons for one test account in five minutes.  
**Correlated:** Later 4624 in example event stream; no device context available.  
**Assessment:** Suspicious pattern, not confirmed credential compromise.  
**Action:** Validate user/device legitimacy and escalate if critical or outside baseline.  
**Limits:** No production evidence; scenario only.
