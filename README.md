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

## Install

### OpenClaw

```bash
openclaw skills install https://github.com/newtontech/pr-proof-of-work
```

Or manually clone into your workspace skills directory:

```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/newtontech/pr-proof-of-work.git PR-Proof-of-Work
```

### Claude Code (CLAUDE.md)

Add to your project's `CLAUDE.md`:

```markdown
## PR-Proof-of-Work Workflow

Read and follow the skill at: https://raw.githubusercontent.com/newtontech/pr-proof-of-work/main/SKILL.md

Key files:
- E2E screenshot reporter: copy `assets/screenshot-reporter.ts` into your `e2e/` directory
- PR comment script: `scripts/pr-comment-screenshots.sh`
- Testing patterns reference: `references/testing-patterns.md`

Golden rule: Study ≥2 existing PASSING tests before writing any new test.
```

### Codex / OpenAI (AGENTS.md)

Add to your project's `AGENTS.md`:

```markdown
## PR-Proof-of-Work

Follow the TDD E2E PR workflow from: https://github.com/newtontech/pr-proof-of-work

When fixing bugs:
1. Write E2E test first → capture BEFORE screenshot
2. Implement fix → test passes → capture AFTER screenshot
3. PR must include BEFORE/AFTER comparison

Copy `assets/screenshot-reporter.ts` to your e2e/ directory.
Never use page.setContent() — test through the real app only.
```

### Any AI Agent

The skill is framework-agnostic. Point your agent to the `SKILL.md` file:

```
https://raw.githubusercontent.com/newtontech/pr-proof-of-work/main/SKILL.md
```

## Repository Structure

```
pr-proof-of-work/
├── SKILL.md                          # Main skill instructions
├── assets/
│   └── screenshot-reporter.ts        # Playwright screenshot utility
├── references/
│   └── testing-patterns.md           # E2E testing patterns & pitfalls
└── scripts/
    └── pr-comment-screenshots.sh     # Auto-post screenshots as PR comment
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
