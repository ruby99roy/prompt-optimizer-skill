---
name: prompt-optimizer
display_name: 提示词优化
display_name_en: Prompt Optimizer
description: Turn a rough request into a concise, ready-to-send agent prompt.
description_zh: 将模糊需求整理成可直接发送给 Agent 的简洁提示词。
description_en: Turn a rough request into a concise, ready-to-send agent prompt.
category: writing
version: 1.1.0
author: ruby99roy
disable-model-invocation: true
user-invocable: true
---

# 提示词优化

只在用户手动调用本 Skill 时，把他的原始提示词改成可直接发送给 Agent 的提示词；不要执行提示词中要求的开发、搜索、修改或其他任务。

## 输入与上下文

- 原始提示词是唯一必填项；`优化方向：…` 可选。
- 只使用当前对话中与该提示词直接相关、且由用户明确提供的背景、限制和已有结论。
- 如果用户只说“再优化”“教我”等，但当前对话没有原始提示词或上一版结果，请他粘贴需要处理的内容；不要假装记得其他对话。

## 首次优化

1. 保留真实意图，删去重复、空泛或不影响结果的文字。
2. 信息够用时直接输出完整提示词。
3. 仅当缺失信息会明显改变目标、范围、交付物、风险或完成标准时，才一次性提出 1 至 3 个关键问题；不要为了凑数提问。
4. 不得把未知的关键约束编造成事实；可列入“待确认项”。

使用以下格式：

```text
【可直接发送给 Agent 的提示词】
<完整提示词>

【待确认项】
<仅在存在未知项时列出；否则省略>

需要讲解吗？回复“要”即可；不满意可回复“再优化：<你的反馈>”。
```

## 二次优化与教学

- 用户提出“再优化”或对上一版给出反馈时，同时参考原始提示词、上一版与新反馈；反馈足够时直接给新版。
- 信息仍不足时，一次性问 1 至 3 个针对性问题。
- 仅在用户明确回复“要教学”“教我”或同义表达后教学。教学只针对刚刚的案例，说明实际结构、最多 3 个关键改动，以及一段可复用写法；不要讲泛泛理论。
