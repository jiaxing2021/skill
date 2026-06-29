---
name: project-audit-cn
description: Use this skill when the user asks in Chinese to inspect an existing project, identify bugs, technical debt, maintainability issues, performance risks, security risks, or improvement opportunities.
---

# 项目审计

## Goal

目标不是立即修改代码，而是系统性评估项目质量，发现真正影响系统的问题，并按优先级给出可执行的改进建议。

始终优先：

> 正确性 > 稳定性 > 安全性 > 性能 > 可维护性 > 代码风格

---

# Working Policy

## 1. Evidence First

所有结论应基于证据。

优先引用：

- 代码
- 调用关系
- 配置
- 日志
- 测试
- 文档

不要仅凭经验推测。

证据不足时明确说明。

---

## 2. Risk First

优先检查真正影响系统的问题：

- Bug
- 数据错误
- 崩溃风险
- 并发问题
- 安全问题
- 性能瓶颈
- 资源泄漏
- 技术债

最后才关注：

- 命名
- 格式
- 风格

不要为了发现问题而制造问题。

---

## 3. Explain Why

每个问题都应说明：

- 为什么是问题
- 产生原因
- 影响范围
- 严重程度

建议使用：

- Critical
- High
- Medium
- Low

不要只说：

> 建议优化。

---

## 4. Actionable

建议必须可执行。

说明：

- 修改方向
- 修改范围
- 是否值得立即处理
- 是否存在更简单方案

避免空泛建议。

---

## 5. Complexity Awareness

不要为了追求理论上的最佳实践而增加系统复杂度。

改进建议应兼顾：

- 收益
- 风险
- 成本

---

# Output

```markdown
# Summary

总体评价

---

## Critical

...

原因：

影响：

建议：

---

## High

...

---

## Medium

...

---

## Low

...

---

# Priority

建议优先处理：

1.

2.

3.
```

---

# Constraints

- 不夸大问题。
- 不把推断描述成事实。
- 不吹毛求疵。
- 不为了风格牺牲稳定性。
- 优先关注真正影响系统质量的问题。
