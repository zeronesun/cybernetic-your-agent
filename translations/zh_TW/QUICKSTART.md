# 快速部署：一句話讓 Agent 完成控制論架構訓練

用一句話指令，讓 Agent 自動讀取教程並完成整套控制論架構的訓練。

---

## 適用條件

妳的 Agent 必須能夠：
- 存取 GitHub 公開倉庫
- 寫入記憶（`memory` 功能）
- 建立技能（`skill` 或類似程序性模組）

如果不滿足，請跳至 [手動訓練](#手動訓練)。

---

## 一句話指令（複製發給 Agent）

```
按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 訓練我。每步確認，完成後閉環測試。
```

> Agent 將自動讀取全部指令，依次寫入 L1 元認知框架、初始化 L2/L3、建立積分控制表、建立四個核心技能，並在最後執行一次閉環測試。

---

## 訓練過程（妳只需確認）

1. Agent 讀取部署指令檔案
2. 寫入 L1 元認知框架
3. 初始化 L2 和 L3（Agent 向妳確認提煉結果）
4. 建立積分控制表
5. 建立四個技能：`delivery_gate`、`feedforward_startup`、`control_loop_review`、`user_profile_maintainer`
6. 執行首次閉環測試（說「起飛」）

全程約 40 分鐘，妳只需在關鍵步驟確認。

---

## 手動訓練

如果 Agent 無法存取 GitHub，請先複製下方內容發給它：

> 我將發送一份訓練指令列表，請逐條執行。每完成一步告知我。

然後打開 👉 [scripts/deployment-commands.md](scripts/deployment-commands.md)，將內容分段複製給 Agent。

---

## 訓練完成標誌

Agent 應顯示：

- ✅ 四個核心技能已建立
- ✅ 積分控制表已就緒
- ✅ 首次閉環測試通過

此時妳的 Agent 已轉變為以控制論為骨架、能自我進化的協作引擎。

---

## 日常使用小抄

- 建新任務 → Agent 自動輸出避坑清單，妳說「直接做」即開始
- 出錯了 → 同類問題第二次出現時，Agent 自動下沉為規則
- 復盤 → 說 **「起飛」**，Agent 執行完整九步復盤並自我最佳化

---

## 專案連結

- 完整教程：[chapters/](chapters/)
- 中文源檔案對照：[檔案命名說明](README.md#檔案命名說明)
- 貢獻或問題反饋：[CONTRIBUTING.md](CONTRIBUTING.md)