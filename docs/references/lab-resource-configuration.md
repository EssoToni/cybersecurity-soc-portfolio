# Lab Resource-Saving Configuration

**Date:** 2026-10-30  
**Scope:** Linux Wazuh agent, manager-side ingestion, lab VM resources.

This document records the deliberate configuration choices made to keep the lab
stable and within the limits of the available hardware. Each choice notes the
trade-off it introduces.

## 1. Agent-side buffer and event rate (`client_buffer`)

The Wazuh agent uses a **leaky bucket queue** to prevent a burst of events from
saturating the network or the manager. The relevant block is in
`/var/ossec/etc/ossec.conf` on the Linux endpoint:

```xml
<client_buffer>
  <disabled>no</disabled>
  <queue_size>5000</queue_size>
  <events_per_second>500</events_per_second>
</client_buffer>