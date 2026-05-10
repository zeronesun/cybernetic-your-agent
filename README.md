# 用钱学森工程控制论训练 AI Agent

> 不教 AI 新知识。用**前馈、积分控制、层级分离、自监控**四个概念，重塑 Agent 的记忆与技能架构，使其从"被动工具"进化为"能自我纠偏和进化的协作引擎"。

---

## 这是什么

一套完整、可复制的实操教程。

将钱学森《工程控制论》的核心思想适配到现代 AI Agent 平台（Hermes、Claude with MCP、自定义 GPTs 等）。不增加 prompt 条目，不引入新模型，而是**通过架构重组**让 Agent 实现：

- 🎯 **前馈避坑** — 任务启动前主动加载你的偏好和历史教训
- 🔧 **积分防震荡** — 吐槽一次只临时修正，两次才系统性地改
- 🧹 **层级分离** — 记忆只存"为什么"，技能只存"怎么做"，永不混淆
- 🚦 **交付自检** — 输出前自动过五关闸门，不合格不交付
- 🔄 **闭环进化** — 每周说一句"起飞"，Agent 自动复盘并优化自身

---

## 快速开始

1. 确认你的 Agent 平台具备：**持久化记忆** + **技能/程序性模块**
2. 阅读教程（建议按顺序，或至少先读第一章确认思路）
3. 进入[第五章](chapters/05-deployment.md)，复制粘贴指令按步骤部署（约 1 小时）
4. [第六章](chapters/06-daily-usage.md)告诉你日常怎么用、怎么验证

---

## 教程结构

| 章节   | 文件                                                         | 一句话内容                                   |
| :----- | :----------------------------------------------------------- | :------------------------------------------- |
| 序章   | [`PREFACE.md`](PREFACE.md)                                   | 为什么 AI 学会所有知识，却学不会"懂你"       |
| 第一章 | [`chapters/01-background.md`](chapters/01-background.md)     | 背景与核心理念                               |
| 第二章 | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | 适用条件与准备工作                           |
| 第三章 | [`chapters/03-core-theory.md`](chapters/03-core-theory.md)   | 四个控制论概念详解（前馈/积分/分离/自监控）  |
| 第四章 | [`chapters/04-architecture.md`](chapters/04-architecture.md) | 系统架构详解（三层记忆体 + 技能层 + 数据流） |
| 第五章 | [`chapters/05-deployment.md`](chapters/05-deployment.md)     | 实操指南（分步骤部署指令，可直接复制）       |
| 第六章 | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md)   | 日常使用与验证方法                           |
| 第七章 | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | 常见问题排障 + 多 Agent / 新理论延伸         |
| 结尾   | [`EPILOGUE.md`](EPILOGUE.md)                                 | 部署之后：架构的意义与后续方向               |

### 文件命名说明

本仓库根目录和章节文件名使用英文，以兼容跨平台和工具链。中文源文件重命名对照：

| 本地文件名（中文）            | GitHub 文件名                   |
| :---------------------------- | :------------------------------ |
| 序章：为什么 AI…md            | `PREFACE.md`                    |
| 第一章：背景与核心理念.md     | `chapters/01-background.md`     |
| 第二章：适用条件与准备工作.md | `chapters/02-prerequisites.md`  |
| 第三章：核心理论详解.md       | `chapters/03-core-theory.md`    |
| 第四章：系统架构详解.md       | `chapters/04-architecture.md`   |
| 第五章：实操指南.md           | `chapters/05-deployment.md`     |
| 第六章：日常使用与验证.md     | `chapters/06-daily-usage.md`    |
| 第七章：常见问题与延伸思考.md | `chapters/07-faq-extensions.md` |
| 结尾：架构之后.md             | `EPILOGUE.md`                   |

文件内部标题和正文保持中文不变。`translations/` 目录预留给其他语言译本（如 `en/`、`ja/` 等）。

### 辅助文件

| 文件                                                         | 说明                                             |
| :----------------------------------------------------------- | :----------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | 第五章全部指令的纯提取版（无解释，方便快速执行） |
| [`examples/`](examples/)                                     | L2/L3 示例、积分控制表示例、闭环梳理输出示例     |
| [`CONTRIBUTING.md`](CONTRIBUTING.md)                         | 贡献指南                                         |
| [`LICENSE`](LICENSE)                                         | 开源协议                                         |

---

## 适用平台

- ✅ **Hermes 3**（完全原生支持，所有指令无缝运行）
- ✅ **Claude（with MCP）**（需微调工具调用语法，核心架构完全适用）
- ✅ **自定义 GPTs**（用 Knowledge 文件模拟记忆，用 Actions 模拟技能）
- 🔸 其他具备**持久化记忆 + 技能/程序性模块**的 Agent 平台
- 🔸 无 Skill 功能的平台（可降阶运行，见[第七章 7.1 节](chapters/07-faq-extensions.md)）

---

## 效果速览

部署前后对比：

| 维度       | 部署前                        | 部署后                                   |
| :--------- | :---------------------------- | :--------------------------------------- |
| 任务启动   | 你说需求，Agent 直接做        | Agent 先输出避坑清单和风险预判，你再确认 |
| 同类错误   | 每次纠正，下次照犯            | 第二次出现时自动下沉为规则，第三次不再犯 |
| 记忆信噪比 | 原则、步骤、案例混在一起      | 三层分离，原则和步骤各有归属             |
| 交付质量   | 你检查，发现套话/格式问题再改 | Agent 自己过五关闸门，不合格不交付       |
| 系统进化   | 凭你感觉偶尔调一下            | 每周说"起飞"，自动复盘、自动优化         |

---

## 核心理念

> **你做的不是一次 prompt engineering，而是一次 architecture engineering。**
>
> 你不是在教 Agent 什么新的知识，而是在用系统工程的思维，为它设计一套能稳定运行、持续进化的内部架构。

更多背景和理念阐述，见[序章](PREFACE.md)和[第一章](chapters/01-background.md)。

---

## 项目名称

**Cybernetic Your Agent** — 为你的 Agent 注入控制论基因。

我们不教 AI 新知识，我们用钱学森工程控制论的前馈、积分控制、层级分离、自监控四个概念，重塑 Agent 的记忆与技能架构。让 Agent 从听懂指令，进化到懂你的判断逻辑——真正成为*你的* Agent。

---

## 许可证

本项目采用 [MIT License](LICENSE)。

---

## 致谢

- 钱学森《工程控制论》— 本教程的理论根基
- 最初提出"用控制论组织 Agent 记忆体"思路的笔记作者及评论区所有实测反馈者
- 所有在早期版本中帮助测试和改进架构的协作者