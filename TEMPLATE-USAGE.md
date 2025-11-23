# 🎯 How to Use This Workflow Template

**This repository is a complete, production-ready workflow template for development with Claude Code and GitHub @claude integration.**

---

## 📋 What You Get

This template includes:

✅ **Complete Development Workflow**
- Specification → Review → Implementation → PR → Merge → Cleanup
- @claude for reviews, ClaudeCode for implementation
- Automated progress tracking and commenting

✅ **GitHub Integration**
- @claude bot for spec and PR reviews (review-only mode)
- Automatic code review on PR creation
- Issue templates for bugs and features

✅ **Automation System**
- Git hooks for tracking commits
- ClaudeCode hooks for capturing prompts
- Scripts for starting work and cleanup

✅ **Documentation**
- Single source of truth workflow
- Automation FAQ and guides
- Setup instructions

---

## 🚀 Quick Start (5 Minutes)

### Step 1: Use This Template

**On GitHub:**
```
1. Click "Use this template" button
2. Create your new repository
3. Clone to your machine
```

**Or clone directly:**
```bash
git clone https://github.com/YOUR_USERNAME/workflow-system.git my-new-project
cd my-new-project
rm -rf .git
git init
git remote add origin YOUR_NEW_REPO_URL
```

---

### Step 2: Customize for Your Project

**Update these placeholders in key files:**

#### **1. CLAUDE.md** (Required)

```bash
# Replace these placeholders:
{YOUR_REPO_NAME} → your-project-name
{YOUR_PROJECT_DESCRIPTION} → Brief description
{YOUR_PROJECT_TYPE} → Project type (e.g., "REST API (Python + Flask)")
{YOUR_TEST_COMMAND} → Your test command (e.g., "pytest" or "npm test")
```

**Find and replace:**
```bash
cd my-new-project
sed -i 's/{YOUR_REPO_NAME}/my-awesome-api/g' CLAUDE.md
sed -i 's/{YOUR_PROJECT_DESCRIPTION}/User Management API/g' CLAUDE.md
sed -i 's/{YOUR_PROJECT_TYPE}/REST API (Node.js + Express)/g' CLAUDE.md
sed -i 's/{YOUR_TEST_COMMAND}/npm test/g' CLAUDE.md
```

#### **2. .claude/WORKFLOW.md** (Required)

```bash
# Update Quick Reference section (lines 6-12)
sed -i 's/{YOUR_PROJECT_NAME}/My Project Name/g' .claude/WORKFLOW.md
sed -i 's/{YOUR_TEST_COMMAND}/npm test/g' .claude/WORKFLOW.md
```

**Manually edit these sections:**
- Line 8: Current Project name
- Line 11: Test command
- Section: "Project Overview" (if you added one)

#### **3. README.md** (Optional)

Update with your project's description, setup instructions, and usage.

---

### Step 3: Set Up GitHub @claude Bot

**Follow the complete guide:** `GITHUB-CLAUDE-SETUP.md`

**Quick version:**

```bash
# 1. Get your Claude OAuth token
cat ~/.claude/.credentials.json | grep accessToken

# 2. Add to GitHub repository secrets
gh secret set CLAUDE_CODE_OAUTH_TOKEN
# Paste your token when prompted

# 3. Verify
gh secret list
# Should show: CLAUDE_CODE_OAUTH_TOKEN

# 4. Enable GitHub Actions
# Go to: https://github.com/YOUR_USERNAME/YOUR_REPO/actions
# Click "I understand my workflows, go ahead and enable them"
```

---

### Step 4: Test the Workflow

**Create a test issue:**

```bash
gh issue create --title "[TEST] Add hello world endpoint" --body "@claude Please review this feature specification:

## Feature: Hello World Endpoint

**Endpoint:** GET /api/hello

**Response:**
\`\`\`json
{
  \"message\": \"Hello, World!\"
}
\`\`\`

**Acceptance Criteria:**
- Returns 200 status
- Returns JSON with message field
- Works when deployed
"
```

**@claude should respond in 30-60 seconds!** ✅

---

## 📖 Complete Setup Guide

### A. Project Customization Checklist

- [ ] **CLAUDE.md** - Replace all `{YOUR_*}` placeholders
- [ ] **.claude/WORKFLOW.md** - Update Quick Reference section
- [ ] **README.md** - Write your project description
- [ ] **.gitignore** - Add project-specific ignore patterns
- [ ] **package.json / pyproject.toml / Cargo.toml** - Your project config
- [ ] **Issue templates** (.github/ISSUE_TEMPLATE/) - Customize if needed

### B. GitHub Integration Checklist

