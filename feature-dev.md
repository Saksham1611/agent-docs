---
name: feature-dev
description: "End-to-end feature development workflow. Guides through discovery, codebase exploration, clarifying questions, architecture design, implementation, and quality review. Use when the user asks to build, add, or implement a feature."
---

## Overview

A 7-phase workflow for building features correctly: understand first, design before coding, review after building. Each phase gates the next — do not skip ahead.

---

## Phase 1 — Discovery

**Goal:** Understand exactly what needs to be built before touching any code.

- Restate the feature request in your own words and confirm understanding
- Identify: the problem being solved, who it affects, and any stated constraints
- If the request is vague, ask focused questions — one round only, no more than 5 questions
- Produce a 2-3 sentence "scope statement" and get explicit confirmation before proceeding

> Do not explore the codebase yet. Discovery is about the requirement, not the implementation.

---

## Phase 2 — Codebase Exploration

**Goal:** Build deep understanding of the relevant existing code before designing anything.

Launch **2–3 `code-explorer` agents in parallel**, each with a distinct focus:

| Agent focus | Example prompt |
|-------------|---------------|
| Similar features | "Find features similar to [feature] and trace their full implementation" |
| Architecture & layers | "Map the module boundaries, abstractions, and data flow for [area]" |
| Integration points | "Identify all entry points, dependencies, and side effects touching [area]" |

After agents return:
- Read every key file they identify
- Summarize findings: patterns found, conventions used, files that will be affected
- Present this summary to the user before moving on

---

## Phase 3 — Clarifying Questions

**Goal:** Resolve all ambiguities surfaced by exploration before designing.

**First — simulate a stakeholder discussion** (see @global_workflows/simulate-discussion.md):
Select 2–3 domain-relevant personas for this feature (e.g. "Backend Engineer", "Frontend Lead", "Security Specialist", "Product Manager"). Have them debate the requirement and codebase findings — they should actively disagree on trade-offs. Use the insights from this discussion to build the question list below.

Then, review the scope statement (Phase 1) against the codebase findings (Phase 2) and identify gaps:

- Edge cases not covered by the requirement
- Error handling and failure modes
- Integration points that need decisions (e.g. async vs sync, new table vs existing)
- Backward compatibility concerns
- Performance or security constraints

Present all questions in a single numbered list. **Wait for answers before proceeding.**

---

## Phase 4 — Architecture Design

**Goal:** Design the implementation approach with full codebase context.

Launch **2–3 `code-architect` agents**, each given a different design constraint:

| Agent focus | Constraint |
|-------------|-----------|
| Minimal footprint | Smallest change, maximum reuse of existing code |
| Clean design | Clearest abstractions, most maintainable long-term |
| Pragmatic balance | Reasonable trade-off between speed and quality |

After agents return:
- Review all approaches
- Form a clear recommendation with rationale
- Present the comparison and recommendation to the user
- **Ask which approach to use and wait for explicit approval before implementing**

---

## Phase 5 — Implementation

**Goal:** Build the feature following the approved architecture.

> **Gate:** Do not start until the user has approved an approach from Phase 4.

- Re-read all files identified in Phases 2–4 before writing any code
- Follow the patterns and conventions discovered in Phase 2 strictly
- Use `TodoWrite` to track progress; mark tasks complete as you go
- Keep changes scoped — do not refactor unrelated code
- After each logical unit of work, confirm it compiles / passes basic checks

---

## Phase 6 — Quality Review

**Goal:** Catch bugs, quality issues, and convention violations before the work is done.

Launch **3 `code-reviewer` agents in parallel**, each with a different lens:

| Agent focus | What to find |
|-------------|-------------|
| Simplicity & DRY | Duplication, unnecessary complexity, dead code |
| Bugs & correctness | Logic errors, unhandled edge cases, off-by-ones |
| Conventions & security | Project standards, CLAUDE.md compliance, injection risks |

After agents return:
- Consolidate findings, grouped by severity (High / Medium / Low)
- Present to the user and ask: **Fix now / Fix later / Proceed as-is**
- Address all High items before marking the feature complete

---

## Phase 7 — Summary

**Goal:** Close out the work with a clear record of what was done.

Produce a summary covering:
- What was built (2–3 sentences)
- Key architectural decisions made and why
- All files created or modified (with paths)
- Suggested next steps (tests to add, follow-up features, docs to update)

Mark all todos complete.

---

## Sub-agents

These agents are launched via the Task tool at the phases indicated.
Their full definitions live in the same `global_workflows/` directory — load them when invoking.

| Agent | File | Invoked in |
|-------|------|------------|
| `code-explorer` | @global_workflows/code-explorer.md | Phase 2 |
| `code-architect` | @global_workflows/code-architect.md | Phase 4 |
| `code-reviewer` | @global_workflows/code-reviewer.md | Phase 6 |
