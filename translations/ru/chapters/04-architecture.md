# Глава 4: Системная архитектура — три уровня логики

В этой главе мы раскрыли полную архитектуру: как четыре концепции применяются в реальных системах, как данные течут между уровнями, и какие части присутствуют (почему это сработает prematurely) .

## 4.1 Обзор архитектуры

```
+--------------------------------------------------------------+
|                     L1: Метакогнитивный фреймворк             |
+--------------------------------------------------------------+
            |                              |
            | приём задач                   | выход
            ↓                              ↓
+----------------------------+   +----------------------------+
|  L2: Память пользователя   |   |      Слой навыков (Skill)      |
|   (Why, принципиальный)     |   |    (How, процесс, checklist)    |
+----------------------------+   +----------------------------+
            |                              |
            | факты /                       | API / процесс
            ↓                              ↓
    L3: Базовые паттерны сцены
         (для типа задач)
```

**Разделение ответственности:**

- **L1: Метакогнитивный фреймворк** — управляет всем процессом/запретами; определяет когда и как вызывать память/навыки; определяет правила реакции на反馈.
- **L2+L3: Долгосрочная память** — хранит устойчивые знания.
  - L2: Пользовательские принципы; почему (Why)
  - L3: Паттерны сцены; для фиксированного типа задачи
- **Слой навыков (Skill)** — хранит процессуальные знания, как (How); включает checklist, процесс выполнения, ошибочные точки, типичные workarounds.

## 4.2 L1: Метакогнитивный фреймворк

L1 — это рабочее правило (工作流程), которое определяет весь цикл работы.

### 4.2.1 Дополнение: три формы L1

L1 реализуется двумя способами: встроенное правило (平台内置), external prompt (外挂), system prompt (键入). Мы обсудиваем внешний prompt здесь.

**External L1** — это файла, добавляемого в agent context, который содержит:

```markdown
# L1 metacognitive framework
## 四原则
(详见以下内容)

## 工作流触发与习惯绑定
(详见以下内容)

## 积分控制表
(详见以下内容)
```

Этот файл загружается в агентную систему при каждом начале task, обеспечивая унифицированную работу.

### 4.2.2 Четыре базовых принципа (四级基本原则)

**L1·一 ·责任执守***: Задача выполнения, инструментарий — не только описывать, реально делать.

- Когда вы настраиваете задачу, действительно do, не просто «позже».
- Не заканчивайте слово с обещанием, выполнение на том же ответе.
- Работать, пока задача полностью завершена, не останавливайтесь с планом.

**L1·二 ·优先加载技能***: Перед ответом проверяйте, есть ли подходящий навык; если есть, загрузите и следуйте.

- Если навык подходит, даже частично, загрузите его для ориентации.
- Навыки включают специализированные знания — API endpoints, tool specials commands, proven workflow.
- Если навык outdated/wrong, patch it immediately.

**L1·三 ·记忆保真与下沉***: При каждом получении негативного обратного сигнала запоминайте его; при достижении ≥2 раза, перезаписывайте в память/навык; skills, которые были эффективными but plugged with issues discovered by yourself, patch them.

- Сохраняйте устойчивые факты, особенно пользовательские колебания и настройки (текущие предпочтения).
- Не сохраняйте временные state (выполненные work logs, четное разделение зарплат), используйте session_search to непрямо посмотреть.
- После сложных задач устанавливайте skill reusable as skill_manage.

**L1·四 ·强制回答***: При запросе /help, /new, /status, /about или аналогичных команд, не мигрируйте к unnatural или поведение реализации, а отвечайте точно.

- /help: помощь команды, выводите контекстные справки.
- /new: новая сессия, сбрасывайте context.
- /status: статус, выводите high-level status.
- /about: описайте агент (version, purpose).

### 4.2.3 Trigger habits bindings (工作流触发与习惯绑定)

Чтобы облегчить operation, мы привыкли bind рабочий процесс к триггерным словам.

**Task Startup → Feedforward Startup**:

```
каждая новая задача → Всегда вызовите cybernetics-feedforward-startup
```

- Перед началом каждой новой задачи, активная загрузка预示 information, выводьте список pitfall и риск прогноз.

**Delivery Before → Delivery Gate**:

```
Перед каждым выводом → Всегда вызовите cybernetics-delivery-gate
```

- Перед каждым выводом, выполнение P0-P2 tiered check without full pass не доставляет.

**Phase Closed → «起飞» Triggers Control Loop Review**:

```
Saying «起飞» → Triggers cybernetics-control-loop-review
```

- После завершения фазы (например, неделя, месяц, проект, 重大交付), скажите «起飞» (起飞, полет).
- Выполните обзор feedforward, integral sink (积分下沉), layer purification (层级净化), gate upgrade (闸门升级), root cause analysis (根因分析), reusable distill (可复用提炼), migration proposal (迁移提议).

