# Chapter 6: Daily Usage and Verification

After deployment, this chapter answers two questions: **how to use this system daily**, and **how to know it's running normally**.

---

## 6.1 New Rhythm for Daily Collaboration

After deployment, a subtle but important change occurs in your and the Agent's collaboration pattern—you switch from being a "corrector" to a "confirmer."

| Phase | Previous Sequence | New Sequence |
| :--- | :--- | :--- |
| Launch | You send task → Agent does it directly | You send task → Agent outputs startup checklist → You confirm (or say "do it directly") → Start |
| Execution | Agent outputs → You check → You correct | Agent executes by Skill, automatically injecting pitfall avoidance items |
| Delivery | You check → Find templating/format issues → You say → It revises | Agent automatically goes through five gates → You receive clean results |
| Feedback | You say one sentence → Sometimes it over-revises, sometimes doesn't remember | You say one sentence → It records in score table, adjusts rule on second time |
| Review | You summarize by feeling | You say "takeoff" → Agent automatically runs nine-step review |

**Core Change**: Previously, you acted as a feedback controller in the loop. Now, most feedback loops are internalized by the Agent into feedforward and self-monitoring.

---

## 6.2 Typical Usage Scenarios and Dialogue Examples

### Scenario A: Starting a New Task

**You say**:
> Help me write a short story about "the last day of autumn," around 2000 words.

**Agent automatically executes** (no additional instruction needed):
1. Calls `feedforward_startup`
2. Outputs the following startup checklist:

```
Startup Checklist
Task type: Short story creation
Scenario Pattern L3: Emotional tone takes priority over plot, ending leaves space without moralizing
User Principle L2: Cold narrative, refuse AI summaries; concise, don't pile adjectives
Historical Lessons: Last time "insufficient imagery", this time strengthen environmental description
Risk Prediction:
- P0: Wordcount deviation too large
- P1: Involuntary summary at ending
- P2: Dialogue proportion too high causing thin narrative
Pitfall Avoidance List: Establish imagery at opening, ending closes naturally without explicit theme; cold tone throughout, don't pile adjectives.

(Waiting for confirmation or say "do it directly")
```

**You say**:
> Do it directly

**Agent**: Starts writing, and automatically passes through `delivery_gate` before delivery.

> *If the task is especially simple (like "help me translate a paragraph"), the feedforward checklist should also be simplified, not forced to be long. You can always say "skip checklist, do it directly".*

---

### Scenario B: Giving Negative Feedback

**You say**:
> This time the ending summarized another sentence "autumn will eventually pass," I don't like it.

