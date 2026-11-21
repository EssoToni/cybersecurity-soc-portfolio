# Lab Resource Configuration

Date: 2026-10-30 (initial)
Updated: 2026-11-21 (observed allocations; Sections 2 to 4 added)

Scope: Wazuh agent ingestion behaviour, per-VM resource allocation, and the
choices made to keep the lab stable within the available hardware.

## 1. Agent-side buffer and event rate (client_buffer)

The Wazuh agent uses a leaky bucket queue to prevent a burst of events from
saturating the network or the manager. The relevant block is in
`/var/ossec/etc/ossec.conf` on each Linux endpoint:

```xml
<client_buffer>
  <disabled>no</disabled>
  <queue_size>5000</queue_size>
  <events_per_second>500</events_per_second>
</client_buffer>