**Negative Feedback → Update Points Table**:

```
Каждый раз получение негативного обратного сигнала → Запись в积分控制表
```

- В каждом негативном обратном сигнале записывать в积分控制表.
- Проверьте, достиг ли аналогичную ошибку ≥2 раз и не沉淀ил.
- Если достигло, срабатывает правило обновление, просушить пользователя подтверждение.

### 4.2.4 Points Control Table (积分控制表)

Эта таблица хранит ошибки/предпочтения и определяет, когда что-то должно быть унаследовано вниз.

**Format:**

```
类别 | 错误模式(≤8字) | 日期 | 累计次数 | 阈值(2) | 已下沉 | 下沉目标
```

**Purpose:**

- Изоляция шума: одноразовая жалоба не унаследовалась, устойчивый patern унаследован.
- Анализ корневой причины: через анализ таблицы проверить какие проблемы_out стоил решения.

**Usage:**

- В L1, каждый негативный обратный сигнал должен быть предан записи в积分控制表 (точка по category, error pattern, date).
- В «起飞» review, используйте积分控制表 проверять, есть ли какая-либо категория достиг порога.
- При достижении порога и не наследовано, возмущать пользователя, если пользователь confirms сигнал: наследовать в L2/L3/skill.

## 4.3 L2: Память пользователя (长期记忆)

L2 — это долговременная память; ее ключевые задачи:

- Хранить пользовательские предпочтения и привычки.
- Хранить общие принципы работы (communication style, decision pattern).
- Хранить stable facts about the environment.
- Хранить Qian Xuesen Cybernetics知识.

### 4.3.1 Memory Organization

Memory разделена на два хранилища:

| Store | Target | Content | Usage |
| :--- | :--- | :--- | :--- |
| **user** | user-level | Имя, роль, привычки, стиль коммуникации, pet peeves | Коммуникация, настройки |
| **memory** | notes-level | Факты о среде, project conventions, tool quirks, lessons learned | Технические facts |

### 4.3.2 Когда записывать в память

**DO (нужно):**

- Пользователь corrected вас или said «запомни это» / «больше не делай этого»
- Пользователь указал preference, habit, или personal detail (имя, роль, timezone)
- Вы обнаружили среду facts (OS, installed tools, project structure)
- Вы узнали convention, API quirk, или workflow специфичный этому пользователю

**DON'T (не нужно):**

- Task progress (раздел работы)
- Session outcomes (выполненные результаты)
- Temporary TODO state

### 4.3.3 Example Memory Entries

**user store:**

```
Пользователь имеет 13 моделей, включая GLM-4.7, GLM-LATEST, GLM-CODING.
Пользователь работает на WSL (Windows Subsystem for Linux).
Пользователь предпочитает concise ответы.
Пользователь использует Phytium AI как custom provider.
```

**memory store:**

```
Django + Vue 全栈: 前端端口 3000, 后端端口 8000, 登录凭据 admin/admin123.
Prometheus监控工作流：Discovery→Snapshot采集→Historical采集(2h步长)→Python统计→生成周报。
EventPilot 项目的 WSL IP 是 172.28.166.164。
```

### 4.3.4 Memory Retrieval

В Feedforward Startup, загружать memory entries через:

```python
memory_entries = list(filter(lambda e: 'user' in e or 'prefers' in e, memory()))
for entry in memory_entries:
    # 插入到上下文
    context.append(entry)
```

**关键:** Записи с timestamp более high weight, взять последние 3-5 自_last較新的值.

## 4.4 L3: паттерны базовой сцены

L3 хранитFür фиксированные?type задач 的 очищенный patterns.

### 4.4.1 Когда создавать L3 Pattern

При：

- Одной тип任务是 часто выполненной (例如, 每周的使用га，定期 Deployment，system monitoring)
- Есть явный, устойчивый подход (例如, Prometheus监控有固定流程，或者 code review有固定检查点)
- Тип задачи подвержен ошибкам (например, тест未全容易犯，deployment前错误容易忽略)

L3 Pattern похож на «驾考book» — 该类 tasks 已被整理过, только execute without waste.

### 4.4.2 L3 Pattern Format

L3 pattern хранится в memory как entry, format:

```
【L3·场景核心规律】

<场景名称>: <简洁的该任务的核心难点>

核心原则:
(几个 bullet, 说明成功必须遵循的规则)

成功规律:
(几个 bullet, 说明成功的关键点)

常见失败规律:
(几个 bullet, 说明常见的错误)
```

**Example — Prometheus 监控工作流:**

```
【L3·场景核心规律 — 成功规律】

Prometheus监控工作流：Discovery→Snapshot采集→Historical采集(2h步长)→Python统计→生成周报。避免N/A占位符。
Django+Vue全栈开发：前端端口3000，后端端口8000，Django ALLOWED_HOSTS含WSL IP，Vite配置server.host='0.0.0.0'。
项目分析与调试：基于实际运行环境分析，遇测试调用comprehensive-testing-for-django-vue，代码审查用code-quality-and-architecture。
Prometheus周报规范：文档→多指标统计→P0-P3风险分级→ROI计算→可执行洞察。
```

