# SOC Search Cookbook — Educational Examples

**Status:** Unexecuted reference queries. Check data schema, permissions, timestamps and the exact event source before use.

## Splunk: group failed Windows logons by host and account

```spl
index=YOUR_WINDOWS_INDEX (EventCode=4625 OR EventID=4625)
| eval user=coalesce(TargetUserName, Account_Name, user)
| stats count as failures min(_time) as first_seen max(_time) as last_seen by host user
| convert ctime(first_seen) ctime(last_seen)
| sort - failures
```

**Goal:** Identify clusters for triage, not declare brute force. Your environment may use different extracted fields.

## Splunk: examine authentication timeline

```spl
index=YOUR_WINDOWS_INDEX (EventCode=4624 OR EventCode=4625 OR EventID=4624 OR EventID=4625)
| eval event_id=coalesce(EventCode, EventID)
| eval user=coalesce(TargetUserName, Account_Name, user)
| table _time host user event_id Source_Network_Address Logon_Type
| sort _time
```

**Goal:** Compare failures and successes with surrounding context. Replace field names with those found in your indexed events.

## Wazuh Dashboard / OpenSearch Discover: example filter

```text
agent.name: "WIN-LAB-01" AND (data.win.system.eventID: "4625" OR data.win.system.eventID: "4624")
```

**Important:** This is an illustrative query-string-style filter, **not a tested universal Wazuh syntax**. Actual dashboard KQL/DQL support, selected data view and mappings vary. In some installations event IDs are numeric or field paths differ; inspect one real document to confirm. Where the dashboard does not support this syntax, use its visual filters for host and event ID.

## What to record when executing

| Field | Value |
|---|---|
| Lab date / timezone | TBD |
| Wazuh or Splunk version | TBD |
| Data source and index | TBD |
| Observed field mappings | TBD |
| Query modified for schema | TBD |
| Number of returned events | TBD |
| Findings / benign alternatives | TBD |

Never paste passwords, tokens, private customer events or confidential IP details into a public GitHub repository.
