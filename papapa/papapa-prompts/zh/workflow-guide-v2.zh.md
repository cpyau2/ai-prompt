# 5階段開發工作流程

## 概述

使用LLM進行軟件開發的結構化方法，跨越5個不同的階段。每個階段都建立在之前的階段之上，需要包含階段提示和生成的文檔以維持上下文。

## 常用提示

- **"需要澄清？"** - 要求LLM識別並請求澄清不清楚的方面
- **"用發現的新需求更新01-requirements.md"** - 用設計階段發現的需求更新需求文檔
- **"如果需要設計更改，更新02-design.md"** - 當實施揭示設計問題時更新設計文檔
- **"在任務執行之間始終等待批准"** - 提醒LLM在階段4任務之間暫停等待批准
- **"我們在迭代X，階段X"** - 在返回前一階段時指示迭代週期（迭代 = 範圍內的功能）
- **"為子任務添加編號"** - 要求LLM為實施計劃子任務添加編號系統
- **"記住在階段4執行期間標記任務為完成"** - 提醒LLM更新實施計劃複選框

## 階段結構

---

### 階段1：需求收集

- **包含：** `@base-prompt.md` + `@p01-requirements-gathering.md`
- **目的：** 定義功能應該做什麼
- **輸出：** `specs/{feature_name}/01-requirements.md`

---

### 階段2：設計創建

- **包含：** `@base-prompt.md` + `@p02-design-creation.md` + `@specs/{feature_name}/01-requirements.md`
- **目的：** 設計功能將如何構建
- **輸出：** `specs/{feature_name}/02-design.md`
- **注意：** 如果您需要對設計方法有信心，請要求LLM提供代碼片段

---

### 階段3：實施計劃

- **包含：** `@base-prompt.md` + `@p03-implementation-planning.md` + `@specs/{feature_name}/01-requirements.md` + `@specs/{feature_name}/02-design.md`
- **目的：** 將工作分解為可管理的編碼任務
- **輸出：** `specs/{feature_name}/03-implementation-plan.md`

---

### 階段4：實施執行

- **包含：** `@base-prompt.md` + `@p04-implementation-execution.md` + `@specs/{feature_name}/01-requirements.md` + `@specs/{feature_name}/02-design.md` + `@specs/{feature_name}/03-implementation-plan.md`
- **目的：** 一個接一個地執行計劃的任務
- **輸出：** `specs/{feature_name}/04-changes-log.md`（僅在臨時更改發生時）

---

### 階段5：文檔更新

- **包含：** `@base-prompt.md` + `@p05-documentation-update.md` + `@specs/{feature_name}/01-requirements.md` + `@specs/{feature_name}/02-design.md` + `@specs/{feature_name}/03-implementation-plan.md` + `@specs/{feature_name}/04-changes-log.md`（如果存在）
- **目的：** 更新所有文檔以反映實際實施
- **輸出：** 更新的主文檔文件
- **注意：** 在實踐中是可選的 - 許多項目在階段4停止

## 關鍵原則

### 文檔積累
- 每個階段都包含所有之前生成的文檔
- 包含階段提示和生成的文檔
- 這防止LLM上下文丟失和幻覺

### 階段進展
- 在進入下一階段之前等待明確批准
- 如果需要重大更改，可以返回前一階段
- 每個階段都建立在積累的上下文之上
- 使用"我們在迭代X，階段X"來指示迭代週期
- 每次迭代 = 通過階段1-5的範圍內功能

### 實施控制
- 在階段4期間一次執行一個任務
- 每個任務後停止等待用戶審查（項目符號編號是暫停點）
- 在 `04-changes-log.md` 中記錄所有更改
- 在階段5中更新需求/設計文檔，而不是在實施期間
- 如果發現設計缺陷，立即停止並建議解決方案
- 在進行下一個子任務之前修復所有錯誤（特別是TypeScript）

## 文件結構

```
specs/{feature_name}/
├── 01-requirements.md
├── 02-design.md
├── 03-implementation-plan.md
├── 04-changes-log.md (可選，僅在臨時更改發生時)
└── 更新的主文檔 (階段5輸出)
```

### 文件管理指導原則
- **對功能名稱使用kebab-case**（例如，`excel-processor`、`user-authentication`）
- **保留：** `01-requirements.md` 和 `02-design.md`（永久文檔）
- **廢棄：** `03-implementation-plan.md`、`04-changes-log.md`（臨時工作文件）
- **測試用例：** 在階段2生成測試文檔（markdown），在階段4實施期間添加JS註釋
- **Excel夾具：** LLM只能描述內容 - 您必須手動創建Excel文件並記錄過程
- **注意：** 測試文檔工作流程"有待確認" - 未經過密集驗證
- **注意：** 編號任務/子任務需要明確批准 - 編號 = 暫停點

## 任務執行示例

### 未編號子任務（作為1個單元執行）
```
- [ ] **11.2** 測試變異鉤子
  - 使用useCreateUser鉤子測試用戶創建
  - 使用useUpdateUser鉤子驗證用戶更新
  - 使用useDeleteUser鉤子測試用戶刪除
  - 檢查緩存失效策略
```

### 編號子任務（作為4個單元執行，每個之間需要批准）
```
- [ ] **11.2** 測試變異鉤子
  - [ ] 11.2.1 使用useCreateUser鉤子測試用戶創建
  - [ ] 11.2.2 使用useUpdateUser鉤子驗證用戶更新
  - [ ] 11.2.3 使用useDeleteUser鉤子測試用戶刪除
  - [ ] 11.2.4 檢查緩存失效策略
```

## 為什麼包含生成的文檔？

**對工作流程成功至關重要：** 包含生成的文檔防止LLM：
- 在階段之間丟失上下文
- 重新開始並產生幻覺解決方案
- 忘記之前的決策和需求
- 重複已經完成的工作

**始終包含：** 階段提示 + 之前階段的所有生成文檔