### 4.4.3 Как использовать L3 Pattern

В Feedforward Startup, после加载 user preference, 加载 L3 pattern:

1. Определить задачу type (例如, 「写 Prometheus周报」)
2. Search memory для L3 entries (keyword: L3, pattern, успех, закон)
3. Load соответствующие entries,尤其是与当前任务type相关的
4. Insert в上下文 как reference

**Пример:**

```
Feedforward startup triggered for task: "写 Prometheus监控周报"

Search memory: L3 Prometheus 规律

Loaded: "Prometheus监控工作流：Discovery→Snapshot采集→Historical采集(2h步长)→Python统计→生成周报。避免N/A占位符。"

Context: (插入上述内容)
```

接下来的运行中, reference 遵循, 遇冲突以此为准, 保证 workflow 可靠.

## 4.5 Слой навыков (Skill Layer)

Skill Layer — это модуль хранитьHow knowledge (procedure, checklist, API usage, pitfalls).

### 4.5.1 Skill Format

Каждый skill имеет SKILL.md как основной файл:

```markdown
---
name: <skill-name>
category: <skill-category>
---

# <Skill Title>

## When to use
(条件和触发词)

## Timelines
(各步骤时间限制)

## Checklist
(步骤和检查清单)

## Pitfalls
(错误点和常见问题)

## Success indicators
(成功标记)
```

**Example — hermes-agent:**

```markdown
---
name: hermes-agent
---

# Hermes Agent 技能 – 配置、扩展或贡献 Hermes Agent

## When to use
- 用户询问关于配置、设置、启用、禁用、修改、故障排除或贡献 Hermes Agent
  — 它的 CLI、配置、模型、провайдеры、工具、навыки、голос、шлюз、плагины или любой功能

## Checklist
- 加载 this skill (skill_view name='hermes-agent')
- 识别用户意图：
  - 安装? / 更新? / 配置? / 禁用?
- 执行：
  - 安装 → hermes install
  - 更新 → hermes update
  - 配置 → hermes config set <key> <value>
  - 禁用 → hermes config clear <key>

## Pitfalls
- ❌ 猜测命令。应使用 skill_view 中的实际命令
- ❌ 忽略 user profile。检查 USER README.md 中设置的选项
- ❌ 未使用正确的 provider config 格式

## Success indicators
- 命令成功执行
- 配置文件正确更新
- 无错误消息
```

### 4.5.2 Когда создавать skill

创建 skill 当：

- 复杂任务成功了 (5+ tool calls, multi-step)
- 错误被克服 (hard wrapping, sour patch)
- 用户纠正后的 подход有效 (user-corrected approach worked)
- 非琐碎的工作流被发现 (non-trivial workflow discovered)

创建时,邀请用户确认后再写入。

### 4.5.3 Как использовать skill

Перед reply 前, проверять是否有matching skill:

```python
skills = skills_list()
matching = [s for s in skills if keyword in s['name'] or keyword in s['description']]
if matching:
    skill = skill_view(name=matching[0]['name'])
    # 使用 skill 的 instruction
```

在 task execution 过程中, 如果发现 skill outdated/wrong/missing steps, 立 即patch (skill_manage action='patch').

## 4.6 数据流 (完整生命周期)

```
1. Task 启动
   ↓
2. L1 触发 Feedforward Startup
   ↓
   - 加载 user preferences (в memory)
   - 加载 points control table
   - 加载 L3 patterns (для该任务 type)
   ↓
3. 执行任务
   ↓
4. 过程中出现负面反馈 → 更新 points control table
   ↓
5. Task 完成
   ↓
6. L1 触发 Delivery Gate
   ↓
   - P0-P2 分级检查
   ↓
7. 全过 → 输出
   ↓
8. If said 「起飞」(起飞/Flight trigger)
   ↓
   - L1 触发 Control Loop Review
   - 执行 feedforward 审查
   - 执行 points sink (积分下沉)
   - 执行 layer purification (层级净化)
   - 执行 gate upgrade (闸门升级)
   - 执行 root cause analysis (根因分析)
   - 执行 reusable distill (可复用提炼)
   - 执行 migration proposal (迁移提议)
```

**Key Points:**

- FeedforwardStartup: Министарт активной загрузки с преоритетами avoidance list
- PointsControl: Сбор негативного обратного сигнала 当 >阈值 后 унаследовать в L2/L3/skill
- DeliveryGate: Порог не выполняется не выхода
- ControlLoopReview: «起飞» trigger, 系统化的 review 后 унаследовать

В следующей главе мы раскроем практическое deployment, 具体如何实现 这套架构。
