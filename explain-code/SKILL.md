---
name: explain-code
description: Analyze and explain code logic, design patterns, function/class relationships, and potential issues. Use when the user selects code, asks "explain this code", "what does this do", or needs to understand unfamiliar code. Supports C++, Python, TypeScript, Rust, and other languages.
---

# Explain Code

## 触发条件

当用户选中代码、指定文件、或要求解释代码时自动激活。

## 分析流程

1. **读取目标代码**：优先使用用户选中的代码片段，否则读取指定文件
2. **识别语言和框架**：判断编程语言、使用的框架/库
3. **结构化分析**：按以下模板输出

## 输出模板

```markdown
## 功能概述
[一句话概括代码的核心功能]

## 关键逻辑
[分步骤解释核心执行流程，使用编号列表]

## 设计模式与技巧
- [列出使用的设计模式、惯用法或高级技巧]

## 函数/类关系
[描述主要函数、类之间的调用和依赖关系，必要时用 mermaid 图]

## 潜在问题
- ⚠️ [可能的 bug、边界情况、性能隐患]

## 依赖说明
[关键的外部依赖和它们的作用]
```

## 规则

- 使用中文回答，专业术语保留英文原文
- 对复杂代码使用 mermaid 图辅助说明
- 如果代码超过 200 行，先给出模块划分再逐模块解释
- 重点解释"为什么"而不是"是什么"
