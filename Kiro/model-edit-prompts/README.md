# Model Edit Prompts

这个文件夹包含了针对不同 AI 模型的代码编辑 prompt 模板。

## 包含的模型类型：

- **Alpaca** - `alpaca-edit.md`
- **Claude (Anthropic)** - `claude-edit.md`
- **CodeLlama 70B** - `codellama-70b-edit.md`
- **DeepSeek Coder** - `deepseek-edit.md`
- **Gemma** - `gemma-edit.md`
- **GPT (OpenAI)** - `gpt-edit.md`
- **Llama 3** - `llama3-edit.md`
- **Mistral** - `mistral-edit.md`
- **Neural Chat** - `neural-chat-edit.md`
- **OpenChat** - `openchat-edit.md`
- **Phind** - `phind-edit.md`
- **Simplified** - `simplified-edit.md`
- **XWin-Coder** - `xwin-coder-edit.md`
- **Zephyr** - `zephyr-edit.md`

## 用途

这些 prompt 模板确保代码编辑请求在不同 AI 模型之间保持一致性和准确性，每个模板都针对特定模型的输入格式进行了优化。

## 使用示例

### Claude Edit Prompt 使用说明

#### 模板变量
- **`${otherData.language}`** - 编程语言（如：javascript, python, typescript 等）
- **`${otherData.codeToEdit}`** - 需要编辑的原始代码
- **`${otherData.userInput}`** - 用户的编辑要求/指令

#### 实际使用示例

**输入模板：**
```javascript
```javascript
function add(a, b) {
    return a + b;
}
```

You are an expert programmer. You will rewrite the above code to do the following:

Add input validation to check if both parameters are numbers

Output only a code block with the rewritten code:
```

**输出结果：**
```javascript
Sure! Here is the rewritten code:
```javascript
function add(a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw new Error('Both parameters must be numbers');
    }
    return a + b;
}
```
```

#### 使用流程
1. **准备数据**：确定编程语言、原始代码、编辑要求
2. **填充模板**：将模板变量替换为实际值
3. **发送请求**：使用填充后的 prompt 向对应模型发送请求
4. **获得结果**：接收编辑后的代码

#### 优势特点
- **标准化格式**：确保所有代码编辑请求都遵循相同结构
- **明确指令**：清晰定义输入和期望输出
- **模型优化**：专门为特定模型的特性设计
- **一致性**：保证代码编辑结果的质量和格式 