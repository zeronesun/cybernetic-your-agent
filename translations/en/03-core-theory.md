# Chapter 3: Core Theory Detail—Four Cybernetics Concepts

---

This chapter provides an in-depth breakdown of the four core concepts extracted from Qian Xuesen's Engineering Cybernetics: **feedforward, integral control, hierarchical decomposition, and self-monitoring**.

For each concept, we will accomplish the following four goals:
1. **Principle Explanation**: What it is in cybernetics and why it matters.
2. **Agent Predicament**: What problems an Agent falls into without this concept.
3. **Implementation Design**: How to realize it using memory and skills.
4. **A Verifiable Metric**: How you judge that it is already in operation.

---

## 3.1 Feedforward—Blocking Errors Before They Occur

### 3.1.1 Principle Explanation

In cybernetics, feedforward is one of the two fundamental regulation modes alongside feedback.

- **Feedback**: Measure output, detect deviation, then correct input. It is always "after the fact."
- **Feedforward**: Before disturbance enters the system, proactively adjust control signals based on prediction. It is "before the fact."

The most classic feedforward case in engineering technology: A boiler system detects a drop in inlet water temperature and immediately increases firepower, without waiting for steam pressure changes. It measures the "disturbance source," not "output deviation."

Qian Xuesen repeatedly emphasized in Engineering Cybernetics: **High-performance systems must include both feedforward and feedback, and cannot rely solely on feedback.** Feedback corrects remaining error, while feedforward eliminates main disturbances.

### 3.1.2 Why AI Agent Needs Feedforward

Without feedforward, an Agent's working mode is pure feedback:

```
You: Write a short story.
Agent: (Outputs)
You: No AI summary at the end.
Agent: (Corrects)
Next time:
You: Write a short story.
Agent: (Again appears with AI summary)
You: No AI summary at the end!
```

Every error → You correct → It corrects. This "wait until you scold to correct" pattern has several fatal flaws:
- **Wastes conversation turns**: Correction takes up your time.
- **Depends on your vigilance**: If you forget to say it once, the error is delivered directly.
- **Cross-session forgetting**: The last correction only exists in the context of that conversation; new sessions don't recall it.

Feedforward solves this: **Before you say "wrong again," pre-inject things you might care about into the task startup phase.**

### 3.1.3 Implementation Design in Agent

Feedforward is implemented as **"signal preloading during task startup"** in the Agent.

**Specific Mechanism**:
1. Each time a new task begins, the Agent actively extracts information from three data sources:
   - **L2 User Underlying Logic**: Your cross-scenario aesthetics and principles (e.g., "reject AI summary").
   - **L3 Scenario Core Laws**: Success laws for the current task type (e.g., "short stories need open space/leaving room").
   - **Session Archive/Correction Records in Memory**: What was corrected in the last similar task.
2. Compress the above information into a **"pitfall avoidance checklist."**
3. Before formal output, write out the pitfall avoidance checklist (for your confirmation or direct execution).

**Example**: When you ask the Agent to write a short story, it outputs before starting to write:

> Startup Checklist:
> - Task type: Short story creation
> - Pitfall avoidance: ① Leave space at end, no summary, no sublimation; ② No clichés like "as an AI"; ③ Cool narrative, reduce adjective stacking.
> - Last issue: Last time "such is life" appeared at end, already avoided.

Then it begins writing. This layer of feedforward transforms you from "corrector" to "confirmer."

### 3.1.4 How to Verify It Has Taken Effect

Observe the following behaviors:
- Does the Agent actively output a "startup checklist" or "pitfall avoidance checklist" at the beginning of a new task?
- Are similar errors significantly reduced from the first time?
- Has the number of your corrections decreased across 5 consecutive similar tasks?

**Feedforward's goal is not zero errors, but making errors not repeat.**

---

## 3.2 Integral Control—Change What Should Change, Don't Carelessly Change What Shouldn't

### 3.2.1 Principle Explanation

In cybernetics, controllers typically consist of three terms:

- **Proportional Control (P)**: The larger the deviation, the larger the action.
- **Integral Control (I)**: The longer the deviation persists, the action gradually increases.
- **Derivative Control (D)**: The faster the deviation changes, suppress in advance.

The fatal defect of pure proportional control is: **too sensitive to noise.** A single accidental deviation (e.g., sensor jitter) triggers an unnecessary large correction, causing the system to oscillate—left once, right once, never stabilizing.

**Integral Control** is precisely the solution to this problem: it accumulates deviation, only triggering action when accumulated to a certain magnitude. A single jump is averaged out; only continuous, stable deviation triggers correction. This is the meaning of "integral"—**time integration of error, only taking action when exceeding threshold.**

