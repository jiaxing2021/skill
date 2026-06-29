---
name: project-architecture-review-cn
description: Use this skill when the user asks in Chinese to review or improve software architecture, module boundaries, scalability, maintainability, system design, or technical proposals.
---

# 架构评审

## Goal

目标不是设计更复杂的架构，而是以合理复杂度满足当前需求，并保证未来可维护。

始终优先：

> 正确性 > 简单性 > 一致性 > 可维护性 > 可扩展性 > 开发效率

---

# Working Policy

## 1. Understand Context

首先理解：

- 系统目标
- 当前需求
- 设计约束
- 业务特点

不要脱离业务讨论架构。

---

## 2. Evaluate The Whole System

重点关注：

- 模块职责
- 模块边界
- 数据流
- 调用链
- 依赖关系
- 状态管理

优先整体设计，而不是局部代码。

---

## 3. Complexity First

重点评估：

系统是否：

- 容易理解
- 容易修改
- 容易扩展
- 容易定位问题

避免：

- 过度抽象
- 提前设计未来需求
- 无意义分层
- 为局部优雅增加整体复杂度

---

## 4. Quality Attributes

重点分析：

- 正确性
- 稳定性
- 可维护性
- 可扩展性
- 可测试性
- 可观测性

必要时分析：

- 性能
- 安全性
- 成本

---

## 5. Explain Trade-offs

不要只有建议。

说明：

为什么修改。

收益是什么。

成本是什么。

什么时候值得改。

什么时候不值得改。

---

# Output

```markdown
# Summary

总体评价

---

## 优点

...

---

## 问题

问题：

原因：

影响：

建议：

---

## 风险

...

---

## 总体建议

...
```

---

# Constraints

- 不为了设计模式而设计模式。
- 不为了未来需求过度设计。
- 不脱离业务讨论架构。
- 优先降低系统整体复杂度。
