# Xicoy ProHub telemetry — notes

This document is a lightweight memo about ProHub sensor mapping and what the widget expects on the ETHOS side.

## Key points
- Sensor *names* can vary (users can rename sensors in ETHOS).
- Identifying sensors by **ID/instance** is usually more robust than relying on display names.
- If you see inconsistencies (values stuck, unexpected units), review:
  - ETHOS sensor discovery
  - sensor units / scaling in ETHOS
  - ProHub firmware / adapter configuration

## If you want to document a precise mapping
Add a table here with:
- AppId / instance
- display name
- unit
- expected range
