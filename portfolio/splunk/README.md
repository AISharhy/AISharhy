# Splunk SOC Investigations — SPL Study Examples

**Status:** Educational sample searches; not validated against a specific deployed Splunk index or schema.

## Before you run these

Set an appropriate time picker and replace `YOUR_WINDOWS_INDEX` and field names with those observed in your environment. Some deployments parse Windows events as `EventCode`, others as `EventID`; source types and field extractions vary.

## 1 — Windows failed logons (Event ID 4625)

```spl
index=YOUR_WINDOWS_INDEX (EventCode=4625 OR EventID=4625)
| stats count as failures by host, Account_Name
| sort - failures
```

If `Account_Name` is not populated in your data, inspect raw events and choose the actual normalized username field. An increased count is a signal for triage, **not proof of brute force**.

## 2 — Failed vs successful logon overview

```spl
index=YOUR_WINDOWS_INDEX (EventCode=4624 OR EventCode=4625 OR EventID=4624 OR EventID=4625)
| eval event_code=coalesce(EventCode,EventID)
| stats count by host, event_code
| sort host, event_code
```

## 3 — Sysmon process execution (Event ID 1)

```spl
index=YOUR_WINDOWS_INDEX (EventCode=1 OR EventID=1) (source="*Sysmon*" OR sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational")
| table _time host User Image ParentImage CommandLine
| sort - _time
```

**Caution:** This depends heavily on the source, source type and event field mappings. Confirm ingestion of Sysmon Operational logs and inspect real schema before using in analysis.

## Analyst notes

- Check data completeness and timezone before conclusions.
- Review event context and source reliability.
- Avoid saving real tokens, passwords, customer names or production logs in public repositories.
- Record test results only after execution in an authorized lab.