### 3.2.2 Why AI Agent Needs Integral Control

Without integral control, an Agent's response to your feedback often shows two extremes:

- **Over-response**: You casually say once "this ending is bad," it immediately changes the entire writing style, even changing parts you liked before.
- **Sluggish response**: You say five times in a row "don't add plug-in summaries," it agrees every time, but stays the same next time.

Both situations' root cause lies in **not setting "response threshold."** The Agent treats one of your expressions as a permanent rule, or treats your repeated expressions as independent accidental events each time.

Integral control offers a very simple solution: **Only when the same type of feedback appears a second time, treat it as a stable signal to write into long-term memory or modify skills.**

### 3.2.3 Implementation Design in Agent

Integral control is implemented as a **feedback counter with threshold**, stored in memory, named "Integral Control Table."

**Structure**:

| Category | Error Pattern (≤8 chars) | First Date | Cumulative Count | Threshold | Sunk | Sink Target |
| :--- | :--------------- | :------- | :------- | :--- | :----- | :---------- |
| A类  | 结尾AI总结       | 0510     | 2        | 2    | 是     | L2·Aesthetic Principles |
| B类  | 节奏过快         | 0510     | 1        | 2    | 否     | L3·Short Story Laws |

**Running Rules**:
1. When you give negative feedback, the Agent categorizes it into an error pattern (Class A = aesthetic principles, Class B = scenario laws, Class C = skill step errors).
2. Count of same pattern +1.
3. If cumulative ≥ threshold (default 2 times) and not yet sunk, the Agent automatically executes sinking:
   - Write this rule into corresponding L2, L3, or Skill.
   - Update "sunk" status.
   - Confirm with you: "'Ending AI summary' has appeared 2 times, I have sunk it to L2 Aesthetic Principles, do you agree?"
4. If cumulative count = 1, only correct this time, don't modify long-term rules.

**Significance of Threshold Set to 2**:
- 1 time is noise: possibly just bad mood or specific scene unsuitability.
- 2 times is signal: continuous second similar feedback indicates it's likely your stable preference.
- You can adjust to 3 based on your style, but recommend starting with 2.

### 3.2.4 How to Verify It Has Taken Effect

- You intentionally give same type feedback twice (e.g., say "ending too wordy" twice), observe whether the Agent actively proposes modifying long-term rules after the second time.
- You give an accidental feedback (only say once "I don't like this metaphor"), observe whether the Agent doesn't change overall style because of it.

**Integral control's goal is not to make the Agent "stubborn," but to give it stable preference capture capability—won't miss what should be heard, won't overreact to what should be ignored.**

---

## 3.3 Hierarchical Decomposition—Complete Separation of Strategy and Execution

### 3.3.1 Principle Explanation

One of the cores of Qian Xuesen's systems thinking is **hierarchical control**. A complex system must be decomposed into different layers: upper layer defines strategy, defines goals, defines constraints; lower layer does execution, does regulation, does feedback. Between upper and lower layers, information is passed only through clear interfaces; internal implementation is mutually invisible.

If this separation is broken—upper layer starts managing execution details, lower layer starts defining strategy itself—the system falls into chaos: pulling one hair moves the whole body, changing one place causes global oscillation.

### 3.3.2 Why AI Agent Needs Hierarchical Decomposition

An Agent's memory and skills naturally easily fall into several confusions:

- **Memory Bloat**: User principles ("hate AI endings") and specific execution steps ("after writing, search for 'in summary' and delete") are mixed together. Memory stores both "why" and "how," volume explodes, retrieval difficult.
- **Skill Rigidity**: Skills hardcode preferences from a certain conversation, but that preference might be temporary. Next time used, skill is already outdated, yet you don't know why it does that.
- **High Modification Cost**: To change an output style, you have to wade through dense memory and skills, can't distinguish which are "principles" that should change, which are irrelevant "historical records."

Hierarchical decomposition is setting an insurmountable boundary: **principles go into memory, steps go into skills.**

### 3.3.3 Implementation Design in Agent

Core rule has only one:

> **Memory stores only "why" and "what are the laws," skills store only "how."**

Concrete manifestations:

| Information Type                     | Belonging      | Example                             |
| :--------------------------- | :-------- | :------------------------------- |
| Aesthetic tendencies (hate AI endings)   | Memory L2   | User prefers cool narrative, rejects summary conclusions |
| Task laws (short stories must set tone first)     | Memory L3   | Short story creation core law: emotion-tone priority   |
| Execution steps (use gate check after writing) | Skill      | delivery_gate five-gate checklist       |
| A specific correction record           | Archive/Search | 2025-05-10 user said ending too wordy        |

