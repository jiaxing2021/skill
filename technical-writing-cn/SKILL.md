---
name: technical-writing-cn
description: Use this skill when the user asks in Chinese to write, revise, critique, or structure technical documents, development plans, READMEs, architecture designs, RFC-style proposals, implementation plans, or engineering design docs. Prefer this skill when the desired output is documentation or a development proposal rather than code edits.
---

# 技术文档写作

## 使用原则

用于技术方案、开发计划、README、架构设计、RFC 和工程设计文档。默认先吸收用户已有草稿、代码或想法，识别目标读者和文档用途，再产出结构化中文文档。内容要求信息完整、结构清晰、论证可检查。

## 工作流

1. 先判断文档类型：技术方案、开发计划、README、架构设计、RFC、评审材料。
2. 识别读者：开发者、维护者、评审者、PM、运维或混合读者。
3. 提取事实、假设、约束、风险和未决问题；不要把假设写成事实。
4. 如需理解代码，用 `rg` 和局部文件读取获取必要依据，不全量读取。
5. 先给结构或提纲；若用户要求直接成稿，可直接输出完整文档。
6. 对方案类文档必须写 tradeoff、风险、验证方式和落地步骤。
7. 对 README 必须优先写安装、运行、配置、测试、常见问题和项目结构。

## 推荐结构

技术方案：

```markdown
# 标题

## 背景
## 目标
## 非目标
## 现状与约束
## 方案
## 接口 / 数据流 / 模块设计
## 权衡
## 风险与边界情况
## 验证方式
## 实施计划
## 未决问题
```

开发计划：

```markdown
# 标题

## 目标
## 范围
## 任务拆分
## 里程碑
## 验证标准
## 风险
## 依赖
```

README：

```markdown
# 项目名

## 简介
## 功能
## 环境要求
## 安装
## 配置
## 运行
## 测试
## 项目结构
## 常见问题
```

架构设计：

```markdown
# 标题

## 背景
## 架构目标
## 总体架构
## 核心模块
## 数据流
## 部署 / 运行时
## 扩展性
## 可观测性
## 安全与权限
## 风险
```

## 写作标准

- 中文表达直接、客观、技术化。
- 优先先列限制、边界、风险，再写结论。
- 避免营销口吻、空泛价值描述和重复解释。
- 对用户方案做技术批判时，按证据、逻辑、边界情况评价。
- 关键结论可给置信度；推测必须标明“推测”。
- 不要为了显得完整添加无依据内容。
