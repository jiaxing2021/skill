my skill push in github created by jiaxing2021

# Skill 使用指南

根据当前目标选择对应的 Skill，而不是根据任务类型。

| Skill                                    | 目标     | 适用场景                                             | 语言 |
| ---------------------------------------- | -------- | ---------------------------------------------------- | ---- |
| **project-development-cn**         | 实现需求 | 新功能、Bug 修复、重构、测试、代码修改               | 中文 |
| **project-debug-cn**               | 定位根因 | 程序异常、测试失败、线上问题、性能异常、崩溃分析     | 中文 |
| **project-architecture-review-cn** | 评审设计 | 架构设计、模块划分、系统设计、技术方案评审           | 中文 |
| **project-audit-cn**               | 全面检查 | 项目巡检、代码质量、技术债、性能、安全、可维护性评估 | 中文 |
| **project-test-cn**                | 代码测试 | 测试策略、用例设计、覆盖率、反模式                   | 中文 |

英文请求对应的调试场景使用 `debug-helper`（不是 `project-debug-cn`）；`explain-code`、`python-refactor`、`define-goal`、`technical-writing-cn`、`pdf` 为独立工具型 skill，不属于本工作流，按需单独触发。

---

## 推荐工作流

```text
project-architecture-review-cn
        ↓
project-test-cn（测试策略）
        ↓
project-development-cn（实现，测试策略不明确时移交回 project-test-cn）
        ↓
project-debug-cn（如有问题）
        ↓
project-audit-cn（上线前或阶段性检查，severity 分级 Critical/High/Medium/Low）
```

---

## 选择原则

- **需要修改代码** → `project-development-cn`
- **需要测试代码/设计测试策略** → `project-test-cn`
- **中文调试问题** → `project-debug-cn`；**英文调试问题** → `debug-helper`
- **需要评审设计** → `project-architecture-review-cn`
- **需要发现问题或优化项目** → `project-audit-cn`

## 已知限制

- Skill 间引用（如 development → test-cn）为文本级提示，非强制调用；无原生 skill 间 dispatch 机制，依赖模型自觉遵守。
- severity 分级词汇（Critical/High/Medium/Low）仅在 development 与 audit 间统一，architecture-review 使用独立的 Low/Medium/High 风险等级，未完全对齐。

