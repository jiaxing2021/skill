my skill push in github created by jiaxing2021
# Skill 使用指南

根据当前目标选择对应的 Skill，而不是根据任务类型。

| Skill | 目标 | 适用场景 |
|-------|------|---------|
| **project-development-cn** | 实现需求 | 新功能、Bug 修复、重构、测试、代码修改 |
| **project-debug-cn** | 定位根因 | 程序异常、测试失败、线上问题、性能异常、崩溃分析 |
| **architecture-review-cn** | 评审设计 | 架构设计、模块划分、系统设计、技术方案评审 |
| **project-audit-cn** | 全面检查 | 项目巡检、代码质量、技术债、性能、安全、可维护性评估 |

---

## 推荐工作流

```text
Architecture Review
        ↓
Project Development
        ↓
Project Debug（如有问题）
        ↓
Project Audit（上线前或阶段性检查）
```

---

## 选择原则

- **需要修改代码** → `project-development-cn`
- **需要定位问题** → `project-debug-cn`
- **需要评审设计** → `architecture-review-cn`
- **需要发现问题或优化项目** → `project-audit-cn`
