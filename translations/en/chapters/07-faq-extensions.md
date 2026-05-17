# Chapter 7: FAQ and Extended Thinking

This is the final chapter of the tutorial, covering two sections: typical obstacles encountered during deployment and operation and their solutions, as well as ideas for extending this framework to more complex scenarios.

---

## 7.1 Deployment-related Questions

### Q1: After I write to L1, the Agent doesn't execute according to the Five Core Rules. What should I do?

**Common causes:**
- Memory is not pinned to the top and gets overwritten or diluted by subsequent writes
- The context window gets squeezed by long conversations, causing L1 to be truncated
- The Agent platform has delays in memory injection timing

**Troubleshooting steps:**
1. Ask the Agent to recite the Five Core Rules of L1. If it cannot recite them completely, there is a problem with memory writing or reading.
2. If it recites correctly but still doesn't execute, restate at the beginning of a new session: `Before starting this session, first review the Five Core Rules of the L1 metacognitive framework in memory.`
3. If the problem persists, consider simplifying the core rules of L1 to one or two sentences and writing them to the platform's "system instruction" or "system prompt" area (if supported) as a double insurance.

---

### Q2: The Agent says it doesn't have `skill_manage` functionality or similar skill management tools

**Two solutions:**

**Solution A (Recommended)**: Simulate skills with memory.
- create memory entries marked `[Skill-SkillName]` in memory, with the content being the skill's operating steps.
- Add a rule to L1: `Each time a skill needs to be executed, retrieve the corresponding [Skill-*] entry from memory and execute strictly according to the steps.`
- Disadvantage: Takes up memory space; Advantage: Logic is complete.

**Solution B**: Simplify architecture, using only L1 + L2 + L3 + Score Control Table.
- Abandon automation at the skill layer, and instead manually remind the Agent at the start of tasks to follow self-check steps.
- Suitable for light use or short-term collaboration.

---

### Q3: When initializing L2/L3, the Agent's extraction of my preferences is completely inaccurate

This doesn't mean the architecture has problems, but rather indicates that the Agent previously had biases in understanding you—which is exactly what this tutorial aims to solve.

**Handling method:**
- Don't accept the Agent's extraction blindly. Correct item by item, treating it as a "calibration conversation."
- After correction, clearly tell the Agent: `Your previous understanding of me had biases. I have corrected the content of L2/L3. Please use my correction as the standard in memory.`
- In subsequent closed-loop reviews, the Agent will automatically update its understanding. Typically after 2-3 reviews, the accuracy of L2/L3 will significantly improve.

---

### Q4: Items in the score control table are increasing. What should I do?

This is a signal that the system is operating normally—it shows you are indeed collaborating continuously and the Agent is continuously learning.

**Maintenance strategy:**
1. Check the score table during each "takeoff" review.
2. For items that have sunk and are running stably, archive them as "solidified" to reduce the number of active items.
3. For items misclassified or no longer applicable, manually delete them.

```
Move "ending AI summary" from the score control table to the archive area (no recurrence in 6 months), and no longer count it as an active item.
```

---

### Q5: After deployment, I found that the feedforward checklist is too long, affecting efficiency

The length of the feedforward checklist should be proportional to task complexity. If simple tasks also output long checklists, adjust with this method:

**Simplification instruction:**
```
Modify feedforward_startup: For simple tasks (such as translation, short Q&A), compress the feedforward checklist to one line—"Pitfall avoidance: xxx". Only complex tasks output the full startup checklist. Whether a task is simple is judged by you during execution and communicated to me.
```

You can also say "skip checklist and proceed directly" at the start of tasks, and the Agent should execute accordingly.

---

## 7.2 Common Questions During Operation

### Q6: The Agent made the same type of error twice which I didn't correct, but sinking wasn't triggered

**Direct check:**
```
Please output the current complete status of the score control table.
```

**Possible causes:**
- The Agent didn't correctly classify your first feedback (e.g., classified as type D occasional).
- The Agent classified the two feedbacks as different error patterns, not the same entry.

**Correction method:**
```
Unify [describe the two feedbacks] into the same error pattern: "[pattern name within 8 characters]". Please update the score table and check if the sinking threshold has been reached.
```

---

### Q7: The Agent always reports "all passed" in the delivery gate report, but I found problems

This indicates that the gate's check items are not detailed enough, or the Agent cut corners when executing the gate.

**Strengthening method:**
1. Point it out immediately when you discover a problem: `The third gate of delivery_gate didn't discover the cliché phrase "it's worth noting". Please explain the reason and update the gate's detection standard.`
2. If specific problems repeat, add targeted check rules to the gate:
```
In the check items of delivery_gate's third gate, add: "Does it contain vague qualifiers like 'to some extent', 'it can be said that'? Delete immediately if found."
```

---

### Q8: The output of the closed-loop review is too template-based, lacking truly valuable root cause analysis

This may be because the Agent hasn't encountered real problems for a long period, or the process setup causes the Agent to tend to "fill forms" rather than "think."

**Activation method:**
- Add specific direction during "takeoff": `Focus this review on [specific problem], please conduct deep root cause analysis.`
- If there are no problems for a long time, tell the Agent: `If this closed-loop review finds no issues requiring correction, it can be shortened to a 3-sentence briefing, no need for the complete nine steps.`

---

### Q9: I'm worried that the Agent's memory keeps growing and eventually exceeds limits

This is a problem already considered in the architectural design. Three built-in mechanisms control inflation:

1. **Hierarchical separation itself is an anti-inflation design**: The volume of principles and patterns is far less than operational steps and cases.
2. **L2/L3 entry limits**: L2 limit is 10 items, L3 limit is 3 items per scenario. When exceeded, a prompt for cleanup appears.
3. **Purification step in closed-loop review**: Check and migrate confusing content during each review.

