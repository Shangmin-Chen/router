---
name: open-source-pr-readiness
description: Verify an open source contribution branch or PR against CONTRIBUTING.md, repo agent docs, CI/test expectations, and maintainer-grade review standards. Use before opening or updating an upstream PR, when asked to run final nits, audit PR cleanliness, check DCO/signoff, branch base, diff scope, PR body, reviewer etiquette, labels, or response to maintainer feedback.
---

# Open Source PR Readiness

Use this skill as a skeptical final reviewer before a contribution reaches upstream maintainers. The goal is not only "does it work?" but "is this easy, safe, and respectful for maintainers to review?"

## Workflow

1. **Load project rules**
   - Read `CONTRIBUTING.md`, `README*`, root agent docs, and package-local agent docs for touched files.
   - Check remotes, current branch, upstream default branch, and fork relationship with `git remote -v` and `git status --short --branch`.
   - Read linked issues, related PRs, and maintainer comments with `gh issue view`, `gh pr view`, and `gh pr diff` when GitHub context matters.

2. **Audit branch hygiene**
   - Confirm the branch is based on current upstream, usually `upstream/main`.
   - Inspect `git log --oneline upstream/main..HEAD`, `git diff --stat upstream/main...HEAD`, and `git diff upstream/main...HEAD`.
   - Remove unrelated local artifacts, generated churn, editor files, agent files, debug prints, secrets, and broad refactors not required by the issue.
   - Check commit convention, DCO/signoff requirements, and whether the project expects one commit or a tidy stack.

3. **Audit implementation quality**
   - Verify the change solves the reported problem with a failing-before/passing-after test, local reproduction, or source-level proof.
   - Confirm tests assert behavior, not implementation tautologies.
   - Check docs and configuration names match the actual shipped behavior.
   - Look for layering violations, magic strings, swallowed errors, logging of secrets, concurrency risks, and public API drift.

4. **Validate locally**
   - Run targeted tests first, then documented full checks from `CONTRIBUTING.md`.
   - Always run `git diff --check`.
   - If a required check cannot run, capture the exact reason and do not pretend it passed.

5. **Prepare the PR**
   - Write a maintainer-friendly body: concise summary, root cause, fix shape, tests run, and `Fixes #...` lines only when the PR should close the issue.
   - Do not assign reviewers, labels, or milestones unless repo norms or permissions make that appropriate.
   - After opening, check CI and mergeability before asking humans for attention.

## Output

Report in this order:

- **Blockers:** issues that should stop PR opening or require a push before review.
- **Nits:** small polish items worth fixing if time allows.
- **Ready:** what is already in good shape.
- **Validation:** exact commands run and results.
- **PR Notes:** body changes, reviewer etiquette, or maintainer-facing caveats.

If there are no blockers, say the branch is ready and name any residual risk plainly.
