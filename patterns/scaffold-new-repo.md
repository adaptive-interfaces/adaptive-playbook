# scaffold-new-repo.md

How to scaffold a new repo using ACS conformance and a
MANIFEST.toml conventions pointer.

## How it works

Each repo declares its conventions source in `MANIFEST.toml`:

```toml
[conventions]
source = "https://github.com/ORG/CONVENTIONS-REPO"
```

That pointer is all an agent needs. The rest is ACS.

## Manual Initialization Sequence

### Commit 1. Add Founding Documents

- `.gitignore`
- `DECISIONS.md` - founding design rationale; first artifact, before any code
- `LICENSE`
- `MANIFEST.toml` - fully configured before any scaffolding
- `README.md`

In the GH Repo (as needed):

- Settings / Pages / Source = GitHub Actions
- Settings / Advanced Security / Grouped security updates / Enable
- Settings / Turn off Wiki
- Settings / Turn off Projects

### Commit 2. Add Agent Instructions

`AGENTS.md` - include formatting conventions, tool requirements, and domain-specific rules.

`AGENT_CONDUCT.md` - (optional) behavior preferences.

`CLAUDE.md` - minimal, points at other documents:

```markdown
# CLAUDE.md (repo-name)

Read these files in order before generating any artifact:

1. [`MANIFEST.toml`](./MANIFEST.toml) - repository contract and agent configuration
2. [`SKILL.md`](./SKILL.md) - operating guide and interface contract
3. [`DECISIONS.md`](./DECISIONS.md) - design rationale
4. [`AGENTS.md`](./AGENTS.md) - workflow requirements
5. [`AGENT_CONDUCT.md`](./AGENT_CONDUCT.md) - behavioral constraints

```

See `adaptive-playbook` for the full behavioral constraint pattern.

### Commit 3. Agent Scaffold from Manifest

Provide the agent with the repo URL.
The repo must have a fully configured MANIFEST.toml and all files from commits 1 and 2.

Example prompt:

```text
Scaffold https://github.com/ORG/REPO.

Use the target repository's MANIFEST.toml as authoritative for the target repo's
identity, package/module names, CLI names, dependencies, docs settings, CI
settings, validation commands, release metadata, and generated artifact names.

Important:
- The target repo is available the link bove.
- The [conventions].source value in MANIFEST.toml points to the conventions
  source repo.
- The conventions source repo is a worked example and conformance source, not
  the target identity.
- Do not copy the conventions source repo's identity into the target repo.
- Do not write directly into the target repository.
- Generate a separate named scaffold folder only.
- The user will manually review the generated scaffold and decide what to copy.
- Do not move on to project-specific logic yet - this is just Commit 3 in 
  the scaffolding process to learn to code like a team member.

Process:
1. Read the target repo's MANIFEST.toml and agent guidance files.
2. Read [conventions].source from MANIFEST.toml.
3. Clone/read the conventions source repo.
4. Discover the scaffold by inspecting the conventions source:
   - repository layout
   - convention files
   - docs configuration
   - CI workflows
   - package configuration
   - source layout
   - tests
   - validation commands
   - naming patterns
   - formatting and comment conventions
5. Classify discovered files into:
   - repo-independent convention files to copy verbatim
   - identity-bearing files to adapt to the target manifest
   - project-specific files that require fresh target stubs
6. Generate the target scaffold in a separate folder named:

   ptat-monitor-commit-3-scaffold

Do not rely on a hard-coded list of files. 
Discover what belongs in the scaffold
from the conventions source and the target manifest.

Before packaging:
- Search generated files for accidental conventions-source identity leakage.
- Verify that identity-bearing files consistently use the target repo identity.
- Run available local checks when possible.
- Do not push, commit, overwrite, or modify the target repository.

Package the scaffold folder as output.zip from the parent directory:

zip -r output.zip ptat-monitor-commit-3-scaffold

The zip must extract to a named review folder, not directly into the repository
root. The user decides what, if anything, to copy into the actual repo.
```

Extract with:

```shell
# Windows
Expand-Archive -Path output.zip -DestinationPath .\REPO\ -Force

# Mac/Linux
unzip output.zip -d ./REPO/
```

### Commit 4. Add Project-Specific Logic

This is typically greenfield:

- Write or generate `src/<package>/` implementation files
- Write or generate `tests/` against the interface
- Update `CHANGELOG.md` `[Unreleased]` with what was added

### Commit 5. Author Agent Operating Guide

- `SKILL.md` - written after interface is stable; evolves with it

### Commit 5 (or after). Branch Protection

Settings / Branches / Add branch protection rule:

- Branch name pattern: `main`
- Require status checks to pass before merging
- Add your CI job name from the Actions tab after first CI run

## Agent Initialization Process

```text
1. Read MANIFEST.toml → find [agent].conformance and [conventions].source
2. Read AGENTS.md and CLAUDE.md → load formatting and behavioral constraints
3. git clone [conventions].source
4. Observe: read all convention files
5. Infer: what changes for this repo's identity, org, package name, CI steps
6. Conform: generate every file against observed patterns
```

## What gets copied verbatim

Examples of convention files that do not change across repos:

```text
.editorconfig
.gitattributes
.markdownlint.yml
.github/.yamllint.yml
.github/dependabot.yml      (if [ci].dependabot = true)
.github/lychee.toml         (if [ci].link_check = true)
.github/workflows/links.yml (if [ci].link_check = true)
.github/workflows/deploy-zensical.yml  (if [docs].deploy = true)
shape.ps1
```

## What gets adapted

Examples of files that change per repo, derived from MANIFEST.toml fields:

```text
pyproject.toml          [package].python_name, cli, dependencies
CITATION.cff            [repo] identity, title, abstract, keywords
CHANGELOG.md            [release].validate_step, org/name URLs
README.md               repo-specific description
zensical.toml           [repo].org, [repo].name, [docs] config
.pre-commit-config.yaml remove conventions-source-specific hooks; keep shared hooks
ci-python-zensical.yml  E1 step uses [release].validate_step
```

## What gets authored fresh

Examples of files that cannot be derived from conventions source:

```text
DECISIONS.md            founding design rationale (first artifact, before code)
SKILL.md                agent operating guide (after interface is stable)
src/<package>/          implementation files
tests/                  test suite
```

## Troubleshooting

If pre-commit is installed but no config exists yet:

```shell
# PowerShell
$env:PRE_COMMIT_ALLOW_NO_CONFIG=1

# bash
PRE_COMMIT_ALLOW_NO_CONFIG=1 git commit -m "..."
```

## Related

- `adaptive-conformance-specification` - ACS behavioral protocol
- `adaptive-onboarding` - team context loading
- Your workspace `SCAFFOLD.md` - org-specific instance of this pattern