If you are still concerned, you can manually clean up regularly:
```
List entries in memory that haven't been accessed in the last 30 days and evaluate whether they can be deleted.
```

---

## 7.3 Extended Thinking

### 7.3.1 From Single Agent to Multi-Agent Collaboration

The core of this architecture—four cybernetic concepts + hierarchical separation—is naturally applicable to multi-Agent scenarios.

**Extension ideas:**
- **Master Agent (orchestrator)**: Holds the L1 metacognitive framework, responsible for task distribution and quality control.
- **Sub-Agents (executors)**: Each holds L3 patterns for specific scenarios and corresponding Skills.
- **Shared memory area**: L2 user underlying logic is visible to all Agents, ensuring different roles follow unified aesthetics and principles.
- **Unified score table**: Negative feedback from all Agents converges to the same score table, with the Master Agent executing sinking decisions.

This essentially maps the "strategy/execution" boundary in "hierarchical separation" to the physical boundary of "Master Agent / Sub-Agents."

---

### 7.3.2 Introducing Other Theoretical Frameworks

This tutorial uses Qian Xuesen's Engineering Cybernetics as the underlying framework throughout. But L1 is not closed—your learning and transfer capability can continuously introduce new theories to the system through the "transfer proposal" step.

Extension attempts that have appeared in the comment section:

| Introduced Theory | Application Direction | Possible Corresponding L1 Extension |
| :----------------------- | :---------------------- | :----------------------------------- |
| Active Portfolio Management | Decision and Resource Allocation | Add "dynamic rebalancing" principle to L1 |
| Bayesian Inference | Judgment Under Uncertainty | Add "prior probability" correction to feedback weights in score control |
| Kelly Criterion + Shannon Information Theory | Information Value Evaluation | Add "information density" check to self-monitoring |
| TRIZ Invention Principles | Conflict Resolution | Add "physical contradiction vs technical contradiction" judgment to root cause analysis |

Method to introduce new theory: During "takeoff" review, when the Agent suggests a transfer, or when you have a clear idea, actively say:
```
I want to introduce [theory name] into L1, with the principle being [one-sentence description]. Please design how to add the 6th rule under the existing four-concept framework, and explain how it affects Skill operation.
```

---

### 7.3.3 Re-thinking the Applicability Boundary of the Framework

A question worth taking seriously appeared in the comment section: **"Engineering cybernetics may not be necessary for current Agents, or this is just adding steps to LLMs in context, not a strong constraint."**

After the complete expansion of this tutorial, the following answer can be given to this question:

1. **"Adding steps to LLMs" is itself an effective constraint**. LLMs are promptable systems, and structured context constraints can indeed change their behavior distribution. The effect doesn't come from hardcoded compulsion, but from continuous structured guidance.

2. **The value of architecture is not in single execution, but in long-term stability**. Looking at a single execution, you can get qualified results without giving the Agent any framework, relying only on ad-hoc commands. But after 50 consecutive tasks, a system with architecture converges better and drifts less. This is insurance, not fuel.

3. **Not all scenarios need it**. Light, one-time, highly random conversations don't need this architecture. Its applicability boundary is: **long-term collaboration × high precision requirement × task types with generalizable patterns**. If you happen to be in this area, the setup cost invested will be recovered in benefits from reduced repetitive error correction.

---

### 7.3.4 Framework Self-Termination Conditions

A healthy system should be able to identify "when I should be simplified."

**Termination or reduction signals:**
- No new items added to the score control table for 3 consecutive months (indicating collaboration has fully stabilized, or collaboration frequency has significantly dropped).
- No substantial findings in each "takeoff" review.
- You find yourself no longer needing the feedforward checklist in collaboration, and preferences are highly internalized.

When these signals appear, you can reduce the closed-loop frequency (e.g., from weekly to monthly), or simplify the architecture (e.g., remove the score table, keep feedforward and self-monitoring).

This is a system's self-humble design choice: **it doesn't pursue eternal existence, but effective operation when needed, and graceful reduction when not needed.**

---

## 7.5 Tutorial Review

| Chapter | Core Delivery | One-Sentence Key Point |
| :----- | :------------- | :----------------------------------------------- |
| Chapter 1 | Background & Philosophy | Not teaching AI new knowledge, but building architecture |
| Chapter 2 | Applicability & Preparation | First inventory your Agent and preferences |
| Chapter 3 | Four Cybernetic Concepts | Feedforward avoids pitfalls, score control prevents oscillation, hierarchical separation cures chaos, self-monitoring guards gates |
| Chapter 4 | System Architecture | Three-layer cognitive logic + mapping of physical storage and data flow |
| Chapter 5 | Practical Deployment | Six reproducible instruction steps, send directly to Agent |
| Chapter 6 | Daily Use & Verification | New collaboration rhythm + health checks + core metrics |
| Chapter 7 | FAQ & Extensions | Troubleshooting, extension, applicability boundary |

The essence of the entire tutorial can be summarized in one sentence: **What you're doing is not prompt engineering, but architecture engineering—you're not teaching the Agent new knowledge, but using systems engineering thinking to design a set of internal architecture that can run stably and evolve continuously.**

---

## 7.6 Final Step

The tutorial ends here. If you have completed deployment according to Chapter 5, you now only need to do three things:

1. **Use normally**—Send tasks normally, give feedback normally.
2. **Regular review**—Remember to say "takeoff."
3. **Adjust when necessary**—When encountering problems, look back at this chapter.

Your Hermes is no longer a tool that needs constant error correction, but a collaborative engine that understands you better over time and continuously aligns with principles. This is not science fiction, but landing 20th-century systems science thinking onto 21st-century AI Agent architecture.

**Very happy to have completed this seven-chapter journey with you.**