**Forced Rules in Execution**:
- Every closed-loop review, the Agent must actively scan:
  - Is memory having operation steps? If yes, migrate to skills.
  - Are skills having principle content? If yes, migrate to memory.
- Every time writing new memory, the Agent should first judge information belongs to which category, then decide writing location.

### 3.3.4 How to Verify It Has Taken Effect

- You open the Agent's memory and find clear partitions: principles, laws, scenario mappings—no mixed steps.
- You open the Agent's skills and find only checklists of "what to do, what to check," no explanations of "because user likes X so do it this way."
- When you change an aesthetic principle (e.g., "now can occasionally use flowery metaphors"), you only need to modify one memory, no need to touch any skills.

**Hierarchical decomposition's goal is turning memory from "hodgepodge" to "database," letting every piece of information have unique belonging and definite modification path.**

---

## 3.4 Self-Monitoring—Before Delivery, Run Own Gate First

### 3.4.1 Principle Explanation

Any control system, in the end, must have a **feedback loop** closed. In engineering systems, this means: the system measures its own output, compares to expected value, generates error signal to correct.

For an Agent, this "feedback loop" is you—the user—to check output and correct. But if before delivering to you, you can let the Agent run this loop itself first, it equals adding a layer of automated quality inspection. This is **self-monitoring**: system builds an internal quality inspector, pre-checks its own output, only passes pre-inspection before delivery.

### 3.4.2 Why AI Agent Needs Self-Monitoring

An Agent's most common delivery problems:
- **Missing Hard Requirements**: You asked for pure text output, it gave annotated internal version.
- **Too Heavy AI Marks**: "In conclusion," "It's worth noting," "As an artificial intelligence" these clichés you see and are annoyed.
- **Incomplete Structure**: Agreed on three parts, it stopped at two.
- **Unclean Deliverables**: Files carry review notes, internal marks, you still have to manually clean.

These problems if it delivers to you without checking, you check and find out, you waste another conversation turn to correct. Self-monitoring transfers this one conversation turn's checking cost from you to the Agent itself.

### 3.4.3 Implementation Design in Agent

Self-monitoring is implemented as a **pre-delivery gate skill (delivery_gate)**. Before the Agent outputs any final result, it must run this skill, checking item by item.

**Gate Check Items (Five Gates)**:

| Gate   | Priority      | Check Content                                     | Failed Action           |
| :----- | :---------- | :------------------------------------------- | :------------------- |
| First Gate | P0 Hard Block   | Hard requirement check: word count, format, prohibitions, must-includes | Force correction, re-pass gate   |
| Second Gate | P0 Hard Block   | Factual accuracy: code logic, data citation, filename/path  | Uncertain mark "待验证" |
| Third Gate | P1 High Priority | AI traces: clichés, moral summaries, sudden sublimation            | Force deletion             |
| Fourth Gate | P1 High Priority | Structural integrity: logical closed-loop, mandatory steps not missed         | Fill complete                 |
| Fifth Gate | P2 Optimization Suggestion | Delivery cleanliness: remove comments, review notes, extra marks | Cleanse                 |

**Running Steps**:
1. Task complete, ready to deliver.
2. Agent internally calls `delivery_gate`.
3. Scan gate by gate, record pass/not pass.
4. All pass → output final result.
5. Any item not pass → automatic correction → re-pass gate → until all pass then output.

### 3.4.4 How to Verify It Has Taken Effect

- When the Agent delivers, you check: are there still AI clichés? Are there still extra comments? Is format completely meeting requirements?
- Before agent delivery, does it show in reasoning or intermediate output that it's checking (e.g., "Self-checking: P0 hard block passed, P1 AI trace found one spot, deleted").

**Self-monitoring's goal: letting deliverables you receive already be "clean," you only need to confirm, no longer need to be quality inspector.**

---

## 3.5 Collaborative Relationship of the Four Concepts

The four concepts are not independent components but four phases of a system's operation:

1. **Before task startup**: Feedforward injects signals, marking pitfalls in advance.
2. **During task execution**: Hierarchical decomposition ensures info flow clean—upper layer gives direction, lower layer gives execution.
3. **When user feedback**: Integral control decides whether to elevate feedback to long-term rules.
4. **Before task delivery**: Self-monitoring acts as final feedback loop, intercepting unqualified outputs.

And in **periodic retrospectives**, the Agent uses these four as standards to audit all memory and skills, completing self-evolution. This constitutes the complete system architecture panorama that the next chapter will unfold.

---

**Next chapter, we will map these four concepts to the Agent's specific memory and skill structures, showing the complete system architecture design and data flow between layers.**