- [ ] Get Claude OAuth token from `~/.claude/.credentials.json`
- [ ] Add `CLAUDE_CODE_OAUTH_TOKEN` secret to GitHub repo
- [ ] Enable GitHub Actions in repository settings
- [ ] Test @claude by mentioning in an issue
- [ ] Verify @claude responds within 60 seconds

### C. Local Development Checklist

- [ ] Install Claude Code: `npm install -g @anthropics/claude-code`
- [ ] Authenticate: `claude auth login`
- [ ] Install GitHub CLI: `gh auth login`
- [ ] Test start-work script: `./scripts/start-work.sh 1`
- [ ] Test post-summary script: `./.claude/hooks/post-summary.sh "Test" "Test"`

---

## 🎯 Understanding the Workflow

### The Complete Flow

```
1. Create Issue (Feature Specification)
        ↓
2. @claude Reviews (GitHub Actions - automatic)
        ↓
3. ClaudeCode Reviews @claude's Review (manual)
        ↓
4. Discussion & Consensus
        ↓
5. ClaudeCode Posts "Final Consensus"
        ↓
6. Start Implementation: ./scripts/start-work.sh {issue-number}
        ↓
7. Implement with ClaudeCode (local)
        ↓
8. Test: {YOUR_TEST_COMMAND}
        ↓
9. Commit with detailed message
        ↓
10. Post Progress: ./.claude/hooks/post-summary.sh
        ↓
11. Push & Create PR
        ↓
12. @claude Reviews PR (automatic)
        ↓
13. Address Feedback & Post Updates
        ↓
14. Merge PR
        ↓
15. Cleanup: ./scripts/cleanup-after-merge.sh
```

**Full details:** See `.claude/WORKFLOW.md`

---

## 📂 Repository Structure

```
your-project/
│
├── CLAUDE.md ⭐ (Enforces workflow - customize this!)
├── README.md (Your project intro - customize this!)
├── TEMPLATE-USAGE.md (This file - can delete after setup)
│
├── .claude/
│   ├── WORKFLOW.md ⭐⭐ (Single source of truth - customize Quick Reference)
│   ├── settings.json (ClaudeCode hooks config)
│   ├── hooks/ (Automation scripts - use as-is)
│   │   ├── post-summary.sh
│   │   ├── user-prompt-submit-enhanced.sh
│   │   ├── post-tool-use.sh
│   │   ├── github-commenter.js
│   │   ├── prompt-logger.js
│   │   └── auto-cleanup-check.sh
│   └── scripts/
│       └── install-hooks.sh
│
├── .github/
│   ├── workflows/
│   │   ├── claude.yml (@claude bot - use as-is)
│   │   └── claude-code-review.yml (PR reviews - use as-is)
│   └── ISSUE_TEMPLATE/
│       ├── bug.md (customize if needed)
│       └── feature.md (customize if needed)
│
├── scripts/
│   ├── start-work.sh (use as-is)
│   └── cleanup-after-merge.sh (use as-is)
│
└── docs/ (Guides - all generic, use as-is)
    ├── GITHUB-CLAUDE-SETUP.md
    ├── AUTOMATION-FAQ.md
    ├── HOOKS-SETUP.md
    └── others...
```

---

## 🔧 Configuration Files to Customize

### Must Customize:

| File | What to Change | Why |
|------|----------------|-----|
| **CLAUDE.md** | Replace `{YOUR_*}` placeholders | ClaudeCode reads this at session start |
| **.claude/WORKFLOW.md** | Update Quick Reference (lines 6-12) | Project name and test command |
| **README.md** | Write your project description | First thing people see |

### Optional Customization:

