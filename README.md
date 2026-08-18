# Find Code Simplifications

[中文说明](README_ZH.md)

An explicitly invoked Codex skill for evidence-backed code simplification investigations across a branch, module, or repository.

It looks beyond cosmetic cleanup to find meaningful reductions in concepts and maintained surface area: dead public surfaces, duplicated state, speculative abstractions, redundant lifecycle machinery, hand-rolled infrastructure, and similar sources of avoidable complexity.

## Core principles

- Start read-only and modify code only after explicit authorization.
- Prove each candidate through real consumers, contracts, configuration, history, and runtime boundaries.
- Distinguish production, non-production, and ambiguous consumers.
- Separate behavior-preserving cleanup from design changes.
- Prefer net simplification over raw line-count reduction.
- Accept “no strong candidates found” as a valid result.

## Installation

Ask Codex to install the skill from this repository with `$skill-installer`, or place this repository's contents in one of the supported skill directories:

- User scope: `~/.agents/skills/find-code-simplifications`
- Repository scope: `.agents/skills/find-code-simplifications`

Codex skills use a folder containing a required `SKILL.md` and optional supporting files. See the [official OpenAI customization documentation](https://learn.chatgpt.com/docs/customization/overview#skills).

## Usage

This skill is intentionally configured for explicit invocation:

```text
Use $find-code-simplifications to investigate the current branch.
```

You can also narrow or broaden the scope:

```text
Use $find-code-simplifications to investigate this module.
```

```text
Use $find-code-simplifications to investigate the entire repository.
```

The investigation is read-only by default. Ask separately if you want selected findings implemented.

## What it reports

For each strong candidate, the skill reports its location, consumer evidence, current cost, proposed simplification, expected net benefit, behavior or contract impact, risk, confidence, and focused verification steps. It also records representative rejected candidates and the status of checks performed.

## Repository structure

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── README.md
└── README_ZH.md
```

`agents/openai.yaml` disables implicit invocation so the skill runs only when explicitly requested.

## Origin

This skill was adapted from a DeepSeek Harness-oriented code simplification workflow and generalized for use across repositories, languages, and architectures.
