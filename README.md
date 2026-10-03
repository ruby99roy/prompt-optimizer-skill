# 最简单的提示词优化 Skill

有些任务，你明明知道自己想要什么，却总是和 AI 来回解释。这一个小 Skill 的作用很简单：把你的半句话，整理成一段能直接交出去做事的提示词。

我们只需在需要的任务开一个临时对话操作，它能帮你两件事：

- **先给你一版能直接发送的提示词**：信息够了就直接给；确实缺关键内容时，才一次问最多 3 个问题。
- **顺手教你怎么写**：你愿意时，它用刚刚的案例解释改了什么，让你下次能自己写得更好。

它只在你手动输入 `$prompt-optimizer` 时工作，不会自动打扰普通对话，也不会替你执行开发、搜索或修改任务。

## 第一次使用：照着做

```text
① 新建一个临时对话
  这里只用来把你的想法说清楚。
        ↓
② 输入 $prompt-optimizer，再写下你的想法
        ↓
③ 复制它给你的“最终提示词”
        ↓
④ 回到主工作对话，粘贴并发送
  这时 Codex 才开始实际开发。
```

## 这样输入

只写原始想法就可以；“优化方向”可写可不写。

```text
$prompt-optimizer

帮我做一个周易角色扮演小程序。
优化方向：先做最简单的 MVP，让 Codex 可以直接开始开发。
```

通常会直接收到一段带有 `【可直接发送给 Codex 的提示词】` 标题的内容。复制标题下的整段内容，粘贴到主工作对话即可。

如果它真的无法判断关键内容，才会一次性问你 1 至 3 个问题；你回答后，它就给最终版，不会反复追问。

## 想学习再开启教学

每次给出最终版后，Skill 会问一句：

```text
要不要我顺便用这次案例讲解优化思路？
```

回复 `要教学` 或 `教我`，它会用当前案例简短说明：

```text
原始提示词
    ↓
目标 / 背景 / 约束 / 完成标准
    ↓
关键改动（最多 3 条）
    ↓
下次可复用的一小段写法
```

不想学就不用回复；它不会自动进入教学，也不会给普通任务增加步骤。

## 对结果不满意怎么办

直接在同一个临时对话里说：

```text
再优化：上一版太泛了。我只想要微信小程序的 MVP，不要登录和支付。
```

反馈足够明确时，Skill 会直接给第二版；不够明确时，才会再问最多 3 个针对性问题。你不需要重新粘贴原始需求。

## 为什么建议用临时对话

| 对话 | 负责什么 | 最后留下什么 |
| --- | --- | --- |
| 临时对话 | 打磨提示词、回答澄清问题、可选教学 | 提示词的讨论过程 |
| 主工作对话 | 执行最终提示词 | 真正的开发过程和结果 |

这样主工作对话里不需要保留“这句话怎么写得更好”的来回讨论，只保留实际做事需要的内容。它不会让所有模型调用都免费，但通常能让主工作对话更干净、更省上下文。

简单任务或你已经写得很清楚时，直接交给正在使用的 Agent 更快，不必使用这个 Skill。

## 安装到你的 Agent

核心文件是 `SKILL.md`。Codex 的额外显示配置在 `agents/openai.yaml` 中，其他 Agent 会忽略它，不影响核心规则。

| Agent | 推荐安装方式 | 安装后怎么用 |
| --- | --- | --- |
| Codex | 把仓库克隆到 `~/.codex/skills/prompt-optimizer` | 新开对话后输入 `$prompt-optimizer` |
| Claude Code | 把仓库克隆到 `~/.claude/skills/prompt-optimizer` | 重开 Claude Code 后按其 Skills 菜单或命令调用 |
| WorkBuddy | 在“技能”页面选择“添加技能 / 上传技能”，上传本仓库下载的 ZIP 包 | 在已安装技能中启用后，在对话中调用 |
| CodeBuddy Code | 如果你说的 “work Buddy” 是 CodeBuddy Code，克隆到 `~/.codebuddy/skills/prompt-optimizer` | 重开或刷新后调用该 Skill |
| 豆包工作 | 打开“技能·连接器·伙伴”，点击 `+` 后选择“上传技能”；若你的版本没有上传入口，选“与豆包对话新建技能”并使用下方提示词 | 在技能列表中启用后调用 |

### Codex / Claude Code / CodeBuddy Code 的命令

本项目的 GitHub 地址：`https://github.com/ruby99roy/prompt-optimizer-skill`

```bash
# Codex
git clone https://github.com/ruby99roy/prompt-optimizer-skill.git ~/.codex/skills/prompt-optimizer

# Claude Code
git clone https://github.com/ruby99roy/prompt-optimizer-skill.git ~/.claude/skills/prompt-optimizer

# CodeBuddy Code
git clone https://github.com/ruby99roy/prompt-optimizer-skill.git ~/.codebuddy/skills/prompt-optimizer
```

Windows 下，Codex 的目标目录通常是：

```text
C:\Users\<你的用户名>\.codex\skills\prompt-optimizer
```

### 直接复制给 Agent 的安装提示词

不想自己找目录时，把下面整段发给你正在使用的 Agent；把方括号里的内容替换掉：

```text
请把 GitHub 仓库 https://github.com/ruby99roy/prompt-optimizer-skill 里的 prompt-optimizer 安装为我的个人全局 Skill。

目标平台：[Codex / Claude Code / WorkBuddy / CodeBuddy Code / 豆包工作]

要求：
1. 先读取仓库中的 README.md 和 SKILL.md，确认内容只是提示词优化规则；
2. 使用该平台官方推荐的个人级 Skill 安装方式；
3. 保留“只手动调用”的行为，不要改成自动触发；
4. 不安装额外软件、不申请 API Key，也不要改动其他已有 Skill；
5. 完成后告诉我：实际安装位置、如何调用、是否需要重启或刷新；
6. 如果该平台不支持直接导入这个 Skill，要明确说明原因，并告诉我最短的可行替代方式，不要假装已经安装成功。
```

不同版本的 WorkBuddy 和豆包工作，上传入口或 Skill 包格式可能不同；以你实际看到的页面为准。

## 使用边界

- 仅手动调用，不会自动影响普通对话。
- 原始提示词是唯一必填项；不要求填表。
- 只使用当前对话中明确、相关的背景，不臆造需求。
- 只优化提示词，不会自行开发、搜索或修改文件。
- 不要把密码、API Key 或其他敏感信息贴进提示词。

## 文件结构

```text
prompt-optimizer/
├── SKILL.md              # Skill 行为规则
├── README.md             # 小白使用说明
└── agents/openai.yaml    # Codex 的显示名与调用策略
```
