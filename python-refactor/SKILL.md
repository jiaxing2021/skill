---
name: python-refactor
description: Refactor Python code to improve readability, maintainability, performance, and adherence to best practices. Use when the user asks to refactor, clean up, optimize, or improve Python code quality.
---

# Python Refactor

## 触发条件

用户要求重构、优化、清理 Python 代码，或改善代码质量时激活。

## 重构流程

### Step 1: 评估现状
- 读取目标代码，理解功能意图
- 识别代码异味（code smells）
- 检查现有测试覆盖情况

### Step 2: 制定方案
- 列出要执行的重构操作及优先级
- 评估每个操作的风险
- 确认不改变外部行为

### Step 3: 执行重构
- 逐步应用变更，每步保持代码可运行
- 使用 SearchReplace 工具精确修改

### Step 4: 验证
- 运行现有测试确认行为不变
- 检查类型注解正确性

## 常见重构操作

### 结构优化
- **提取函数**：将重复逻辑或过长函数拆分为单一职责的小函数
- **提取类**：将相关函数和数据封装为类
- **合并重复**：消除 copy-paste 代码，使用参数化或继承
- **简化条件**：用 early return、guard clause、策略模式替代深层嵌套

### 类型与接口
- **添加类型注解**：为函数签名和关键变量添加 type hints
- **使用 dataclass/TypedDict**：替代裸 dict 和 tuple
- **定义 Protocol/ABC**：明确接口契约

### 性能优化
- **生成器替代列表**：大序列使用 `yield` 或生成器表达式
- **缓存**：`functools.lru_cache` / `functools.cache`
- **避免全局查找**：热路径中局部化频繁访问的名称

### 现代 Python 风格
- **f-string**：替代 `.format()` 和 `%` 格式化
- **walrus 运算符**：`:=` 简化赋值+判断
- **match-case**（3.10+）：替代复杂 if-elif 链
- **pathlib**：替代 `os.path` 操作
- **上下文管理器**：确保资源正确释放

## 输出模板

```markdown
## 重构分析

**代码异味**:
- [列出的问题]

**重构计划**:
1. [操作 1] - 风险：低/中/高
2. [操作 2] - 风险：低/中/高

## 变更说明
[每项变更的原因和效果]

## 验证
- [ ] 测试通过
- [ ] 类型检查通过
- [ ] 无新增 lint 警告
```

## 规则

- 使用中文回答，专业术语保留英文原文
- **绝不改变代码的外部行为**
- 每次重构操作后保持代码可运行
- 优先使用标准库，避免引入新依赖
- 保留原有注释，必要时更新过时注释
