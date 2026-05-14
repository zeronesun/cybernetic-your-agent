# 快速部署：一句话让 Agent 完成控制论架构训练

用一句话命令，让 Agent 自动读取教程并完成整套控制论架构的训练。

---

## 适用条件

你的 Agent 必须能够：
- 访问 GitHub 公开仓库
- 写入记忆（`memory` 功能）
- 创建技能（`skill` 或类似程序性模块）

如果不满足，请跳至 [手动训练](#手动训练)。

---

## 一句话指令（复制发给 Agent）

```
按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 训练我。每步确认，完成后闭环测试。
```

> Agent 将自动读取全部指令，依次写入 L1 元认知框架、初始化 L2/L3、建立积分控制表、创建四个核心技能，并在最后执行一次闭环测试。

---

## 训练过程（你只需确认）

1. Agent 读取部署指令文件
2. 写入 L1 元认知框架
3. 初始化 L2 和 L3（Agent 向你确认提炼结果）
4. 建立积分控制表
5. 创建四个技能：`delivery_gate`、`feedforward_startup`、`control_loop_review`、`user_profile_maintainer`
6. 运行首次闭环测试（说“起飞”）

全程约 40 分钟，你只需在关键步骤确认。

---

## 手动训练

如果 Agent 无法访问 GitHub，请先复制下方内容发给它：

> 我将发送一份训练指令列表，请逐条执行。每完成一步告知我。

然后打开 👉 [scripts/deployment-commands.md](scripts/deployment-commands.md)，将内容分段复制给 Agent。

---

## 训练完成标志

Agent 应显示：

- ✅ 四个核心技能已创建
- ✅ 积分控制表已就绪
- ✅ 首次闭环测试通过

此时你的 Agent 已转变为以控制论为骨架、能自我进化的协作引擎。

---

## 日常使用小抄

- 建新任务 → Agent 自动输出避坑清单，你说“直接做”即开始
- 出错了 → 同类问题第二次出现时，Agent 自动下沉为规则
- 复盘 → 说 **“起飞”**，Agent 执行完整九步复盘并自我优化

---

## 项目链接

- 完整教程：[chapters/](chapters/)
- 中文源文件对照：[文件命名说明](README.md#文件命名说明)
- 贡献或问题反馈：[CONTRIBUTING.md](CONTRIBUTING.md)
