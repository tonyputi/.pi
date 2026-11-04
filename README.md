# A small, opinionated starter for Pi

**Your language in chat. English in the repository. A human in charge of the merge.**

A public GitHub template for [Pi Coding Agent](https://pi.dev): shared working rules and two deliberately chosen extensions, without someone else's credentials, model preferences, or company setup.

[Get started](#get-started) · [Working rules](#working-rules) · [Customize](#make-it-yours) · [Security](#security-and-privacy)

## What you get

| File | Purpose |
| --- | --- |
| [`AGENTS.md`](AGENTS.md) | Shared instructions for communication, implementation, Git delivery, and safety. |
| [`settings.json`](settings.json) | Two pinned Pi packages; no imposed AI provider or model. |
| [`.gitignore`](.gitignore) | An explicit allowlist that keeps runtime files out of Git by default. |

### Two extensions, no kitchen sink

- **[GitHub App Auth](https://github.com/tonyputi/pi-github-app-auth)** — our extension for giving agent-run GitHub commands a separate App identity, without replacing your normal terminal credentials.
- **[Pi Voice](https://github.com/earendil-works/pi-voice)** — the official Pi extension for local speech-to-text: dictate prompts and transcribe audio/video files.

No cloud-provider integration, MCP server, subagent framework, custom router, or personal memory is bundled. Add what your projects actually need.

## Get started

### 1. Install the prerequisites

- **[Pi](https://pi.dev)** — follow its installation guide. For an npm installation, Pi requires Node.js **22.19 or newer**.
- **Git** and **[GitHub CLI](https://cli.github.com)** — for agent-driven branches, issues, and pull requests.
- **[FFmpeg](https://ffmpeg.org/download.html)** — only needed for transcription of existing audio/video files, not a prerequisite for this template itself.

Review the two extensions before loading them: Pi packages execute code with your user's permissions.

### 2. Create your copy

Click **Use this template → Create a new repository** on GitHub, then clone your new repository into a normal working directory.

**Do not clone over an existing `~/.pi/agent` directory, and do not copy your live Pi directory into this repository.** The repository contains the shareable baseline; the agent directory contains your private runtime state.

### 3. Install the configuration

From your cloned repository, copy **only** `AGENTS.md` and `settings.json` into your Pi agent directory.

For a fresh configuration on macOS or Linux:

```bash
mkdir -p ~/.pi/agent
cp -i AGENTS.md settings.json ~/.pi/agent/
```

`cp -i` asks before overwriting an existing file. If either file already exists, decline the overwrite and merge the relevant instructions or package entries manually. Keep your existing providers, packages, and preferences.

On Windows, copy those same two files into `%USERPROFILE%\.pi\agent` using your file manager. If you set `PI_CODING_AGENT_DIR`, use that directory instead on any platform.

There is no installer script and no symlink into your private configuration. Copying the files is the entire installation; later template changes must be copied or merged again.

### 4. Start Pi and connect your accounts

Start Pi from a project directory, not from this template repository:

```bash
cd /path/to/your/project
pi
```

Pi installs the packages declared in `settings.json` on startup. Internet access is needed for their initial download. Use `/login` to connect your own AI provider.

Inside Pi, complete the two local setup steps:

| Command | What it does |
| --- | --- |
| `/github-app-auth setup` | Guides you through creating and installing your own GitHub App. |
| `/github-app-auth status` | Confirms the authentication state before agent GitHub operations. |
| `/voice-settings` | Lets you choose and, after confirmation, download a local speech-to-text model. |

The packages are predeclared, **not preauthenticated**. No template can safely supply your GitHub credentials or select and download a speech model without your involvement.

> **Check GitHub App status before use.** Until configured, the extension is inactive and agent commands may still use your personal credentials. It provides authentication, not PR automation or a security sandbox. See its [setup and security documentation](https://github.com/tonyputi/pi-github-app-auth#setup).

For dictation, use `/voice` or the default **Ctrl+Alt+Z** shortcut. Speech recognition runs locally and needs no cloud speech API key. The resulting text is still sent to your chosen AI provider when you submit it as a prompt.

### 5. Give it a task

For example:

```text
Implement issue #42 and deliver a PR. Follow the project's conventions,
run the relevant checks, and leave the merge to me.
```

The shared instructions guide the agent to work in an isolated worktree, use a branch such as `feat/42/add-search`, and open a focused PR containing `Closes #42`.

## Working rules

The full instructions live in [`AGENTS.md`](AGENTS.md). In brief:

| Area | Default |
| --- | --- |
| Language | Reply in the user's language; write code, documentation, issues, commits, and PRs in English, except explicitly requested localization. |
| Scope | Small, complete changes that reuse project conventions; no speculative abstractions. |
| Issues | Required for non-trivial work, not for small, low-risk edits such as typos. |
| Branches | `{feat\|fix\|hotfix\|docs\|chore}/{issue-number}/{short-title}`; omit the issue segment for trivial work without an issue. |
| Isolation | Prefer Git worktrees inside the project's ignored `.worktrees/` directory. |
| Delivery | Conventional Commits; a delivery request authorizes commits, branch push, and a PR—not a direct push to the default branch. |
| Issue closure | Resolving PRs use `Closes`, not `Refs`; verify the issue is closed after merge. |
| Review | A human reviews and merges, unless the user explicitly asks the agent to perform that merge. |
| Checks and docs | Run relevant existing checks, update affected documentation, and disclose skipped checks or remaining risks. |
| External changes | No unrelated publication, infrastructure operation, deployment, or data deletion without approval. |

GitHub automatically closes linked issues when a resolving PR merges into the repository's **default branch**. A different target branch requires an explicit closure plan. See [GitHub's closing-keyword rules](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue).

These are agent instructions, **not enforced branch protection, CI checks, or background automation**. Post-merge verification happens when the agent next checks the merged PR; this template does not run a watcher.

## Make it yours

- **Personal defaults:** edit your local agent-directory `settings.json` to select providers, models, and display preferences.
- **Project rules:** keep build commands, architecture conventions, and project-specific constraints in that project's `AGENTS.md`. Resolve conflicts with the shared instructions explicitly.
- **Shareable changes:** edit the template files in your repository, review them for secrets, then copy or merge the changes into your agent directory. Run `/reload` in an existing Pi session after changing settings or instructions.
- **More files:** add explicit entries to `.gitignore` for new, reviewed template files. Files are ignored by default on purpose.

There are no separate personal and work profiles. The baseline is shared; organization-specific details stay in local or project configuration.

## Updates and removal

Package versions are pinned in `settings.json`. To upgrade, review the upstream release, update the relevant version, then merge that declaration into your live settings. Restart Pi or run `/reload` to reconcile the configuration. Updating this repository alone does not update previously copied files.

To remove the setup, remove the two package declarations and the shared instructions from your live configuration, preserving unrelated settings. Restart Pi. Removing a package declaration does not revoke its GitHub App installation or erase credentials and downloaded models; manage those separately using the extensions' documentation.

## Security and privacy

**Public baseline in Git; private runtime state outside it.**

Never publish API keys, GitHub App private keys, access tokens, `auth.json`, `pi-github-app-auth.json`, MCP credentials, session history, logs, voice preferences, or company data. Every user supplies their own credentials locally.

The allowlist in `.gitignore` protects against accidental additions of runtime files. It does **not** detect a secret pasted into an allowed file, and `git add -f` bypasses it. Stage explicit files and inspect the staged diff before committing:

```bash
git add README.md AGENTS.md settings.json .gitignore
git diff --cached --check
git diff --cached
```

Do not paste suspected credentials into public issues. If a secret is exposed, revoke or rotate it immediately: deleting the current file does not remove it from Git history.

## Upstream projects

- [Pi Coding Agent and documentation](https://pi.dev)
- [pi-github-app-auth](https://github.com/tonyputi/pi-github-app-auth)
- [Pi Voice](https://github.com/earendil-works/pi-voice)
