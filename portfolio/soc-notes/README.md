# SOC Analyst L1 — Practical Knowledge Base

**Purpose:** Concise learning notes for technical interviews and day-to-day analyst fundamentals.

## What a SOC L1 analyst does

Monitor security events, validate alerts, establish context, consult playbooks, document findings and escalate when warranted. An L1 analyst should avoid taking disruptive containment actions without authorization.

## SIEM vs EDR/XDR

- **SIEM (e.g., Wazuh, Splunk):** Collects and searches events from multiple sources; detection and correlation capabilities vary by product and configuration.
- **EDR (e.g., Cortex XDR endpoint capabilities):** Provides detailed endpoint visibility and investigation/response capabilities.
- **XDR:** Extends detection and response through integrated telemetry and analytics across supported security domains; exact coverage is vendor-specific.

## Alert vs incident

An **alert** is a signal requiring evaluation. An **incident** is a security event (or set of events) assessed under an organization's incident criteria. Not every alert is an incident.

## Networking interview quick notes

- **DNS:** Resolves domain names to records; inspect query patterns and response context.
- **TCP three-way handshake:** SYN → SYN/ACK → ACK; establishes a connection.
- **HTTP/HTTPS:** HTTP is an application protocol; HTTPS adds TLS protection in transit.
- **Firewall:** Enforces traffic rules; logs can help explain allowed or blocked connections.
- **NAT:** Translates network addresses; understand how translated addresses affect log correlation.

## When an endpoint alert arrives

1. Record host, username, detection name, time and source.
2. Verify telemetry and policy context.
3. Review process tree, hashes, parent/child relationships and related connections **where data is available**.
4. Check business legitimacy and benign causes.
5. Classify with explicit confidence and evidence.
6. Follow the approved escalation and incident-response playbook.

## Honest interview description

> "I have used Wazuh, Splunk, and Palo Alto Cortex XDR in learning and guided SOC exercises. I am developing my ability to validate alerts, correlate logs and explain escalation decisions. I distinguish training experience from autonomous production responsibility."

## Next exercises

- Complete a sanitized Wazuh event-ingestion walkthrough.
- Run and document a Splunk query in a lab.
- Write one evidence-backed incident report from a simulated scenario.
