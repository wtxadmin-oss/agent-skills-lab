# Agent Skills Lab

面向 Agent 工具链的 Skills 实验仓库，聚焦可复用能力契约、证据驱动参数提取、子任务路由与人工确认边界。

## Thinking Parameter Extraction

ThinkingParameterExtraction 用于从模型官方文档 URL、官方代码片段或两者组合中提取 Thinking / Reasoning 参数，并生成可审查的结构化证据。

### 路由规则

~~~text
仅代码片段 ──────────────► code_extractor
仅官方文档 URL ─────────► url_extractor
URL + 代码片段 ─────────► 双路提取与一致性检查
                              │
                              └─ 发生冲突 ─► compare
~~~

### 输出内容

- Thinking 启用参数。
- Reasoning effort 参数。
- 允许的 effort 值。
- 原始来源、证据片段与置信度。
- 双来源冲突时的评分、选择和合并原因。

### 质量门禁

- 不发明官方文档未出现的参数。
- 不确定字段必须显式标记。
- 每个候选字段必须能回溯到证据。
- Skill 只生成预览，不自动触发保存。
- 最终持久化必须经过前端人工确认。

## 目录

~~~text
ThinkingParameterExtraction/
└── SKILL.md
~~~

## 适用场景

- 异构模型 Provider 的 Thinking 参数适配。
- 模型版本升级后的参数兼容检查。
- 从官方文档和示例代码生成可审计配置。
- 将复杂 Agent 能力沉淀为可复用 Skill Contract。

## 工程关注点

该仓库强调 Skills 的边界设计，而不是只描述 Prompt：

- 输入和运行时上下文必须明确。
- 子任务的触发条件和输出 Schema 必须稳定。
- 工具读取与持久化写入必须分离。
- 高风险或冲突结果需要 Human-in-the-Loop。

