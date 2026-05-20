# Глава 7: Часто задаваемые вопросы и расширенное применение

Эта глава освещает распространенные вопросы при развертывании, а также показывает, как расширить этот фреймворк до multi-agent и multi-role сценариев.

---

## 7.1 Часто задаваемые вопросы во время развертывания

### Q1: Моя платформа не поддерживает настройку system prompt. Есть ли способ внедрить этот фреймворк?

**A:** Есть два режиме:

1. **Режим "симуляции памяти" (Memory Simulation Mode)**
   - Хранить содержимое L1 rules как обычные записи памяти с типом "L1-metacognitive-framework"
   - Передать platform's memory reading mechanism:
     ```
     При начале задачи: Автоматически read все записи памяти типа "L1-*", insert в контекст.
     При выводе: Автоматически read 所有事项 в图中.
     ```
   - Недостаток: Consumes много token; преимущество: Полной реализации без изменения system prompt.

2. **Внешний prompt загрузки (External Skill Loading)**
   - Если ваша платформа на базе API поддерживает loading custom prompts (напр., через `system`, `custom_prompts`, `skill_load` и т.п. endpoints), загрузить L1 rules как внешний skill.
   - Этот метод быстра и чист, но требует, чтобы platform поддерживал такой интерфейс.

### Q2: Feedforward Startup загружал слишком много информации (例如, 记忆很长的历史随便). 怎么优化?

**A:** Есть три стратегии:

1. **Фильтрация по ключевым словам**
   - 只 SEARCH `prefers`, `喜欢`, `likes`, `values`, `不喜`, `dislikes` 这些词
   - 避免加载所有记录, 只命中更 relevant 部分

2. **Ограничение количества результатов (Limit the result count)**
   - 只取最新的 3-5 条
   - по timestamp descending, 保证只看最近的

3. **Кэширование (Caching)**
   - 如果平台支持 caching, 缓存最近的查询结果下一次直接复用

### Q3: 积分控制表 由谁来维护? 用户还是 Agent 自动?

**A:** Бесконтрольно смешаны:

- **Agent автоматическая maintenance**: 每次收到负面反馈时, 自动更新积分控制表 (добавить entry 或 count+1)
- **User вмешательство**: 只在用户明确confirm时才执行沉淀 (например, Agent спрашивает: 「是否沉淀?」)
  - 避免了一次偶然抱怨就被误判为偏好
  - 保证了沉淀的内容真的是用户认可的

### Q4: Delivery Gate 总是输出 "All passed"，但实际上我看到了错误输出。 Why?

**A:** 有三种可能:

1. **检查项不足**
   - 错误类型不在检查项内 (例如, 你不希望文件 content 为 0，但 gate 没检查)
   - **对策**: 扩展 delivery gate 的检查项 (например, 添加新的 P1 或 P2 检查)

2. **检查逻辑错误**
   - 检查项写错了 (例如, check `if file exists` 但未 check `file content`)
   - **对策**: read testing scripts 对比实际的 failing case，修正检查逻辑

3. **P0/P1 fail 但不影响 logic**
   - 有时 P0/P1 被 critical error detected (语法错误) 被重新运行后 cowboy 无问题
   - 但 gate 可能输出的 "all passed" 因修改后不再错误
   - **对策**: 正常情况, 说明 gate 捕获到问题并 allowing agent fix

### Q5: 某个模式已经下沉到 L2，但用户又再次反馈不同意见。 What to do?

**A:** Accept 用户输出，update L2 entry:

- L2 正值是由from multiple Feedbacks 构成的 tolerant range
- 不要删除 or 改写整条 L2，而应 adjust with more nuance
- Example: 如果既有「喜欢详细解释」, 又有新 feedback「太详细了，简洁一点」，则 update:
  ```
  [L2·沟通细节度] 用户偏好：在需要深入讲解时详细解释。在日常操作中讲究简洁直接。避免长 preamble 或空泛铺垫。
  ```

---

## 7.2 Расширенное сценарий: Multi-Agent система

如果你有多个 AI Agents (例如，一个负责 DevOps，一个负责代码开发，一个负责写报告)，这套架构可以扩展为:

### 7.2.1 Шаринг L3 和 Skills

- **L3 (паттерны сцены)**: Каждый agent access к общим L3 patterns
  - Example: 所有 agents 都遵循「前置检查 pwd+ls+项目识别」 pattern
  - Example: 所有 agents 都遵循「测试前调用 skill 进行 systematize testing」 pattern
  - **好处**: 避免 duplicate learning，统一 workflow 执行标准

- **Skills (процедурные знания)**: Skils общие для всех agents (例如, 「测试工作流」、「文件操作规范」)
  - 也可以 agent-specific (например，「DevOps 相关 skill」，「开发相关 skill」)
  - **好处**: 可复用，且当一个 agent 发现新的 workflow 后可 share 给其他 agents

### 7.2.2 Per-Agent L2 (用户底层逻辑)

每个 agent 有独立的 L2，针对性 their role-specific preferences:

- **DevOps Agent L2**:
  ```
  L2·任务执行：所有 terminal 命令不超过5秒，超过必须设置 timeout。
  L2·监控：任何监控指标变化超过10%立即预警。
  输出格式：只输出数值，不输出解释。
  ```

- **Development Agent L2**:
  ```
  L2·代码组织：所有新 feature 必须有对应的 test。
  L2·协作：和 Mentors、Senior 配合时，主动汇报计划。
  L2·安全：永远不将 API key 写在 public repos。
  ```

- **Writing Agent L2**:
  ```
  L2·写作风格：保持专业且简洁，避免夸张措辞。
  L2·重复检查：生成后必须检查是否有重复的句子。
  L2·Audience：优先为技术开发人员服务。
  ```

每个 agent 的 L2 将 load 该 agent's 记忆 store (在 platform's multi-agent 架构中通常会由 `user_level: agent_id` 处理)。即使这些 L2 存在 overlapped content (例如，所有 agents 都偏好简洁)，但由于各自的 agent_id，不会冲突。

### 7.2.3 Периодический「起飞」 для Multi-Agent Review

在一周的「起飞」中，每个 agent 可以 trigger 自己的 review：

```
DevOps Agent → trigger control loop review →沉淀 DevOps-specific 知识
Development Agent → trigger control loop review →沉淀 Dev-specific 知识
Writing Agent → trigger control loop review →沉淀 Writing-specific 知识
```

随后，可以 execute 一个 **Global Review**：

```
1. Пересобрать所有 agents 的 L3 共通模式
2. Пересобрать所有 agents 的 general skills
3. 检查是否有跨 agents 的不一致配置 (例如，一个 agent 偏好详细输出，另一个偏好简洁)
4. Выполнить Alignment:
   - 对于不一致的地方，由用户identify哪个是正确的
   - Update 所有 agents 的相关配置
```

По сути，这 thành了一名 「Team Orchestrator» (团队协调员) 角色，协调多个 agents share 与 align。

### 7.2.4 Inter-Agent 协作

当多个 agents 协作完成一个任务时，需要注意：

- 每个 agent 需要知道全局的计划
- 每个 agent 需要知道 сегмент-specific constraints
- 每个 agent 开始前 trigger feedforward loading её relevant L2/L3

**示例 workflow:**

```
User: 「部署新的 Django 后端到Production。」

→ Orchestration agent (Team Orchestrator) создал план:
   1. DevOps Agent: 配置 infrastructure
   2. Dev Agent: ревизор deployment script
   3. DevOps Agent: 执行 deployment
   4. All Agents:验证 в Production

→ DevOps Agent 开始:
   - Feedforward: load DevOps L2, load L3「standard deployment workflow」
   - 执行
   - Delivery gate passes

→ Dev Agent 开始:
   - Feedforward: load Dev L2, load L3「code review - PRI-P3 checks」
   - 执行
   - Delivery gate passes

→ DevOps Agent 开始:
   - Feedforward: load DevOps L2, load L3「production deployment checklist」
   - 执行
   - Delivery gate passes
```

---

## 7.3 Расширенное сценарий: Multi-Role система

有时候一个 agent 承担多个角色 (例如，有时候做 developer，有时候做 writer，有时候做 devops)。对于这样的 multi-role agent，架构扩展为:

