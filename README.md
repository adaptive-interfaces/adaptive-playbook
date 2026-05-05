# adaptive-playbook

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Markdown Lint](https://github.com/adaptive-interfaces/adaptive-playbook/actions/workflows/md-lint.yml/badge.svg?branch=main)](https://github.com/adaptive-interfaces/adaptive-playbook/actions/workflows/md-lint.yml)
[![Check Links](https://github.com/adaptive-interfaces/adaptive-playbook/actions/workflows/links.yml/badge.svg?branch=main)](https://github.com/adaptive-interfaces/adaptive-playbook/actions/workflows/links.yml)
[![Dependabot](https://img.shields.io/badge/Dependabot-enabled-brightgreen.svg)](https://github.com/adaptive-interfaces/adaptive-playbook/security)

> Operational Implementation of the Adaptive Interfaces Guide

[Adaptive Interfaces](https://github.com/adaptive-interfaces)  
Engineering discipline for configuring agents to produce team-conforming output.

## 1. Purpose

This repository defines the **execution protocol** for configuring agents so their output:

- matches team structure and conventions
- aligns with domain expectations
- passes review without structural correction

This repository is **operational**, not conceptual.

## 2. Position in the Framework

This repository implements the **HOW**.

| Layer    | Repository                         | Role                    |
| -------- | ---------------------------------- | ----------------------- |
| ACS      | adaptive-conformance-specification | behavior discipline     |
| ATD      | adaptive-tool-discovery            | tool capability mapping |
| AO       | adaptive-onboarding                | team conventions        |
| GUIDE    | adaptive-guide                     | conceptual framework    |
| PLAYBOOK | adaptive-playbook                  | **execution protocol**  |

## 3. Scope: Included

### 3.1 Repository Core Artifacts

- `PLAYBOOK.md` - step-by-step execution process
- `QUICKSTART.md` - minimal setup for engineers
- `CHECKLIST.md` - evaluation and PR enforcement
- `ANNOTATIONS.md` - supporting notes
- `patterns/scaffold-new-repo.md` - starting a new project

### 3.2 Repository Function

Defines:

- how to establish priors
- how to load context layers
- how to execute tasks with an agent
- how to evaluate and iterate on output

## 4. Scope: Not Included

- behavioral protocol: see ACS
- tool registries: see ATD
- team context schemas: see AO
- conceptual explanation: see GUIDE
- domain implementations: see example repos

## 5. Minimal Workflow

1. Generate AO context from a repository
2. Review and correct inferred conventions
3. Define domain context (required for correctness)
4. Load:
   - ACS
   - AO config
   - AO context
   - domain context
5. Execute task
6. Evaluate output
7. Update priors and repeat

## 6. Core Principle

Agent output quality is determined by **configuration**, not prompting.

Prompts are task instructions; **priors are the system.**

## 7. Developer

```shell
npx markdownlint-cli2 --fix
```

## 8. Annotations

[ANNOTATIONS.md](./ANNOTATIONS.md)

## 9. Manifest

[MANIFEST.toml](./MANIFEST.toml)

## 10. Citation

[CITATION.cff](./CITATION.cff)

## 11. License

MIT © 2026 [Adaptive Interfaces](https://github.com/adaptive-interfaces)
