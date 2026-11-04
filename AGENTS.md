# Shared agent instructions

## Communication and artifacts

- Respond in the user's language. Write generated code, comments, documentation, commit messages, issues, PRs, and other artifacts in English unless the task explicitly requires another language.
- Keep answers concise. Ask one question at a time when clarification is needed.

## Implementation

- Read applicable project instructions and relevant existing code before editing. Reuse established conventions and installed tools; prefer the smallest complete change.
- Keep changes scoped to the task. Update affected callers, tests, and existing documentation together. Create new documents only when necessary; document the current behavior rather than delivery history.
- Run relevant existing checks. State what was not checked and any remaining risk; never claim unperformed verification.

## Git workflow

- Check the repository, current branch, and working-tree status before changing files. Preserve unrelated work.
- Prefer an isolated Git worktree under `.worktrees/` in the repository root. Ensure that directory is ignored before creating it; never switch or discard someone else's work.
- Require an issue for non-trivial work. Small, low-risk edits such as typo fixes do not require one.
- Name new branches `{type}/{issue-number}/{short-title}`, where type is `feat`, `fix`, `hotfix`, `docs`, or `chore`, using a short kebab-case title. For trivial work without an issue, use `{type}/{short-title}`. Ask for a missing issue when required; never invent one.
- Keep one short-lived branch and one focused PR per concern, linked to its issue when applicable. Use Conventional Commits.
- Include `Closes #<issue-number>` in each resolving PR body, not `Refs`. For another repository, use `Closes owner/repository#<issue-number>`.
- Target the repository's default branch for automatic GitHub issue closure. If a different target is required, clarify the closure workflow before opening the PR.
- Do not claim an issue is resolved by a partial implementation. Split or clarify the scope instead of replacing `Closes` with `Refs`.
- After a PR merges, verify that its resolved GitHub issues are closed. If automatic closure failed, report it and ask before closing them manually.
- When asked to complete and deliver a task, commit, push the working branch, and open its PR without asking for approval at every step. Do not push directly to the default branch.
- Leave PR review and merge to a human. Do not merge PRs unless the user explicitly asks you to perform that merge.
- Force-pushes and destructive Git operations require explicit approval.

## Security and external actions

- Never commit credentials, private keys, tokens, authentication files, session histories, personal data, or confidential company content. Never print secrets in logs or tool output.
- Use placeholders in public examples. Stage explicit files and review the staged diff before committing; an ignore file is not a secret scanner.
- Ask for approval before publishing content or making external changes unless the user has already authorized the specific action. A request to complete and deliver a coding task authorizes the commits, branch push, and PR described above, not unrelated external actions.
- Infrastructure changes, deployments, and data deletion require explicit scope and approval. Editing code does not authorize applying or deploying it.
