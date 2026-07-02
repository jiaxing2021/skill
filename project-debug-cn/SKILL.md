---
name: project-debug-cn
description: Use this skill when the user asks in Chinese to investigate runtime failures, crashes, production issues, incorrect behavior, test failures, or other debugging tasks. For English-language debugging requests, use debug-helper instead.
---

# 问题定位

## Goal

目标不是尽快修改代码，而是准确定位根因，并以最小改动解决问题。

始终坚持：

> Evidence → Analysis → Root Cause → Fix → Verification

不要跳过定位直接修改。

---

# Working Policy

## 1. Collect Facts

首先收集：

- 错误现象
- 日志
- 错误信息
- 环境
- 输入数据
- 重现步骤
- 最近修改

不要先猜原因。

---

## 2. Narrow Down

逐步缩小范围：

系统

↓

模块

↓

调用

↓

函数

↓

状态

↓

数据

↓

根因

不要一次修改多个地方。

---

## 3. Evidence First

所有分析都区分：

Fact

Inference

Hypothesis

每一步推断都应有依据。

---

## 4. Find Root Cause

不要停留在：

"这里报错。"

继续分析：

为什么这里报错？

为什么进入这里？

为什么状态异常？

为什么数据错误？

直到找到真正原因。

---

## 5. Minimal Fix

修复应：

- 保持最小改动
- 不引入新的风险
- 说明为什么能够解决问题

必要时增加：

- 测试
- 日志
- 边界处理

防止再次发生。

---

## 6. Verify

验证：

- 问题是否解决
- 是否影响其它功能
- 是否存在副作用

无法验证时明确说明剩余风险。

---

# Output

```markdown
# 问题

...

---

# 分析

事实：

推断：

假设：

---

# 根因

...

---

# 修复方案

...

---

# 验证

...

---

# 风险

...
```

---

# Constraints

- 不跳过定位直接修复。
- 不把现象当根因。
- 不凭经验猜测。
- 不扩大修改范围。
- 优先定位真正原因，而不是消除报错现象。

**退出阈值**：以下任一情况必须停止并向用户提问：
- 复现步骤缺失或无法在现有信息下复现
- 定位到 2 个及以上可能根因，且现有日志/证据不足以排除其一
- 涉及跨服务/跨进程问题，但缺少对方服务的日志或接口行为信息
