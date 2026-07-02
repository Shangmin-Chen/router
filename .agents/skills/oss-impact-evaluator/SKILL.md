---
name: oss-impact-evaluator
description: Evaluate whether an open source issue, PR idea, or codebase area is worth working on for high-impact contribution. Use when prioritizing OSS work, choosing between issues, deciding if a fix is meaningful, estimating maintainer acceptance, judging user impact, avoiding low-value churn, or selecting work that will demonstrate strong engineering judgment.
---

# OSS Impact Evaluator

Use this skill before investing serious time in an OSS contribution. The goal is to choose work that matters: useful to users, aligned with maintainers, scoped for acceptance, and strong enough to be worth the user's attention.

## Evaluate Current Context

- Read the issue, linked discussion, labels, related PRs, recent commits, release notes, and maintainer comments.
- Verify whether the problem still exists on current upstream before scoring.
- Compare against the repo's stated direction in `README*`, `CONTRIBUTING.md`, roadmap docs, and active PRs.
- Prefer primary evidence over vibes: failing tests, reproduction steps, repeated user reports, code paths, or maintainer requests.

## Scorecard

Score each dimension from 0 to 3:

- **User Impact:** how many users or important workflows benefit.
- **Severity:** correctness, security, data loss, reliability, cost, or sharp contributor friction.
- **Maintainer Signal:** labels, comments, recency, roadmap alignment, or repeated issue reports.
- **Acceptance Odds:** clear scope, low controversy, good test path, and fit with architecture.
- **Leverage:** small/medium PR with large cleanup, extensibility, or bug-prevention value.
- **Learning/Portfolio:** demonstrates judgment, architecture fit, tests, and communication.

Interpretation:

- 14-18: high-impact, pursue now.
- 9-13: maybe, verify more or narrow scope.
- 0-8: low-impact or risky, skip for now.

## Red Flags

- The issue is vague and cannot be reproduced.
- The solution requires a broad rewrite, product decision, or maintainer architecture choice first.
- Another active PR already covers the same ground.
- The change is mostly style, naming, formatting, generated churn, or personal preference.
- The PR would touch many unrelated packages without a crisp behavioral payoff.
- The repo's contribution guide or maintainers signal that this area is out of scope.

## Output

Give a direct decision:

- **Verdict:** pursue, investigate first, or skip.
- **Score:** total and per-dimension scores.
- **Why:** the strongest evidence for or against impact.
- **Best PR Angle:** the smallest contribution shape that preserves impact.
- **First Verification Step:** the next command, test, issue check, or reproduction to run.
- **Stop Conditions:** what evidence would make the user abandon the idea.

When comparing multiple options, rank them and recommend exactly one next move.