| File | What to Change | Why |
|------|----------------|-----|
| **.github/ISSUE_TEMPLATE/** | Modify bug/feature templates | Match your issue format |
| **.gitignore** | Add project-specific patterns | Ignore your build artifacts |
| **scripts/start-work.sh** | Change branch naming if needed | Personal preference |

### Use As-Is (Don't Modify):

| File | Why |
|------|-----|
| **.claude/hooks/*.sh** | Automation scripts - tested and working |
| **.claude/hooks/*.js** | GitHub integration - tested and working |
| **.github/workflows/*.yml** | @claude bot configuration - already optimized |
| **scripts/cleanup-after-merge.sh** | Generic cleanup script |
| **docs/*.md** | Generic documentation |

---

## 💡 Common Customizations

### Example 1: Python Project

```bash
# CLAUDE.md customization
Repository: my-flask-api
Type: REST API (Python + Flask)
Test Command: pytest
Main Branch: main
```

```bash
# .claude/WORKFLOW.md (line 11)
**Test Command:** `pytest` (must pass before PR)
```

### Example 2: Rust Project

```bash
# CLAUDE.md customization
Repository: my-rust-cli
Type: CLI Tool (Rust)
Test Command: cargo test
Main Branch: main
```

```bash
# .claude/WORKFLOW.md (line 11)
**Test Command:** `cargo test` (must pass before PR)
```

### Example 3: Frontend Project

```bash
# CLAUDE.md customization
Repository: my-react-app
Type: Web Application (React + TypeScript)
Test Command: npm test
Main Branch: main
```

```bash
# .claude/WORKFLOW.md (line 11)
**Test Command:** `npm test` (must pass before PR)
```

---

## 🎓 Learning the Workflow

### For First-Time Users:

1. **Read:** `.claude/WORKFLOW.md` (comprehensive workflow guide)
2. **Read:** `AUTOMATION-FAQ.md` (common questions answered)
3. **Try:** Create a test issue and follow the workflow
4. **Practice:** Make a simple feature following all steps

### Key Documents:

| Document | Purpose | When to Read |
|----------|---------|--------------|
| **CLAUDE.md** | ClaudeCode's instructions | (Auto-read by ClaudeCode) |
| **.claude/WORKFLOW.md** | Complete workflow process | At start of each session |
| **AUTOMATION-FAQ.md** | Automation questions | When using scripts |
| **GITHUB-CLAUDE-SETUP.md** | Setup @claude bot | During initial setup |
| **HOOKS-SETUP.md** | Hook configuration | If customizing hooks |

---

## ✅ Verification Checklist

After setup, verify everything works:

### 1. GitHub @claude Bot

```bash
# Create test issue with @claude mention
gh issue create --title "Test" --body "@claude hello"

# Check Actions tab - should see workflow running
# @claude should respond in 30-60 seconds ✅
```

### 2. Local ClaudeCode

```bash
# In your project directory
claude

# ClaudeCode should start and read CLAUDE.md automatically
# Ask: "What workflow phase should I follow?"
# ClaudeCode should reference .claude/WORKFLOW.md ✅
```

### 3. Scripts

```bash
# Test start-work script
./scripts/start-work.sh 1
# Should create feature/1--description branch ✅

# Test cleanup script (after merging a PR)
./scripts/cleanup-after-merge.sh
# Should switch to main and delete feature branch ✅
```

### 4. Automation

```bash
# Test post-summary script
./.claude/hooks/post-summary.sh "Test request" "Test achievement"
# Should post to GitHub issue ✅
```

---

## 🆘 Troubleshooting

### @claude doesn't respond

**Check:**
1. Is `CLAUDE_CODE_OAUTH_TOKEN` secret set? (`gh secret list`)
2. Are GitHub Actions enabled? (Settings → Actions)
3. Did you mention @claude in the issue/comment?
4. Check Actions tab for error logs

**Fix:**
```bash
# Re-add the token
cat ~/.claude/.credentials.json | grep accessToken
gh secret set CLAUDE_CODE_OAUTH_TOKEN
```

### Scripts don't execute

**Check:**
1. Are they executable? (`ls -la scripts/`)
2. Are you in the repository root?

**Fix:**
```bash
chmod +x scripts/*.sh .claude/hooks/*.sh
```

### ClaudeCode doesn't read workflow

**Check:**
1. Does `CLAUDE.md` exist in repository root?
2. Does `.claude/WORKFLOW.md` exist?

**Fix:**
```bash
# Verify files exist
ls -la CLAUDE.md .claude/WORKFLOW.md

# Re-copy from template if missing
```

---

## 🚀 Next Steps

After setup:

1. **Delete this file** (`TEMPLATE-USAGE.md`) - you don't need it anymore
2. **Create your first real issue** - start building!
3. **Follow the workflow** - let @claude and ClaudeCode guide you
4. **Iterate and improve** - customize as you learn

---

## 📚 Additional Resources

- **Complete Workflow:** `.claude/WORKFLOW.md`
- **Automation Guide:** `AUTOMATION-FAQ.md`
- **GitHub Setup:** `GITHUB-CLAUDE-SETUP.md`
- **Hook Details:** `HOOKS-SETUP.md`
- **Troubleshooting:** `POST-MERGE-CLEANUP.md`

---

## 💬 Support

**Issues with the template?**
- Check `.claude/WORKFLOW.md` first
- Read `AUTOMATION-FAQ.md`
- Create an issue in the workflow-system repository

**Questions about Claude Code?**
- https://docs.anthropic.com/claude-code
- https://github.com/anthropics/claude-code

---

**Happy coding with your new workflow! 🎉**

The workflow will:
- Keep you organized
- Maintain high code quality
- Document everything automatically
- Make collaboration seamless

**Just follow `.claude/WORKFLOW.md` and let the automation handle the rest!**
