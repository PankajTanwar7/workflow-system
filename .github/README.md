# GitHub Configuration

## Workflows

This repository includes two optimized GitHub Actions workflows for Claude integration:

### claude.yml - Interactive @claude Bot
- **Purpose:** Responds to @claude mentions in issues and PRs
- **Triggers:** Issue comments, PR comments, reviews, new issues with @claude
- **Features:**
  - 30-minute timeout protection
  - Concurrency control to prevent abuse
  - Failure notifications
  - Full git history access
  - Optional review-only mode (commented out by default)

### claude-code-review.yml - Automatic PR Reviews
- **Purpose:** Automatically reviews pull requests
- **Triggers:** PR opened or synchronized (with smart path filtering)
- **Features:**
  - PR size checking (skips PRs >50 files or >2000 lines)
  - Smart file filtering (excludes lock files, minified files)
  - Structured review template with severity levels
  - Failure notifications
  - Full code analysis tools (Read, Glob, Grep)

**See `.github/workflows/` for the actual workflow files.**

---

## Issue Templates

This repository uses custom issue templates for Feature Requests and Bug Reports.

**Important:** These templates are designed for **Claude Code CLI** workflow, NOT GitHub web integrations.

### How to Use

1. **Create Issue** using the template (Feature Request or Bug Report)
2. **DO NOT** tag `@claude` or any automation tools in the issue
3. **Run start script** to begin work: `./scripts/start-work.sh {issue-number}`
4. **Work with Claude Code** in your terminal
5. **Progress will be posted** to the issue automatically via scripts

### Why No @claude Tags?

- `@claude` mentions trigger GitHub's web integration
- This conflicts with our Claude Code CLI workflow
- We want manual control over when implementation starts
- Our automation handles posting updates to issues

### Templates Available

- **feature_request.md** - For new features
- **bug_report.md** - For bug fixes

Both templates guide you through the process without triggering unwanted automations.

---

## Configuration Files

- **claude.yml** - Interactive @claude bot with safety features
- **claude-code-review.yml** - Automatic PR reviews with size limits
- **ISSUE_TEMPLATE/** - Custom issue templates

---

For complete workflow documentation, see:
- `.claude/WORKFLOW.md` - Single source of truth
- `GITHUB-CLAUDE-SETUP.md` - Setup instructions