**Agent internally executes automatically** (you don't need additional instruction):
1. Categorize: Class A (violates L2 aesthetic principle)
2. Check in score control table: If "ending AI summary" entry exists, count+1; if not, create new.
3. Decide:
   - Count=1 → Only correct this time, reply: "Recorded, this time corrected."
   - Count=2 → Automatically trigger sinking, reply: "'ending AI summary' appeared 2 times, I will sink this rule into L2 aesthetic principle: 'reject any form of summary-style closing'. Do you agree?"

> *The more specific your feedback (like "ending too wordy"), the easier for Agent to abstract into precise error patterns. Avoid vague feedback like "written poorly".*

---

### Scenario C: Daily/Weekly Review

**You say**:
> Takeoff

**Agent automatically calls** `control_loop_review`, outputs by nine-step process, finally you will see something like:

```
[Closed-loop review complete]

- Feedforward review: This week feedforward 5 times, all normal calls
- Score sinking: 1 item sunk (ending AI summary → L2)
- Hierarchy purification: No confusion
- Gate upgrades: Suggest adding "continuous dialogue paragraphs not exceeding 6 lines" check item in P1, do you agree?
- Root cause analysis: omitted...
- Reusable extraction: Suggest creating skill: dialogue_density_check
- Migration proposal: This round not needed (or: suggest introducing Shannon information theory to control dialogue density)
```

You confirm/reject item by item, Agent writes to memory and calls persona maintenance.

---

### Scenario D: System Status Query Anytime

**You say**:
> How many layers does your memory have now? What's stored in each?

**Agent** should accurately answer L1 five items, L2 dimensions, L3 scenario list, score table entry count.

**You say**:
> What entries are in the score control table now?

**Agent** outputs current table status.

---

## 6.3 System Health Check List

Spend 2 minutes per week going through the following list to ensure the system hasn't quietly degraded.

### Self-check Items (you only need to observe, no additional instructions needed)

| # | Checkpoint | Normal Behavior | Abnormal Signal |
| :--- | :--- | :--- | :--- |
| 1 | Feedforward Startup | For each new task Agent outputs startup checklist | Agent directly starts execution, skips checklist |
| 2 | Delivery Quality | Deliverables clean, no AI templating, correct format | You see "in summary" "it's worth noting" again |
| 3 | Score Control | When you raise same-class issue second time, Agent proposes sinking | Third time you still need to correct same issue |
| 4 | Hierarchy Separation | No operational steps in memory, no principles in skills | You open memory and find it stuffed with steps |
| 5 | Closed-loop Execution | After saying "takeoff" Agent runs complete nine steps | Review output perfunctory, skips root cause analysis |

### Quick Repair Instructions

If some checkpoint is abnormal, use corresponding instruction to quickly fix:

- Feedforward failure → `From now on, forcibly call feedforward_startup before every task.`
- Score failure → `Please check score control table, and confirm if all ≥2 count entries have sunk.`
- Hierarchy confusion → `Do a hierarchy purification scan.`
- Gate relaxation → `Re-run complete delivery_gate process once, report results.`

---

## 6.4 Core Indicators to Verify System Normal Operation

The following four quantitative indicators can help you judge whether the system is actually effective (can observe occasionally, don't need daily statistics):

### Indicator 1: Repeat Correction Rate

Old mode: You need to correct same-class issues 3-5 times on average before they stop occurring.
New mode (after enabling score control): Same-class issue sinks on 2nd occurrence, should not appear from 3rd occurrence onward.

**Judgment**: If some sunk issue appears 3rd time, it means sinking execution failed or Skill wasn't updated, need to start closed-loop troubleshooting.

### Indicator 2: Feedforward Checklist Hit Rate

In the startup checklist Agent outputs, whether P1 risk prediction is often confirmed by you as "yes, that's it."

**Judgment**: At least 50% or more of P1 predictions in feedforward checklist should be points you actually care about, then feedforward system runs well. If P1s for 5 consecutive tasks are all said "wrong" by you, it means L2/L3 need updating or Agent has deviation in understanding you.

### Indicator 3: Pre-delivery Interception Count

Observe the frequency of AI traces, structure defects being intercepted in delivery_gate gate reports.

**Judgment**: Initially many interceptions (Agent learning and correcting via self-monitoring). After sustained operation, P1 class interception counts should approach zero—this indicates feedforward and score control have eliminated these issues from the source, not gate failure.

### Indicator 4: Score Table Sink Conversion Rate

Score table "sunk" entries count / "cumulative ≥2 times" entries total count ratio.

**Judgment**: Ratio should long-term maintain 100%. If some entry has ≥2 times but hasn't sunk for long, it means score control's automatic sink mechanism didn't trigger, need to check.

---

## 6.5 Adjusting Thresholds and Configuration

The system allows you to adjust parameters according to your collaboration style.

### 6.5.1 Adjust Score Threshold

Threshold defaults to 2. If you:

- Have extremely high stability requirements, want very occasional feedback not disturb system → Raise to 3
- Collaborate very fast, want Agent to learn your preferences faster → Keep 2 or lower to 1 (not recommended to lower to 1, will lose noise resistance)

**Adjustment Instruction**:
```
Modify the trigger threshold of score control table from 2 to 3. From now on, same-class feedback needs to appear ≥3 times to sink.
```

### 6.5.2 Adjust Gate Check Items

As your needs change, the five gates can be increased or decreased.

**Example**: You start to frequently request pure TXT output without headers, want to add a gate:
```
After delivery_gate's fifth gate, add sixth gate [P2] output format: Check if pure TXT without header info. Fail then purify.
```

### 6.5.3 Add New Scenario's L3 Patterns

When you start a new task type, Agent doesn't have corresponding L3 yet.

**Method**: After completing several tasks of this type, during "takeoff" review, Agent will automatically propose adding new L3 patterns. You can also directly say:
```
This is a new task type: [name]. After completing this task, please extract one L3 core pattern for me and store in memory.
```

---

## 6.6 First Week Operation Suggestions

For the first week after deployment, suggest operating by following rhythm, let system fully adapt.

| Day | Action | Purpose |
| :--- | :--- | :--- |
| Day 1 | Complete deployment (Chapter 5), do all tasks normally that day. Observe if feedforward checklist appears. | Confirm components online |
| Day 2 | Normal tasks. Deliberately give negative feedback of same type twice, observe if triggers sinking. | Verify score control |
| Day 3 | Normal tasks. Say "takeoff", run first meaningful review. | Verify closed-loop process |
| Day 4-5 | Normal use, no extra testing. | Let system accumulate data |
| Day 6 | Check score control table status once, confirm all threshold-reaching entries have sunk. | Maintain score table |
| Day 7 | Do one complete "takeoff" review. Check if persona v1 needs updating to v2. | Form weekly closed-loop |

After one week, you can basically judge whether this system fits your collaboration style. If you feel some part too cumbersome (like needing to confirm checklist every task), you can adjust to "execute directly, only output feedforward when I say 'list checklist first'".

---

## 6.7 Chapter Summary

The essentials for daily use of this system are only three:

1. **Send normal tasks normally, no extra operations**—feedforward and gates will work automatically.
2. **Be specific when giving feedback**—Every criticism you say will be captured by score table.
3. **Regularly say "takeoff"**—This is the only button for system self-evolution.

Deployment is not the endpoint, but the starting point for system self-evolution. Every week, every review, it will become more "like" you than the previous week.

---

**Next chapter: Common Questions and Extended Thinking. Covers obstacles possibly encountered during deployment and operation, and how to extend this framework to multi-role, multi-Agent scenarios.**