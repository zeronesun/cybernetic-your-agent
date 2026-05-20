# Chapter 4: System Architecture in Detail - Three-Tier Memory + Skill Layer

The previous three chapters addressed "why" and "what" questions respectively. This chapter assembles them into a complete, practically runnable **system architecture**, giving the four cybernetics concepts clear positioning and data flow patterns within the Agent's memory and skill system.

---

## 4.1 Architecture Overview

The core principle of this architecture is: **Define cognitive boundaries through logical layering, implement storage and execution separation through physical layering**.

```
┌────────────────────────────────────────────┐
│          Your Agent (Controlled System)    │
├────────────┬───────────────────────────────┤
│  Logical   │  Physical Storage              │
├────────────┼───────────────────────────────┤
│  L1 Meta-cognition  │  Memory Top Region (immutable)         │
│  L2 User Logic      │  Memory Main Body Region              │
│  L3 Scenario Rules  │  Memory Main Body Region              │
│  Integral Control   │  Memory Main Body Region              │
├────────────┼───────────────────────────────┤
│  Execution  │  Skill Modules                 │
│  Feedforward List   │  Session Context (temporary)          │
│  Historical Correction Record │ Session Archive (long-term readonly)│
└────────────┴───────────────────────────────┘
         ↑ ↓ Control Flow and Data Flow
    ┌─────┴──────┐
    │  Your Task   │ ← Controlled System
    └────────────┘
```

Each layer has strict information entry criteria, expanded below.

---

## 4.2 L1: Metacognitive Framework - System Constitution

### 4.2.1 Positioning

L1 is the Agent's "thought constitution," defining **how it processes information, how it evaluates its own behavior, and how it makes decisions**. It does not target any specific task or user preference, but imposes mandatory constraints on the Agent's way of operation itself.

### 4.2.2 Physical Storage

