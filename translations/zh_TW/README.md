[English](../en/README.md) | [简体中文](../../README.md) | 繁體中文 | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Русский](../ru/README.md) | [Deutsch](../de/README.md)

# 用錢學森工程控制論訓練 AI Agent

> 不教 AI 新知識。用**前饋、積分控制、層級分離、自監控**四個概念，重塑 Agent 的記憶與技能架構，使其從「被動工具」進化為「能自我糾偏和進化的協作引擎」。

---

## 這是什麼

一套完整、可複製的實操教學。

將錢學森《工程控制論》的核心思想適配到現代 AI Agent 平台（Hermes、Claude with MCP、自訂 GPTs 等）。不增加 prompt 條目，不引入新模型，而是**透過架構重組**讓 Agent 實現：

- 🎯 **前饋避坑** — 任務啟動前主動載入你的偏好和歷史教訓
- 🔧 **積分防震盪** — 吐槽一次只做臨時修正，兩次才系統性地改
- 🧹 **層級分離** — 記憶只存「為什麼」，技能只存「怎麼做」，永不混淆
- 🚦 **交付自檢** — 輸出前自動過五關閘門，不合格不交付
- 🔄 **閉環進化** — 每週說一句「起飛」，Agent 自動覆盤並優化自身

---

## 快速開始

把這句話發給你的 Agent，它會自動完成整套訓練（約 40 分鐘）：

```
按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 訓練我。每步確認，完成後閉環測試。
```

**適用條件**：Agent 需能訪問 GitHub、寫入記憶、創建技能。如果不滿足，請按下方手動步驟操作。

1. 確認你的 Agent 平台具備：**持久化記憶** + **技能／程序性模組**
2. 閱讀教學（建議按順序，或至少先讀第一章確認思路）
3. 進入[第五章](chapters/05-deployment.md)，複製貼上指令按步驟部署（約 1 小時）
4. [第六章](chapters/06-daily-usage.md)告訴你日常怎麼用、怎麼驗證

---

## 教學結構

| 章節   | 檔案                                                         | 一句話內容                                        |
| :----- | :----------------------------------------------------------- | :------------------------------------------------ |
| 序章   | [`PREFACE.md`](PREFACE.md)                                   | 為什麼 AI 學會所有知識，卻學不會「懂你」          |
| 第一章 | [`chapters/01-background.md`](chapters/01-background.md)     | 背景與核心理念                                    |
| 第二章 | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | 適用條件與準備工作                                |
| 第三章 | [`chapters/03-core-theory.md`](chapters/03-core-theory.md)   | 四個控制論概念詳解（前饋／積分／分離／自監控）    |
| 第四章 | [`chapters/04-architecture.md`](chapters/04-architecture.md) | 系統架構詳解（三層記憶體 + 技能層 + 資料流）      |
| 第五章 | [`chapters/05-deployment.md`](chapters/05-deployment.md)     | 實操指南（分步驟部署指令，可直接複製）            |
| 第六章 | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md)   | 日常使用與驗證方法                                |
| 第七章 | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | 常見問題排障 + 多 Agent／新理論延伸               |
| 結尾   | [`EPILOGUE.md`](EPILOGUE.md)                                 | 部署之後：架構的意義與後續方向                    |

### 檔案命名說明

本倉庫根目錄和章節檔名使用英文，以相容跨平台和工具鏈。中文來源檔案重新命名對照：

| 本地檔案名稱（中文）            | GitHub 檔案名稱                |
| :------------------------------ | :----------------------------- |
| 序章：為什麼 AI…md              | `PREFACE.md`                   |
| 第一章：背景與核心理念.md       | `chapters/01-background.md`    |
| 第二章：適用條件與準備工作.md   | `chapters/02-prerequisites.md` |
| 第三章：核心理論詳解.md         | `chapters/03-core-theory.md`   |
| 第四章：系統架構詳解.md         | `chapters/04-architecture.md`  |
| 第五章：實操指南.md             | `chapters/05-deployment.md`    |
| 第六章：日常使用與驗證.md       | `chapters/06-daily-usage.md`   |
| 第七章：常見問題與延伸思考.md   | `chapters/07-faq-extensions.md`|
| 結尾：架構之後.md               | `EPILOGUE.md`                  |

檔案內部標題和正文保持中文不變。`translations/` 目錄預留給其他語言譯本（如 `en/`、`ja/` 等）。

### 輔助檔案

| 檔案                                                         | 說明                                                     |
| :----------------------------------------------------------- | :------------------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | 第五章全部指令的純提取版（無解釋，方便快速執行）         |
| [`examples/`](examples/)                                     | L2／L3 範例、積分控制表範例、閉環梳理輸出範例            |
| [`CONTRIBUTING.md`](CONTRIBUTING.md)                         | 貢獻指南                                                 |
| [`LICENSE`](LICENSE)                                         | 開源協議                                                 |

---

## 適用平台

- ✅ **Hermes 3**（完全原生支援，所有指令無縫執行）
- ✅ **Claude（with MCP）**（需微調工具呼叫語法，核心架構完全適用）
- ✅ **自訂 GPTs**（用 Knowledge 檔案模擬記憶，用 Actions 模擬技能）
- 🔸 其他具備**持久化記憶 + 技能／程序性模組**的 Agent 平台
- 🔸 無 Skill 功能的平台（可降階執行，見[第七章 7.1 節](chapters/07-faq-extensions.md)）

---

## 效果速覽

部署前後對比：

| 維度       | 部署前                            | 部署後                                       |
| :--------- | :-------------------------------- | :------------------------------------------- |
| 任務啟動   | 你說需求，Agent 直接開始          | Agent 先輸出避坑清單和風險預判，你再確認     |
| 同類錯誤   | 每次糾正，下次照犯                | 第二次出現時自動下沉為規則，第三次不再犯     |
| 記憶信噪比 | 原則、步驟、案例混在一起          | 三層分離，原則和步驟各有歸屬                 |
| 交付品質   | 你檢查，發現套話／格式問題再改    | Agent 自己過五關閘門，不合格不交付           |
| 系統進化   | 憑感覺偶爾調整一下                | 每週說「起飛」，自動覆盤、自動優化           |

---

## 核心理念

> **你做的不是一次 prompt engineering，而是一次 architecture engineering。**
>
> 你不是在教 Agent 什麼新的知識，而是在用系統工程的思維，為它設計一套能穩定執行、持續進化的內部架構。

更多背景和理念闡述，見[序章](PREFACE.md)和[第一章](chapters/01-background.md)。

---

## 專案名稱

**Cybernetic Your Agent** — 為你的 Agent 注入控制論基因。

我們不教 AI 新知識，我們用錢學森工程控制論的前饋、積分控制、層級分離、自監控四個概念，重塑 Agent 的記憶與技能架構。讓 Agent 從聽懂指令，進化到懂你的判斷邏輯——真正成為*你的* Agent。

---

## 授權條款

本專案採用 [MIT License](LICENSE)。

---

## 致謝

- 錢學森《工程控制論》— 本教學的理論根基
- 最初提出「用控制論組織 Agent 記憶體」思路的筆記作者及留言區所有實測回饋者
- 所有在早期版本中幫助測試和改進架構的協作者

## Star History

<a href="https://www.star-history.com/?repos=zeronesun%2Fcybernetic-your-agent&type=date&legend=bottom-right">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&theme=dark&legend=bottom-right" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
 </picture>
</a>