### 7.3.1 Role-Aware L2

不使用单一的 L2 store，而使用 per-role L2 stores:

```
L2_dev:
  - Dev偏好 и принцип (例如，“必须写 test”)

L2_writer:
  - Writer偏好 и принцип (例如，“保持简洁”)

L2_devops:
  - DevOps偏好 и принцип (例如，“只输出数值”)
```

### 7.3.2 Role Detection в Feedforward

在 feedforward startup，添加步骤:

```
1. Detect 当前 role (на базе задачи类型 perhaps)
   - 例如，「写报告」 → Role = writer
   - 例如，「部署服务» → Role = devops
   - 例如，「开发功能» → Role = dev

2. Load 该 role 的 L2
3. Load 通用 L2
4. Load 通用 L3 和 Skills
```

### 7.3.3 Per-Role Delivery Gate Checks

Delivery gate 也可以根据 role 有不同检查项:

```
Role = writer:
  P2: [检查重复句子] 检查是否有重复句子超过3次
  P2: [检查夸张措辞] 检查是否有夸张或 sensational words

Role = dev:
  P1: [测试覆盖] 检查是否写至少一个 test
  P1: [API key 安全] 检查是否将 старый API key 写入新文件

Role = devops:
  P1: [超时保护] 检查所有 terminal 命令是否设置了 timeout
  P2: [监控预警] 检查是否有监控检查用于新的 metric
```

这使得一个 agent 同时 sophisticatedly play 多个角色，每个角色有自己不同 «flavor»。

---

## 7.4 Расширенное сценарий: Collaboration 外界 Systems

在这个架构可以和其他外部系统集成，建立更强大的 knowledge pipeline:

### 7.4.1 Интеграция с External Experimental Systems

例如，你有一个「实验机」 (例如，A/B testing env)，可以定期 feed 数据 в积分控制表作为自动 feedback:

```
实验机结果:
  - Experiment A: click-through rate 提升 5%
  - Experiment B: conversion rate 降低 3%

→ Автоматически写 в **积分控制表**:
  Performance | 实验A提升 | <date> | 1 | 2 | 否 | skill: performance-testing

→ 下次当执行类似实验 (例如，「Run experiment for optimizing CTR») 时，feedforward 会加载:
  - L3: 「实验机工作流：启动 → 收集数据 → 分析 → 下报」
  -_POINTS: 如果类似 pattern 之前被沉淀为 skill，会自动 load 该 skill

→ Offloading 手 knowledge 至「实验机驱动 role upgrading»
```

### 7.4.2 Интеграция с Issue Trackers

如果你在 GitHub или类似平台使用 issue tracker (例如，「bug 甄别工具»)，当 bug 被标记为「正確」(verified)，可以自动化 trigger「积分控制表» ::督:

```
GitHub action:
  - Bug #123 被标记为 confirmed (исправный bug)

→ Автоматически写 в **积分控制表**:
  Bug | #123 confirmed | <date> | 1 | 2 | 否 | L2 bug-prevention

→ 之后当出现类似 bug pattern，feedforward 会加载预警规则
```

这有助于「bug prevention» workflow (bug engineering)。

---

## 7.5 测试 граничные情况

### Сценарий A: 第一次系统全部空白

**Тест**:

1. 创建全新环境 (no prior records)
2. 启动 feedforward startup:
   - Should 输出: 「 Нет записей пользователя, 请提供偏好信息。」
3. 执行任务，交付 gate 应 pass
4. 给负面反馈:
   - Should 自动创建 записей в积分控制表
5. 再次给负面反馈 (相同类别):
   - Should 触发沉淀
   - Should 创建/更新记忆或技能

**期望**:
- 第一次无记录时，feedforward 应优雅降级，不崩溃
- 积分控制首次反馈机制正常工作
- 沉淀机制在第二次反馈时正常触发

### Сценарий B: 沉淀后有冲突的新 feedback

**Тест**:

1. 已沉淀规则：「用户偏好简洁表达」
2. 用户反馈：「太简洁了，详细点」
3.期望动作**:
   - Agent 应识别冲突 (contradiction)
   - Agent 应 update L2 entry 更加 nuanced
   - 不应直接 rewrite existing L2 (删除重要历史)