- **Location**: Top region of `memory` (e.g., the frontmost position in Hermes's `memory(target='memory')`).
- **Property**: **Immutable by self-modification**. The Agent can *suggest* modifications during closed-loop reviews, but must await user confirmation. This ensures the system skeleton will not be accidentally distorted by the Agent's own evolution process.

### 4.2.3 Content Structure

L1 stores specific behavioral guidelines for the four cybernetic concepts, not abstract definitions. Each guideline must satisfy:
- Start with "You must" or "You must not."
- Include clear trigger conditions and execution actions.
- Short enough to load entirely into context at once.

**Standard Entry Examples**:

```
① Feedforward: When each new task starts, you must first retrieve L2, L3, and session archives,
   output a "startup checklist" and pre-assess P0-P3 risks.
② Integral Control: When receiving negative feedback, you must record it in the integral control table.
   When similar accumulations reach ≥2 occurrences, propose a下沉 (consolidation) plan and confirm with the user.
③ Hierarchical Separation: Content you write to memory may only contain "principles/rules,"
   and must not contain operation steps. Operation steps must be written to skills.
④ Self-Monitoring: Before delivering any result, you must execute delivery_gate,
   passing all five gates before outputting the final result.
⑤ Root Cause Analysis: In closed-loop review, for each problem you must ask down to the level of "rule error" or "execution error."
```

Total entries are recommended to be controlled within 5-7, ensuring the Agent can recollect them completely at once.

---

## 4.3 L2: User Underlying Logic - Your "Principle Repository"

### 4.3.1 Positioning

L2 stores your **stable preferences and core principles** spanning different tasks. These preferences are not limited to specific scenarios, but define the basic behavioral direction of the Agent's collaboration with you.

If L1 is the cybernetic shell, L2 is **your personalized kernel**, a computable model of your judgment patterns by the Agent.

### 4.3.2 Physical Storage

- **Location**: Main body of `memory`, immediately following L1.
- **Update Permissions**: Written by the Agent during integral consolidation or closed-loop review, subject to your confirmation.
- **Capacity Control**: Each entry ≤ 30 characters, total ≤ 10 entries (adjustable). Avoid L2 inflating into a "memo," forcibly preserving only cross-scenario stable principles.

### 4.3.3 Content Structure and Examples

**Organization**: Grouped by dimension for easy retrieval.

| Dimension          | Storage Example                           | Notes                     |
| :----------------- | :----------------------------------------- | :------------------------ |
| Communication Style | User preference: concise and direct, no pleasantries | Don't output "Hope this helps you" |
| Output Standard   | User requirement: code first with verification methods | Don't just give solutions, give "how to verify" |
| Decision Pattern  | User decision: risk upfront, expose complete risks first | List risks first, then discuss returns |
| Aesthetic Orientation | User aesthetics: cold narrative, rejects AI-style summary | Novel endings leave blank, don't elevate |

**Key Constraints**:
- No specific scenarios: e.g., "how short story creation should be" belongs in L3.
- No operation steps: e.g., "delete summary in the third step" belongs in Skills.
- Each entry must be an abstraction of user judgment, not a description of task results.

### 4.3.4 Interfaces with Other Layers

- **Called by L1 Feedforward**: When a task starts, Agent reads relevant dimensional principles from L2, integrating them into the avoidance checklist.
- **Written by Integral Control**: When an aesthetic principle accumulates 2 feedback occurrences, Agent consolidates it into L2.
- **Audited by Closed-Loop Review**: Each review checks whether L2 is outdated or whether new principles need adding.

---

## 4.4 L3: Scenario Core Rules - Task "Success Password"

### 4.4.1 Positioning

L3 stores **success rules** for specific task types. It answers: "When doing this type of task, what rules must be followed to do it correctly."

L2 is a cross-scenario "axiom," L3 is a scenario-related "theorem." An L3 entry should be condensed wisdom for a task type, not an operation manual.

### 4.4.2 Physical Storage

- **Location**: Main body of `memory`, below L2, organized by task type nodes.
- **Update Permissions**: Same as L2, written through integral consolidation or closed-loop review, subject to your confirmation.
- **Capacity Control**: 1-3 rules per task type, each expressing "the core contradiction or most critical principle in this scenario" in one sentence.

### 4.4.3 Content Structure and Examples

**Organization**: Divided by task type nodes, 1-3 entries under each node.

```
[L3·Scenario Core Rules]

- Short Story Creation:
  • Emotional tone setting takes priority over plot development
  • Endings leave blank, no value summary
- Code Review:
  • First check architectural rationality and boundary conditions, then naming conventions
  • Each category of problem must provide modification suggestions, not just point out errors
- Issue Troubleshooting:
  • First locate log root causes, do not guess from experience
  • Mark uncertain points as "to verify," do not force conclusions
- Architecture Design:
  • First define system boundaries and data flows, then select tech stack
  • Evaluate scalability and failure modes, not just write happy path
```

**Key Constraints**:
- "Rules" must be able to drive Skill design: if an L3 cannot enable Skill to write checklist items, it's not abstract or essential enough.
- Prohibit filenames, tool names, and other easily outdated information.
- Prohibit "what to do in step three" and similar operation steps.

### 4.4.4 Relationship with Skill Layer

L3 is the **design specification** for the skill layer. A Skill should be an execution pipeline derived from corresponding L3 rules. When closed-loop review finds execution results problematic, first check Skill steps (execution layer); if Skill has no errors, then check whether L3 rules were extracted incorrectly (strategy layer).

---

## 4.5 Integral Control Table - System "Feedback Threshold Regulator"

### 4.5.1 Positioning

The integral control table is the physical carrier of cybernetic concept #2 (integral control). It's a lightweight structured log recording **repeated error patterns and their disposition status**.

### 4.5.2 Physical Storage

- **Location**: Main body of `memory`, independent node.
- **Operation**: Automatically maintained by Agent when receiving negative feedback, no need for your manual management.

### 4.5.3 Data Structure

| Field          | Description                                              | Example               |
| :------------- | :------------------------------------------------------- | :-------------------- |
| Category       | Class A (violates L2) / Class B (violates L3) / Class C (Skill step error) | B Class               |
| Error Pattern  | Abstract extraction within 8 characters                  | "Short story ending AI summary" |
| First Date     | Date of first occurrence                                  | 2026-05-10            |
| Accumulated Count| Current accumulated count                                | 2/2                   |
| Threshold      | Default 2                                                | 2                     |
| Consolidated   | Whether written to L2/L3/Skill                            | Yes                   |
| Consolidation Target| Which position consolidated to                         | L3·Short Story Creation|

### 4.5.4 Operation Logic

When user gives negative feedback → Agent abstracts to error pattern → searches table for similar patterns:
- Exists and reached threshold: prompt user, this pattern has consolidated.
- Exists and not reached threshold: increment count by 1. If threshold reached, auto-consolidate and confirm.
- Does not exist: create new entry, count set to 1.

Each closed-loop review must output the complete state of this table.

---

## 4.6 Execution Layer: Skills - Operation Pipeline

### 4.6.1 Positioning

The skill layer is the system's **hands and feet**, responsible for all specific operations. It includes three types of skills:

| Type           | Example                                                         | Corresponding Cybernetic Concept |
| :------------- | :--------------------------------------------------------------- | :------------------------------- |
| Meta Skills    | `feedforward_startup`, `delivery_gate`, `control_loop_review`    | Feedforward, self-monitoring, closed-loop |
| Task Skills    | `short_story_writer`, `code_reviewer`, etc.                     | Driven by L3                     |
| Maintenance Skills | `user_profile_maintainer`                                   | Profile maintenance              |

### 4.6.2 Skill Design Specification

Each skill must contain the following fields (using `short_story_writer` as example):

```
- Trigger Condition: When user requests a short story
- Dependent L3: [L3·Short Story Creation] emotional tone priority, ending blank
- Feedforward Injection: Load L2 aesthetic orientation + L3 corresponding rules
- Execution Steps:
  1. Confirm theme and word count
  2. Determine emotional tone (cold/warm/suspense)
  3. Writing (establish visual feel in first three sentences)
  4. ……
- Self-check Steps: Call delivery_gate five-gate scan
```

No skill may hardcode "user preferences" in steps; preferences must be injected through feedforward. This ensures when you modify an aesthetic principle in L2, all skills automatically take effect without individual modification.

### 4.6.3 Skill Versioning

Each skill name has a version suffix (e.g., `_v1`); when updating, create a new version and keep the old one for reference. Versioning lets you roll back anytime and facilitates comparing modifications during closed-loop reviews.

---

## 4.7 Data Flow Overview: How a Task Travels Through All Layers

Using "write a short story" as example, showing complete data flow:

```
Task: Write Short Story
  │
  ├─[1. Feedforward Startup] Skill: feedforward_startup
  │    ├─ Read L1: Confirm feedforward rules
  │    ├─ Read L2: Extract "cold narrative, reject AI summary"
  │    ├─ Read L3: Extract "short story: emotional tone priority, ending blank"
  │    ├─ Retrieve Archive: Last correction "insufficient visual feel"
  │    └─ Output "startup checklist" → await confirmation
  │
  ├─[2. Task Execution] Skill: short_story_writer
  │    ├─ Inject avoidance items from feedforward checklist
  │    ├─ Organize content according to L3 rules
  │    └─ Complete first draft
  │
  ├─[3. Delivery Self-check] Skill: delivery_gate
  │    ├─ P0: Hard requirement check
  │    ├─ P1: AI traces + structural integrity
  │    ├─ P2: Delivery cleanliness
  │    └─ All pass → output final draft
  │
  └─[4. User Feedback → Integral Control]
       ├─ Negative feedback → abstract to pattern
       ├─ Write to integral control table
       ├─ If accumulation ≥2 → consolidate to L2/L3/Skill
       └─ Wait for next task's feedforward call
```

**Closed-Loop Review (run periodically)**:
1. Trigger (user says "take off").
2. Agent calls `control_loop_review`.
3. Audit all L2, L3, Skills, integral tables according to L1's four standards + root cause analysis standard process.
4. Output rectification plan.
5. Call `user_profile_maintainer` to update profile.

---

## 4.8 Architecture Self-Preservation Mechanisms

To prevent the system itself from "drifting" or "inflating," three self-preservation rules are built in:

1. **L1 Unmodifiable by Self**: Agent wanting to modify L1 must propose and await confirmation.
2. **L2/L3 Entry Limits**: upper limits of 10/3 entries per category; exceeding prompts user to clean outdated entries.
3. **Skill Versioning and Deprecation**: old version skills archived or deleted after confirmed useless, preventing accumulation.

---

## 4.9 Chapter Conclusion

This chapter presents a complete system architecture with **cybernetics four concepts as logical layers, memory and skills as physical layers, and data flow as operational neurons**. It is essentially a set of "design patterns," a re-planning of the Agent's memory and skill system, not adding new features.

**In the next chapter, we will translate this architecture into directly executable deployment instructions, building a complete cybernetic engine on your Agent step by step in sequence.**
