# Chapter 2: Applicable Conditions and Preparations

## 2.1 Minimum Requirements for Agent Platforms

Before you begin, confirm whether the Agent platform you're using possesses the following capabilities. These are the physical foundations for implementing this architecture.

### 2.1.1 Essential Capabilities (Missing Any One Prevents Complete Implementation)

| Capability | Description | Purpose |
| :--- | :--- | :--- |
| **Persistent Memory** | Memory systems that can store, read, and update across sessions | Hosts L1 metacognitive framework, L2 user logic, L3 scenario patterns, point control tables |
| **Procedural Modules** | Ability to create, call, and update skills/Skills/GPTs, etc. | Hosts execution layer (delivery gates, feedforward initiation, closed-loop organization, etc.) |
| **Sufficient Context Window** | Recommended 100k tokens or more | Accommodates feedforward lists within sessions, pitfall records, task execution processes |

If your platform possesses all three of the above capabilities, you can fully implement all content in this tutorial.

### 2.1.2 Bonus Capabilities (Stronger With Them, Can Operate at Reduced Level Without Them)

| Capability | Description | Alternative When Missing |
| :--- | :--- | :--- |
| **Session Retrieval** | Search content and correction records in historical sessions | Manually write key lessons into memory after each correction, as feedforward material |
| **Tool Calling** | Agent can actively call external tools (search, code execution, etc.) | Scope is limited but core architecture is unaffected |

### 2.1.3 What If Your Platform Lacks Skill Functionality

Some platforms (such as basic ChatGPT, simple chat interfaces) don't have skill modules. In this case, you can adopt the **"Memory Simulation Method"**:

- Store Skill content as structured memory entries, such as `[Skill-Delivery Gate] Content: ...`
- Add mandatory rules in the L1 metacognitive framework: "Before each delivery, must read and execute all memory entries marked [Skill-*]"
- Disadvantage: consumes memory capacity and requires Agent to actively retrieve; advantage: logic is fully preserved, suitable for light usage scenarios.

## 2.2 Self-Assessment: Are You Suitable for Using This Tutorial?

### 2.2.1 Strongly Recommended User Profiles

- **High-Precision Collaboration Users**: You have stable quality requirements for Agent outputs (such as writing style, code standards)
- **Repetitive Task Users**: You frequently perform similar tasks with Agents (such as daily/weekly similar workflows)
- **Systems Thinking Users**: You're willing to invest upfront setup costs in exchange for long-term collaboration efficiency
- **Clear-Boundary Users**: You can clearly express preferences and red lines, and are willing to point them out when Agents make mistakes

### 2.2.2 Less Suitable Users

- Only performing one-time, non-reusable random Q&A
- Use cases span very widely, making it difficult to abstract stable patterns
- Do not wish to establish long-term collaboration relationships with Agents

## 2.3 Preparation Work Before Starting

Before formal deployment, complete the following four preparations, which can significantly reduce subsequent adjustment costs.

### 2.3.1 Take Stock of Current Agent Status

Run the following two commands and record the current status as a baseline:

```
List all the skills you currently have, along with summaries of their content.
```

```
List all content currently stored in your memory and evaluate usage rate.
```

**Key Recording Points**:
- How many skills are currently there? Are they still in use?
- What percentage of memory is being used? Is the content already mixed/confused?
- Is there a large amount of outdated information?

### 2.3.2 List Preferences and Rules You Want to Solidify

Use a simple table to list the principles you want the Agent to follow long-term. This step helps you extract actionable rules from vague "feelings":

| Dimension | Your Principles | Example |
| :--- | :--- | :--- |
| Communication Style | Concise and direct, no pleasantries | Don't output "hope this helps you" |
| Output Format | Code first, with verification methods | Include test steps when outputting solutions |
| Decision Preference | Risks first, expose problems upfront | List risks before discussing benefits |
| Aesthetic Preference | Cool narrative, reject AI summarization | Leave endings of novels open, don't elevate |

You don't need to exhaust everything once, 4-6 core principles are sufficient. The Agent will help you continuously supplement them in the closed loop later.

### 2.3.3 Recall 3-5 Task Types You Frequently Execute

- For example: short story writing / code review / operations troubleshooting / architecture design / data analysis
- For each type, try writing one sentence describing what you consider the key pattern for "doing it right" for this type of task

**Examples**:
- Short story creation: "Emotional tone setting takes priority over plot unfolding, endings must be left open."
- Code review: "First look for architectural problems, then check naming conventions; for each type of problem found, provide modification suggestions."
- Problem troubleshooting: "First check logs to locate root causes, don't wait and guess; when uncertain, mark as 'pending verification'."

These will directly become the initial content of your L3 scenario patterns.

### 2.3.4 Backup Current Status

Before starting deployment, **backup your current memory and skills status**. Specific methods depend on your platform:

- If the platform supports export, export a copy first
- If not supported, manually copy current memory and skill lists to a local document
- If there's version management (such as memory snapshots on some platforms), create a restore point

The purpose of this step is: in case disorder occurs during deployment, you can restore to the initial state and start over.

## 2.4 Completion Indicators for Preparation Phase

When you can answer the following three questions, the preparation phase is complete and you can enter Chapter 3:

1. Does my Agent platform possess persistent memory + skill modules? (Yes / No / Partially)
2. How many core preferences and principles have I identified? (Recommended ≥4)
3. How many high-frequency task types have I listed, and for each type do I have preliminary "pattern judgments"? (Recommended ≥3)
