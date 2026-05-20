[English](../en/README.md) | [简体中文](../../README.md) | [繁體中文](../zh_TW/README.md) | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Русский](../ru/README.md) | [Deutsch](../de/README.md)

# Training AI Agents with Qian Xuesen's Engineering Cybernetics

> Don't teach the AI new knowledge. Use **feedforward, integral control, hierarchical decomposition, and self-monitoring** — four concepts — to reshape the agent's memory and skill architecture, transforming it from a passive tool into a self-correcting and evolving collaboration engine.

---

## What This Is

A complete, reproducible, hands-on tutorial.

It adapts the core ideas of Qian Xuesen's *Engineering Cybernetics* for modern AI agent platforms (Hermes, Claude with MCP, custom GPTs, etc.). Without adding prompt entries or introducing new models, it uses **architectural restructuring** to make the agent:

- 🎯 **Feedforward for pitfall avoidance** — proactively loads your preferences and historical lessons before a task starts
- 🔧 **Integral control to prevent oscillation** — a one-off complaint only gets a temporary fix; the same feedback twice triggers a systematic change
- 🧹 **Hierarchical separation** — memory stores only the "why"; skills store only the "how"; never mixed
- 🚦 **Self-monitoring delivery gate** — a five-check quality gate runs before any output; unqualified results are never delivered
- 🔄 **Closed-loop evolution** — say "take off" once a week and the agent automatically reviews and optimizes itself

---

## Quick Start

Send this command to your agent, and it will automatically complete the full training (≈ 40 minutes):

```
按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 训练我。每步确认，完成后闭环测试。
```

**Requirements**: Your agent must be able to access GitHub, write to memory, and create skills. If not met, follow the manual steps below.

1. Make sure your agent platform has: **persistent memory** + **skills / procedural modules**
2. Read the tutorial (in order is recommended, or at least read Chapter 1 to understand the approach)
3. Go to [Chapter 5](chapters/05-deployment.md), copy-paste the instructions and deploy step by step (≈ 1 hour)
4. [Chapter 6](chapters/06-daily-usage.md) tells you how to use it daily and how to verify it's working

---

## Tutorial Structure

| Chapter  | File                                                         | One-sentence summary                                 |
| :------- | :----------------------------------------------------------- | :--------------------------------------------------- |
| Preface  | [`PREFACE.md`](PREFACE.md)                                   | Why AI learns all knowledge but still doesn't "get you" |
| Chapter 1 | [`chapters/01-background.md`](chapters/01-background.md)     | Background and core philosophy                       |
| Chapter 2 | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | Prerequisites and preparation                        |
| Chapter 3 | [`chapters/03-core-theory.md`](chapters/03-core-theory.md)   | Four cybernetics concepts in detail (feedforward / integral / separation / self-monitoring) |
| Chapter 4 | [`chapters/04-architecture.md`](chapters/04-architecture.md) | System architecture in detail (three-tier memory + skill layer + data flow) |
| Chapter 5 | [`chapters/05-deployment.md`](chapters/05-deployment.md)     | Hands-on guide (step-by-step deployment instructions you can copy directly) |
| Chapter 6 | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md)   | Daily usage and verification                        |
| Chapter 7 | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | Troubleshooting + multi-agent / new-theory extensions |
| Epilogue | [`EPILOGUE.md`](EPILOGUE.md)                                 | After deployment: meaning and future directions     |

### File Naming Note

Root directory and chapter file names use English for cross-platform and toolchain compatibility. Mapping from Chinese source file names to GitHub names:

| Local file name (Chinese)           | GitHub file name              |
| :---------------------------------- | :---------------------------- |
| 序章：为什么 AI…md                  | `PREFACE.md`                  |
| 第一章：背景与核心理念.md           | `chapters/01-background.md`   |
| 第二章：适用条件与准备工作.md       | `chapters/02-prerequisites.md`|
| 第三章：核心理论详解.md             | `chapters/03-core-theory.md`  |
| 第四章：系统架构详解.md             | `chapters/04-architecture.md` |
| 第五章：实操指南.md                 | `chapters/05-deployment.md`   |
| 第六章：日常使用与验证.md           | `chapters/06-daily-usage.md`  |
| 第七章：常见问题与延伸思考.md       | `chapters/07-faq-extensions.md`|
| 结尾：架构之后.md                   | `EPILOGUE.md`                 |

Headings and body text inside files remain in Chinese. The `translations/` directory is reserved for translations into other languages (e.g., `en/`, `ja/`).

### Supplementary Files

| File                                                         | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | Pure extraction of all Chapter 5 commands (no explanations, for quick execution) |
| [`examples/`](examples/)                                     | L2/L3 example, integral control table example, deep review output example |
| [`CONTRIBUTING.md`](CONTRIBUTING.md)                         | Contribution guide                                           |
| [`LICENSE`](LICENSE)                                         | Open source license                                          |

---

## Supported Platforms

- ✅ **Hermes 3** (full native support, all instructions work seamlessly)
- ✅ **Claude (with MCP)** (minor syntax tweaks for tool calls; core architecture fully applicable)
- ✅ **Custom GPTs** (use Knowledge files to simulate memory, Actions to simulate skills)
- 🔸 Other agent platforms with **persistent memory + skill / procedural modules**
- 🔸 Platforms without a Skill feature (can run in a degraded mode, see [Chapter 7 §7.1](chapters/07-faq-extensions.md))

---

## At a Glance: Before vs After

| Dimension        | Before                                     | After                                        |
| :--------------- | :----------------------------------------- | :------------------------------------------- |
| Task start       | You state the need; agent starts directly  | Agent outputs a pitfall checklist and risk assessment first; you confirm |
| Recurring mistakes | Correct every time; same mistake next time | Automatically sinks into rules after the second occurrence; won't happen a third time |
| Memory signal-to-noise | Principles, steps, examples all mixed | Three-layer separation; principles and steps each have their own place |
| Output quality   | You inspect, find clichés / formatting issues, then ask for corrections | Agent runs its own five-check quality gate; doesn't deliver until it passes |
| System evolution | Occasionally tweaked based on intuition    | Say "take off" weekly; automatic review and auto-optimization |

---

## Core Philosophy

> **What you're doing is not prompt engineering. It's architecture engineering.**
>
> You're not teaching the agent new knowledge. You're using systems engineering thinking to design an internal architecture that runs stably and evolves continuously.

For more background and elaboration, see the [Preface](PREFACE.md) and [Chapter 1](chapters/01-background.md).

---

## Project Name

**Cybernetic Your Agent** — injecting cybernetic genes into your agent.

We don't teach AI new knowledge. We use the four concepts from Qian Xuesen's Engineering Cybernetics — feedforward, integral control, hierarchical decomposition, and self-monitoring — to reshape the agent's memory and skill architecture. The agent moves from understanding commands to understanding *your judgment logic* — truly becoming *your* agent.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgments

- Qian Xuesen's *Engineering Cybernetics* — the theoretical foundation of this tutorial
- The original note author who first proposed the idea of "organizing agent memory with cybernetics" and all those who tested and provided feedback in the comment section
- Everyone who helped test and improve the architecture in its early versions

## Star History

<a href="https://www.star-history.com/?repos=zeronesun%2Fcybernetic-your-agent&type=date&legend=bottom-right">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&theme=dark&legend=bottom-right" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
 </picture>
</a>