**期望结果**:
```
Updated L2:
[L2·沟通细节度] 用户偏好：在需要深入讲解时详细解释。在日常操作中讲究简洁直接。避免长 preamble 或空泛铺垫。
```

### Сценарий C: 抵达积分阈值但不沉淀

**Тест**:

1. 已达到阈值 count=2 (例如，「太啰嗦» 已 2 次)
2. 但沉淀机制fail (из-за bug, incorrect skill name, memory API error)
3.Треть раз反馈同样问题**
4.期望动作**:
   - 系统应检测 count >= 2 и не sunk
   - 应提示用户 (report issue)
   - 应尝试补救 (re-trigger沉淀 endpoints)

**期望**:
- 积分控制不应无限增长而不沉淀
- 不会导致系统 performance degrade

---

## 7.6 Измерение и проект RX (ROI)  системы

### 7.6.1 量化指标 (Quantitative Metrics)

| Метрика | Метод *Measure** | What говорит |
| :--- | :--- | :--- |
| **Коэффициент повторных ошибок** | (Повторных ошибок) / (общее число ошибок) | Снижение表明系统 在沉淀/预防 error 上有效 |
| **Коэффициент feedthrough hit** | (feedthrough predictions 正确) / (feedthrough всего predictions) | >50%表明 feedthrough system 良好 aligning с user preferences |
| **Delivery gate P0/P1 阻拦率** | (P0/P1 阻拦并修复) / (输出尝试次数) | Изначально高，长期降低表明 upstream (feedthrough/score control) 良好 |
| **积分沉淀转化率** | (превратившись в записей沉淀) / (достигших ≥2 threshold 的记录) | Сходить 100%表明 автоматический沉淀机制 工作无缝 |

### 7.6.2 ROI (Возвращение инвестиции)

虽然难以直接量化 ROI (это关于 эффективности кибернетического engineering)，但可以 inspect:

**唔 前**:
- 用户每一类问题需要 3-5 次 correction 才形成 stable pattern
- Agent不记住用户的 preferences
- 每次新任务都需要重复c remind同样的事情

**唔 后**:
- 每一类问题 2 次反馈后自动沉淀，不再重复
- Preferences сохранены и loaded автоматически
- New tasks автоматически avoid historical pitfalls

**时间节约**:
- 假设平均每天有 10 次需要 correction 的问题，每次 correction 需要 2 分钟
- 淀淀后，从第 3 次 开始该类问题自动预防
- 假设每类问题平均出现 8 次/周，之前每次需要 correction (8 * 2 = 16 min/周)，之后只在第1、2次需要 correction (2 * 2 = 4 min/周)，节约 12 分钟/周 ≈ 1 小时/月 ≈ 12 小时/年

**Acquisition cost**:
- 初始部署：约 2-4 小时 (根据平台复杂度)
- 维护：每周 2 分钟审查«起飞» review

**ROI ratio**:
- 第一年：12 hours saved / 4 hours cost ≈ 3x ROI
- 第二年及之后：12 hours / ~0.5 hours ≈ 24x ROI

---

## 7.7 Заключение

Моя цель этой системы — не «useless control layer», 而是:

1. **Избежать repeat same corrections** (從「你要править我» 转向 「Яself-learn»)
2. **Помочь вам 追踪 ваш workflow** (от чаевой oversight к прослеживаемойpatterns)
3. **Для multi-agent/multi-role:** координированно тамне schedsame workflow, align各异 preferences

Это — инженерное кибернетическое приложение к AI Agent system，但最终很简单 — **它只是让你少说几次「我跟你讲了……是这样的」**。

Если в развертывании惊讶 что有 путь不清晰的地方，说「takeoff」，我們可以一起沉淀到知识庫中。

---

**Следующие шаги:**

1. **Развернуть свой агент с этим фреймворком** (Chapter 5)
2. **使用 одну неделю** следуя Chapter 6 guiding
3. Если works для你， extension к multi-agent / multi-role (本章 7.2/7.3)
4. Регулярно «takeoff» → система разработается с你的偏好 evolve
