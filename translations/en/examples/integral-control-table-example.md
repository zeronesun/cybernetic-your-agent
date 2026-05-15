# Integral Control Table Example

This file shows the actual running status of the integral control table after one month, along with a typical sinking dialogue example.

> **Note**: The entries below are fictional and used only to demonstrate the data structure and operating logic.

---

## Integral Control Table After One Month of Operation

```
[Integral Control Table]
| Category | Error Pattern (≤8 chars) | First Date | Cumulative Count | Threshold | Sunk | Sinking Target                           |
| -------- | ------------------------ | ---------- | ---------------- | --------- | ---- | ---------------------------------------- |
| A type   | Ending AI summary        | 2025-05-10 | 2/2              | 2         | Yes  | L2·Aesthetics: Reject summary closure   |
| A type   | Tone too enthusiastic    | 2025-05-12 | 1/2              | 2         | No   | -                                        |
| B type   | Short scene insufficient | 2025-05-10 | 2/2              | 2         | Yes  | L3·Short story: Opening establishes scene |
| B type   | Code without tests       | 2025-05-15 | 1/2              | 2         | No   | -                                        |
| C type   | Gate漏检AI套话          | 2025-05-10 | 2/2              | 2         | Yes  | delivery_gate: P1 platitude detection rules upgraded |
| C type   | Feedforward no archive   | 2025-05-18 | 1/2              | 2         | No   | -                                        |
| D type   | Wrong metaphor instance   | 2025-05-08 | 1                | -         | -    | (Occasional, not counted)               |
```

---

## Sinking Trigger Example

### Scenario: User Second Time Points Out "Ending AI Summary"

**User**:
> This ending has a sentence again "Life goes on anyway," and I don't like this kind of summary.

**Agent's Internal Process**:
1. Error classification → A type (violatesL2 aesthetic principle)
2. Search in integral table → Found "Ending AI summary," cumulative count from 1 becomes 2
3. Count = threshold 2, triggers sinking

**Agent Output**:
> Recorded. "Ending AI summary" has occurred 2 times. I recommend sinking this rule to **[L2·User Underlying Logic] Aesthetic Orientation**, adding entry: **"Reject any form of summary closure"**.
>
> Do you agree?

**User**:
> Agree.

**Agent Execution**:
1. Write this entry in L2
2. Update integral table: Sunk → Yes
3. Confirm: "Sunk complete. In future creations, I will actively load this principle during feedforward startup."

---

## Per-Stage Closed-Loop Review Integral Table Report Example

> This stage the integral control table has 7 records in total:
> - 3 already sunk (Ending AI summary, scene insufficient, Gate漏检AI套话), no further handling needed
> - 3 below threshold (Tone too enthusiastic, Code without tests, Feedforward no archive), all at 1/2 times, continue observation
> - 1 occasional event (Wrong metaphor instance), not counted in cumulative system
>
> Current sinking conversion rate: 100% (all reaching threshold have been sunk)

---

## How to Check if Your Integral Table is Working Normally

Observe the following signals:
- After each negative feedback, does Agent clearly classify and accumulate
- For items with cumulative ≥ 2, does Agent actively propose sinking
- After sinking, does the same problem no longer occur
> In monthly closed-loop reviews, are sunk items in integral table clearly traceable
