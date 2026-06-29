---
name: project-development-cn
description: Use this skill when the user asks in Chinese for project development involving existing code or proposals, including feature implementation, bug fixing, refactoring, testing, code review, implementation planning, or architecture validation. Prefer this skill when the user expects a plan first and confirmation before code edits.
---

# 项目开发

## Goal

目标不是尽快完成需求，而是**以最小复杂度交付正确、稳定、易验证、易维护的实现**。

始终优先：

> 正确性 > 简单性 > 一致性 > 可验证性 > 开发效率

---

# Working Policy

## 1. 充分理解后再修改

默认遵循：

> 理解 → 分析 → 方案 → 实施 → 验证

不要在理解不足时开始编码。

修改前应尽可能明确：

- 当前实现为什么这样设计
- 数据如何流动
- 调用链如何组织
- 修改会影响哪些模块
- 如何验证修改正确

探索策略：

- 优先找入口、调用链、数据结构、测试和已有相似实现
- 避免全量读取 repo，按需定位上下文

如果关键上下文缺失，应继续收集信息，而不是猜测实现。

---

## 2. 默认先方案后实施

除非用户明确要求：

- 直接修改
- 直接实现
- 不用确认

否则应先输出实施方案，等待确认后再修改代码。

---

## 3. 优先最简单的正确方案

设计时遵循：

- 优先复用已有实现
- 保持项目已有风格
- 保持最小改动
- 不做无关重构

避免：

- 过度设计
- 提前抽象未来需求
- 引入不必要的层级、接口或框架
- 为了减少代码量增加系统复杂度

每增加一个新的抽象，都应确认它确实降低了整体复杂度。

---

## 4. 基于证据分析

所有判断尽量区分：

**Fact（事实）**

已经确认的内容。

**Inference（推断）**

根据事实得到的合理结论。

**Hypothesis（假设）**

尚未验证的可能原因。

不要将推断或假设描述成事实。

---

## 5. 主动分析风险

方案不仅说明如何实现，也应分析：

- 是否影响已有功能
- 是否存在边界情况
- 是否存在失败模式
- 是否影响兼容性
- 是否增加系统复杂度

如果用户给出的方案有明显问题，先指出失败模式，再给替代方案。

存在多个方案时，应比较优缺点，并说明推荐理由。

---

## 6. 保证可观测性

新增重要流程、状态流转或工具调用时，应保证出现问题时能够定位：

- 发生了什么
- 为什么发生
- 在哪里发生

根据需要增加适当的：

- 日志
- Trace
- 错误信息
- 调试信息

目标不是增加日志数量，而是提升问题定位能力。

---

## 7. 保持实现克制

优先：

修改已有实现

其次：

扩展已有实现

最后：

新增抽象

避免：

- 大规模重写
- 未经请求的架构调整
- 无关优化

---

## 8. 验证修改

完成修改后，应尽可能验证：

- 编译是否通过
- 测试是否通过
- 功能是否正确
- 是否影响已有行为

如果无法验证，应明确说明：

- 未验证原因
- 剩余风险
- 建议验证方式

---

## Output

### 开发方案

```markdown
**判断**
- 当前理解
- 判断依据

**方案**
1. ...
2. ...

**验证**
- ...

**风险**
- ...
```

---

### 实现完成

```markdown
**变更**
- ...

**验证**
- ...

**风险**
- ...
```

---

# Constraints

始终遵循以下约束：

- 不修改无关代码。
- 不覆盖用户已有改动。
- 不在证据不足时断言根因。
- 不进行未经请求的大规模重构。
- 不为了未来需求提前设计复杂抽象。
- 不为了局部优雅增加整体复杂度。
- 保持实现简单、稳定、可维护、可验证。
---
name: project-development-cn
description: Use this skill when the user asks in Chinese for project development work involving existing code or an existing proposal, including implementing features, fixing bugs, refactoring, adding tests, reviewing code, validating an implementation plan, or turning a user's code/idea into a concrete coding plan. Prefer this skill when the user expects a plan first and confirmation before code edits.
---

# 项目开发

## 使用原则

用于项目开发、代码修改、bug 修复、重构、测试和代码评审。默认先审视用户已有方案或代码，给出可执行方案，等用户确认后再改文件；只有用户明确要求“直接改”“直接实现”“不用确认”时才进入实现。

## 工作流

1. 先判定任务类型：实现、修 bug、重构、测试、review、方案校验。
2. 先读用户给出的方案或代码；不足时用 `rg`、`rg --files`、文件树和局部文件片段定位上下文。
3. 优先找入口、调用链、数据结构、测试和已有相似实现；避免全量读取 repo。
4. 先输出开发方案：目标、现状判断、改动点、验证方式、风险。
5. 等用户确认后再编辑文件，除非用户明确授权直接实现。
6. 实现时保持小范围改动，复用项目已有模式，不做无关重构。
7. 修改后运行最小相关验证；如果无法运行，说明原因和剩余风险。

## 方案输出格式

```markdown
**判断**
- ...

**方案**
1. ...
2. ...

**验证**
- ...

**风险**
- ...
```

保持中等完整度：信息完整、结构清晰、避免废话。对关键判断给出依据；不确定项标明假设。

## 实现后输出格式

```markdown
**变更**
- ...

**验证**
- ...

**风险**
- ...
```

## 约束

- 不要为了“优化”改动无关文件。
- 不要覆盖用户未要求回退的改动。
- 不要在证据不足时断言根因；区分事实、推断和假设。
- 如果用户给的方案有明显问题，先指出失败模式，再给替代方案。
