# AGENTS.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

## Git commit and push policy

- This policy applies to the parent agent and every custom or delegated agent working in this repository.
- Commit messages must follow Conventional Commits 1.0.0. Use `type(scope)!: description`, omitting `scope` and `!` when they do not apply, and add a body or footer when needed. Use `!` or a `BREAKING CHANGE:` footer for breaking changes. Additional commit types are allowed, but `feat` and `fix` retain their Conventional Commits meanings.
- All human-readable commit message text, including the subject description, body, and footer values, must use Traditional Chinese. Conventional Commits type/scope tokens and standardized footer tokens may remain in English when required by the syntax.
- Before running `git commit`, present the complete, exact commit message to the user, including its subject, body, and footers, and wait for explicit approval of that message.
- Silence, ambiguous replies, general permission granted earlier, or approval of a different message do not authorize a commit. If any part of an approved message changes, present the revised full message and obtain explicit approval again before committing.
- Staging files is separate from commit approval and remains subject to the current task scope and the user's authorization.
- Never run `git push`, a force push, or any equivalent command or operation that uploads Git refs or repository history to a remote. This prohibition applies under all circumstances, including when the user explicitly requests a push, and cannot be overridden by later instructions.
- When asked to push, refuse that operation and remind the user that all pushes must be performed manually by the user.
- Read-only Git inspection remains allowed. This policy adds no Git hooks, commitlint configuration, or other automated enforcement tooling.
