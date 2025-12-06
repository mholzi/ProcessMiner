# SEPA Direct Debit Process Chart
**Source:** Uploaded by SME (simulated)
**Format:** Process Flow Chart
**Date:** 2025-12-03

---

## Process Flow: SEPA Direct Debit Execution

```
[START]
    |
    v
+---------------------------+
| 1. Receive DD Collection  |
|    File from Client       |
+---------------------------+
    |
    v
+---------------------------+
| 2. Validate File Format   |
|    (pain.008 / XML)       |
+---------------------------+
    |
    v
+---------------------------+
| 3. Check Mandate Status   |
|    in Mandate Database    |
+---------------------------+
    |
    +-------[Invalid]-------> [Reject & Notify Client]
    |
    v [Valid]
+---------------------------+
| 4. Apply Cut-off Time     |
|    Check                  |
+---------------------------+
    |
    v
+---------------------------+
| 5. Submit to Clearing     |
|    (STEP2 / EBA)          |
+---------------------------+
    |
    v
+---------------------------+
| 6. Process Settlement     |
|    on Due Date            |
+---------------------------+
    |
    v
+---------------------------+
| 7. Handle Returns (R-Tx)  |
|    if applicable          |
+---------------------------+
    |
    v
[END]
```

---

## Key Information from Chart

### Systems Mentioned:
- Mandate Database
- STEP2 / EBA Clearing
- Client File Interface

### Checkpoints:
- File format validation
- Mandate validation
- Cut-off time check

### Exception Path:
- Invalid mandate -> Reject & Notify Client
