# Adaptive Playbook

> Operational Implementation of the Adaptive Interfaces Guide

## 1. Purpose

This playbook defines the **exact process engineers follow**
to configure an agent so that it produces output that
conforms to team conventions, structure, and domain expectations.
It offers a **repeatable execution protocol**.

## 2. Core Principle

Agent output quality is determined by **context configuration**, not model capability.

Correct setup produces:

- code that matches team structure
- tests aligned with domain expectations
- minimal PR correction

Incorrect setup produces:

- technically correct but misaligned output
- repeated review friction
- inconsistent results across sessions

## 3. Required Layers

Agents must be configured with the following layers **in order**:

1. **ACS**: behavior discipline
2. **ATD**: tool capability mapping (if applicable)
3. **AO Config**: declared team conventions
4. **AO Context**: observed repository patterns
5. **Domain Context**: definition of correctness

## 4. Required Artifacts

### 4.1. AO Config (declared conventions)

```text
.agent/ao-config.toml
.agent/ao-config-*.toml
```

Defines:

- structure expectations
- naming conventions
- config patterns
- definition of done
- team norms

### 4.2. AO Context (observed patterns)

```text
.agent/ao-context.toml
.agent/ao-context-*.toml
```

Generated from repository evidence.

Must include:

- inferred conventions
- divergences
- gaps

### 4.3. Domain Context (required for correctness)

```text
.agent/ao-domain.toml
```

Defines:

- what “correct” means in this problem space
- expected ranges
- anomaly definitions
- domain-specific constraints

Without this, output may be well-structured but incorrect.

### 4.4. Tool Registry (optional)

```text
.agent/tools/*.toml
```

Only required when tools are non-trivial.

## 5. Setup Process

### 5.1 Step 1. Load ACS

Agent must:

- observe before acting
- infer from evidence
- stop when evidence is insufficient
- not guess

No output is generated at this step.

### 5.2 Step 2. Generate AO Context

Run onboarding against the repository:

- scan structure
- inspect representative files
- identify patterns

Produce:

```text
.agent/ao-context.toml
```

### 5.3 Step 3. Review AO Context

Engineer must:

- verify inferred conventions
- correct incorrect assumptions
- ensure divergences are recorded
- fill gaps where evidence is missing

### 5.4 Step 4. Define Domain Context

Engineer creates:

```text
.agent/ao-domain.toml
```

Must define:

- anomaly definitions
- expected behavior
- tolerance thresholds
- correctness criteria

This is mandatory for domain-driven work.

### 5.5 Step 5. Confirm Priors

Mark entries:

- `confirmed = true` → stable, authoritative
- `confirmed = false` → must be validated against repo evidence

### 5.6 Step 6. Execute Task

Agent is invoked with:

1. ACS
2. AO Config
3. AO Context
4. Domain Context
5. Task prompt

## 6. Execution Rules

Agent must:

- follow repository structure exactly
- use config-driven values (no inline constants)
- conform to naming and layout conventions
- align logic with domain definitions
- stop if required information is missing

## 7. Definition of Done

Output is acceptable only if:

- structure matches repository conventions
- no structural refactoring is required in PR
- configuration is used correctly
- domain expectations are satisfied
- tests reflect correct behavior
- CI would pass without modification

## 8. Evaluation Checklist

After generation, verify:

- naming matches conventions
- file placement matches structure
- functions match expected size/complexity
- constants are not inlined
- configuration is used appropriately
- domain logic is correct
- output requires no interpretation to resolve ambiguity

## 9. Iteration Process

If output fails:

1. Identify failure category:
   - structure
   - conventions
   - domain correctness
   - missing information

2. Update:
   - AO config (rules)
   - AO context (inference)
   - domain context (definitions)

3. Re-run task

Improvement must be immediate and traceable.

## 10. Failure Modes

Common causes of poor output:

- missing domain context
- weak or incomplete AO context
- excessive or vague rules
- duplication of lint/formatter concerns
- agent guessing due to insufficient evidence
- reliance on prompt instead of priors

## 11. Non-Goals

This playbook does not:

- define formatter or lint rules
- replace engineering judgment
- eliminate review
- act as a prompt engineering guide

## 12. What This Enables

When correctly applied:

- agent output matches team code patterns
- PR friction is reduced
- test generation aligns with domain expectations
- agents behave like consistent team members

## 13. Summary

To produce team-conforming output:

- define priors explicitly
- separate behavior, tools, conventions, and domain
- load context before execution
- evaluate output against team standards
- iterate on priors, not prompts

The agent is not the system;
**the configuration is the system.**
