# PR-Proof-of-Work

> TDD-driven E2E workflow with real Playwright browser screenshots as PR proof.
> One Issue → One PR → Visual BEFORE/AFTER evidence.

## What is it?

PR-Proof-of-Work is a skill for AI coding agents (OpenClaw, Claude Code, Codex, etc.) that enforces a **test-first, evidence-based** PR workflow:

1. **Pick** an open GitHub issue
2. **Write** a Playwright E2E test — capture a **BEFORE** screenshot of the bug
3. **Fix** the code
4. **Verify** the test passes — capture an **AFTER** screenshot
5. **Submit** a PR with BEFORE/AFTER comparison screenshots embedded in the comment

No more "It works on my machine." Let the screenshots speak.

## Why?

- **"It works" is not proof** — Reviewers shouldn't have to pull and run your code
- **Screenshots > words** — A visual diff is worth 1000 lines of description
- **Reproducible** — Screenshots come from automated tests, not manual captures
- **Regression-safe** — E2E tests guard against future breakage

## Example

| Before (Bug) | After (Fixed) |
|:---:|:---:|
| ![Before](https://github.com/newtontech/Aether/raw/e2e-screenshots/e2e-screenshots/issue-refresh-button/BEFORE-file-tree-before-refresh-1775071501583.png) | ![After](https://github.com/newtontech/Aether/raw/e2e-screenshots/e2e-screenshots/issue-refresh-button/AFTER-file-tree-after-refresh-1775071501788.png) |

Real PR: [newtontech/Aether#15](https://github.com/newtontech/Aether/pull/15)

---

## Install

### 🐾 OpenClaw

```bash
openclaw skills install https://github.com/newtontech/pr-proof-of-work
```

Or manually clone into your workspace skills directory:

```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/newtontech/pr-proof-of-work.git PR-Proof-of-Work
```

### 🤖 Claude Code (as Plugin)

Install as a plugin (recommended — adds `/pr-proof-of-work:tdd-e2e-pr` slash command):

```bash
# In your project directory
claude /install-plugin https://github.com/newtontech/pr-proof-of-work
```

Or test locally without installing:

```bash
claude --plugin-dir /path/to/pr-proof-of-work
```

**Manual install** — add to your project's `.claude/skills/` directory:

```bash
# Project-level skill (available in this project only)
mkdir -p .claude/skills/pr-proof-of-work
cp -r skills/pr-proof-of-work/* .claude/skills/pr-proof-of-work/

# Or personal skill (available across all your projects)
mkdir -p ~/.claude/skills/pr-proof-of-work
cp -r skills/pr-proof-of-work/* ~/.claude/skills/pr-proof-of-work/
```

Once installed, invoke with:

```
/pr-proof-of-work:tdd-e2e-pr
```

Or just describe what you want — Claude will auto-load the skill based on the description in SKILL.md.

### ⚡ Codex (OpenAI)

Add to your project's `.codex/skills/` directory:

```bash
mkdir -p .codex/skills/pr-proof-of-work
cp -r skills/pr-proof-of-work/* .codex/skills/pr-proof-of-work/
```

Codex discovers skills from `.codex/skills/<name>/SKILL.md` automatically. Once installed, reference it in your `AGENTS.md` or simply describe the task — Codex will pick it up based on the skill's description.

**Git submodule** (recommended for version tracking):

```bash
git submodule add https://github.com/newtontech/pr-proof-of-work.git .codex/skills/pr-proof-of-work
```

### 🔧 Other AI Agents

Point your agent to the SKILL.md file:

```
https://raw.githubusercontent.com/newtontech/pr-proof-of-work/main/SKILL.md
```

---

## Repository Structure

```
pr-proof-of-work/
├── .claude-plugin/
│   └── plugin.json                   # Claude Code plugin manifest
├── skills/
│   └── pr-proof-of-work/
│       ├── SKILL.md                   # Main skill instructions
│       ├── assets/
│       │   └── screenshot-reporter.ts # Playwright screenshot utility
│       ├── references/
│       │   └── testing-patterns.md    # E2E testing patterns & pitfalls
│       └── scripts/
│           └── pr-comment-screenshots.sh # Auto-post screenshots as PR comment
├── SKILL.md                           # Root-level (OpenClaw / Codex compatibility)
├── assets/                            # Root-level copies (OpenClaw / Codex)
├── references/
├── scripts/
└── README.md
```

## Quick Start

```bash
# 1. Install Playwright
npx playwright install

# 2. Copy screenshot reporter to your e2e/ directory
cp assets/screenshot-reporter.ts your-project/e2e/

# 3. Pick an issue
gh issue list --repo owner/repo --state open

# 4. Run the workflow (your AI agent handles this)
# → Write test → BEFORE screenshot → Fix → AFTER screenshot → PR with proof
```

## License

MIT
