---
name: technical-debt-impact-hunter
description: Find substantial technical debt in a codebase worth fixing, not style nits. Use when asked to audit for technical debt, find high-leverage OSS PR opportunities, identify brittle architecture, duplicated logic, missing tests, flaky behavior, layering violations, stale configuration, hidden correctness risks, or codebase cleanup that can create meaningful maintainer and user impact.
---

# Technical Debt Impact Hunter

Use this skill to find debt that deserves a real PR. Prefer concrete, reachable, testable problems over speculative rewrites or aesthetic cleanup.

## Search Strategy

1. **Understand the system shape**
   - Read `README*`, `CONTRIBUTING.md`, root agent docs, package-local docs, and architecture notes before judging code.
   - Identify critical paths: request handling, auth, persistence, provider integrations, config, migrations, CLI/install flows, and test infrastructure.
   - Use `git log --stat`, recent issues/PRs, and TODO/FIXME searches to find areas maintainers already touch.

2. **Look for substantial debt signals**
   - Repeated logic across three or more places with inconsistent behavior.
   - Missing tests around behavior that is user-visible, security-sensitive, billing/cost-sensitive, or provider-dependent.
   - Layering violations, concrete adapter leakage, hidden I/O in pure packages, or duplicated wiring outside the composition root.
   - Silent fallbacks, swallowed errors, ambiguous config names, stale docs, stale generated artifacts, and drift between providers.
   - Flaky or skipped tests, race-prone state, global mutable singletons, unbounded retries, missing cancellation, and poor timeout behavior.

3. **Filter hard**
   - Ignore style-only renames, broad modernization, formatting churn, dependency bumps without a bug, and speculative performance work without evidence.
   - Favor fixes that can be reviewed in one coherent PR, proven by tests, and explained in a short maintainer-facing rationale.
   - Check open issues and PRs before recommending work so the user does not duplicate ongoing maintainer effort.

## Evidence Standard

Do not call something high-impact unless at least two are true:

- A real user flow, public API, documented behavior, or common contributor workflow is affected.
- The issue appears in multiple files, packages, providers, or tests.
- Existing tests miss a meaningful regression.
- Maintainers recently touched or discussed the area.
- The fix reduces future bug surface or makes a known feature easier to extend.

## Output

Produce a ranked list. For each candidate include:

- **Debt:** the concrete problem.
- **Evidence:** files, commands, issue links, or code paths that prove it exists.
- **Impact:** who benefits and what risk or friction is reduced.
- **PR Shape:** the smallest coherent fix.
- **Validation:** the test or reproduction that would prove the fix.
- **Risk:** why this might be rejected or too broad.

End with one recommended first PR candidate and the first verification step.
