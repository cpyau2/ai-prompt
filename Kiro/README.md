# Prompts 文件夹

这是 Kiro AI 助手系统的 prompt 模板库，包含了各种不同场景下使用的标准化指令模板。

## 文件夹结构

```
prompts/
├── model-edit-prompts/     # 模型特定的代码编辑 prompt
├── tool-prompts/          # 工具操作相关的 prompt
├── workflow-prompts/      # 工作流程相关的 prompt
├── system-prompts/        # 系统级别的 prompt
└── README.md             # 本文件
```

## 分类说明

### 1. Model Edit Prompts (`model-edit-prompts/`)
- 针对不同 AI 模型的代码编辑指令模板
- 包含 14 种不同模型的编辑 prompt
- 确保代码编辑请求的一致性和准确性

### 2. Tool Prompts (`tool-prompts/`)
- 各种工具操作的标准化指令
- 包含文件操作、搜索、命令执行等工具
- 定义参数说明、使用规则和最佳实践

### 3. Workflow Prompts (`workflow-prompts/`)
- 复杂开发工作流程的指令模板
- 支持 Spec 流程（需求→设计→实施→执行）
- 包含 Hook 创建等自动化流程

### 4. System Prompts (`system-prompts/`)
- Kiro AI 助手的基础配置
- 定义身份、能力、行为规则
- 包含安全规则和响应风格指导

## 使用说明

每个子文件夹都包含详细的 README 文件，说明该类别下所有 prompt 的用途和内容。这些 prompt 模板为 Kiro 系统提供了标准化的指令库，确保在不同场景下都能提供一致和有效的 AI 助手服务。 