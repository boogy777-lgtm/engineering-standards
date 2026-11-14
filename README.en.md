# Engineering Development Standards

[![Русский](https://img.shields.io/badge/Documentation-Русский-2374C8?style=for-the-badge)](README.md) [![English](https://img.shields.io/badge/Documentation-English-555555?style=for-the-badge)](README.en.md) [![中文](https://img.shields.io/badge/Documentation-简体中文-D97706?style=for-the-badge)](README.zh-CN.md)

English-language overview of [asckye/engineering-standards](https://github.com/asckye/engineering-standards). The original Chinese documentation is preserved in [README.zh-CN.md](README.zh-CN.md). The complete rules have **not** yet been translated into English.

This repository provides engineering development standards packaged as [Agent Skills](https://agentskills.io). Each rule has an identifier and an obligation level. The skills guide AI coding agents and can also be read as engineering documentation.

## Skills

| Scope | Skill | Status |
|---|---|---|
| All projects | [general-engineering-standard](skills/general-engineering-standard/SKILL.md) | 3.0 |
| MCP servers | [mcp-server-standard](skills/mcp-server-standard/SKILL.md) | Draft 0.2 |
| Industrial HMI | [hmi-standard](skills/hmi-standard/SKILL.md) | 3.0 |
| Machine vision | [machine-vision-standard](skills/machine-vision-standard/SKILL.md) | Draft 0.2 |
| Dashboards | [dashboard-standard](skills/dashboard-standard/SKILL.md) | Draft 0.2 |
| Desktop apps | [desktop-app-standard](skills/desktop-app-standard/SKILL.md) | 3.0 |
| Web apps | [web-app-standard](skills/web-app-standard/SKILL.md) | 3.0 |
| Mobile apps | [mobile-app-standard](skills/mobile-app-standard/SKILL.md) | 3.0 |

The general standard applies to every project. The author states that the standards have not yet undergone independent review or empirical validation.

## Installation

For Claude Code:

```bash
claude plugin marketplace add asckye/engineering-standards
claude plugin install engineering-standards@asckye-standards
```

Other Agent Skills-compatible clients can copy the required folders from `skills/` to their skill directories. Copying all eight folders together preserves cross-links.

## How the standards work

Each `SKILL.md` is a compact entry point. Detailed rules are stored in `references/` and templates in `assets/`. Agent instructions alone cannot enforce compliance; automate verifiable requirements in CI.

For local validation:

```bash
python build-tools/check_standards.py
python -m unittest discover -s build-tools
```

Evaluation scenarios are in `evals/` and may be run with Claude Code:

```bash
claude plugin eval . --allow-tools Write --no-publish
```

See the [Russian README](README.md) or the [original Chinese README](README.zh-CN.md) for adoption steps, versioning, and the roadmap.

## License and attribution

Copyright © 2026 asckye. Documentation, skills, and evaluation cases: [CC BY 4.0](LICENSE). Scripts under `build-tools/`: [MIT](build-tools/LICENSE).

Adapted from “工程开发规范” by asckye, [source repository](https://github.com/asckye/engineering-standards). This is an English overview; the original rules are unchanged.
