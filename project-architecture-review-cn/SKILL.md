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

# Checklist

评审时逐项核对，标记 Pass/Fail/N-A：

- [ ] 模块边界是否单一职责，是否存在循环依赖
- [ ] 数据流是否可追溯（能否画出输入到输出的完整路径）
- [ ] 状态管理是否集中，是否存在多处真相源（multiple sources of truth）
- [ ] 错误处理路径是否明确（失败时系统进入什么状态）
- [ ] 关键路径是否有可观测性（日志/trace/metrics）
- [ ] 是否存在为未验证的未来需求预留的抽象
- [ ] 扩展新功能是否需要修改现有模块而非新增

---

# Output

```markdown
# Summary

总体评价（1-2 句，含总体风险等级：Low/Medium/High）

---

## Checklist 结果

| 项目 | 结果 | 说明 |
|------|------|------|
| ... | Pass/Fail/N-A | ... |

---

## 问题

问题：

原因：

影响：

建议：

成本 vs 收益：

---

## 总体建议

...
```

## 示例（片段）

问题：订单状态由 `OrderService` 和 `PaymentService` 各自维护一份副本
原因：历史上分两个团队开发，未做状态收敛
影响：支付成功但订单状态未同步时出现数据不一致，已知有 2 次线上事故记录
建议：将订单状态收敛到单一 `OrderStateStore`，`PaymentService` 通过事件通知而非直接写状态
成本 vs 收益：改造成本中等（预计 3-5 天），收益是消除一类数据不一致风险，值得做

---

# Constraints

- 不为了设计模式而设计模式。
- 不为了未来需求过度设计。
- 不脱离业务讨论架构。
- 优先降低系统整体复杂度。

**退出阈值**：以下任一情况必须停止并向用户提问：
- 系统目标/业务约束未明确，无法判断某设计是否"合理复杂度"
- Checklist 中 3 项及以上因信息不足无法判定 Pass/Fail
- 用户要求的改动与现有架构根本冲突，且无法确认哪个优先级更高
