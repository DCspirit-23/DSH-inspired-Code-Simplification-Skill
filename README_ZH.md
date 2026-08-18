# 查找代码精简机会

[English](README.md)

这是一个需要显式调用的 Codex skill，用于对分支、模块或整个仓库开展有证据支撑的代码精简调查。

它不会停留在格式整理或少写几行代码，而是寻找真正能够减少概念数量与维护面的机会，例如：没有生产消费者的公开接口、重复状态、投机性抽象、冗余生命周期机制、重复造轮子等。

## 核心原则

- 默认从只读调查开始，只有在用户明确授权后才修改代码。
- 通过真实调用方、契约、配置、历史记录和运行时边界证明每个候选项。
- 区分生产消费者、非生产消费者和用途不明确的消费者。
- 将保持行为不变的清理与设计变更分开报告。
- 关注净精简收益，而不是单纯减少代码行数。
- 接受“没有发现足够强的候选项”这一有效结论。

## 安装

可以让 Codex 使用 `$skill-installer` 从本仓库安装，也可以将 `find-code-simplifications` 文件夹复制到以下任一 skill 目录：

- 用户级：`~/.agents/skills/find-code-simplifications`
- 仓库级：`.agents/skills/find-code-simplifications`

Codex skill 采用文件夹结构，其中 `SKILL.md` 为必需文件，其他支持文件为可选。详情参见 [OpenAI 官方自定义文档](https://learn.chatgpt.com/docs/customization/overview#skills)。

## 使用方式

本 skill 被刻意设置为仅支持显式调用：

```text
使用 $find-code-simplifications 调查当前分支。
```

也可以指定更小或更大的范围：

```text
使用 $find-code-simplifications 调查这个模块。
```

```text
使用 $find-code-simplifications 调查整个仓库。
```

调查默认只读。如果希望实施其中某些结论，需要另行明确提出。

## 输出内容

对于每个强候选项，skill 会报告其位置、消费者证据、当前成本、建议的精简方式、预期净收益、行为或契约影响、风险、置信度以及针对性的验证方法。它还会记录具有代表性的被否决候选项，以及已执行检查的状态。

## 仓库结构

```text
.
├── find-code-simplifications/
│   ├── SKILL.md
│   └── agents/
│       └── openai.yaml
├── README.md
└── README_ZH.md
```

`find-code-simplifications/agents/openai.yaml` 已禁用隐式调用，因此只有在用户明确指定时才会运行本 skill。

## 来源

本 skill 由面向 DeepSeek Harness 的代码精简流程改编而来，并已泛化为适用于不同仓库、语言和架构的版本。
