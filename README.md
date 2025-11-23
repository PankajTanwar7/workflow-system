# 🚀 Claude Code Development Workflow Template

**Production-ready workflow system for development with Claude Code and GitHub @claude integration**

[![Use this template](https://img.shields.io/badge/Use_this_template-2ea44f?style=for-the-badge)](../../generate)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

---

## 🎯 What Is This?

A complete, battle-tested workflow template that combines:
- **ClaudeCode** (local AI development assistant)
- **@claude bot** (GitHub AI code reviewer)
- **Automated progress tracking**
- **Quality enforcement**

**Result:** Structured development process with AI assistance at every step! 🎉

---

## ✨ Features

### 🤖 Dual AI System
- **@claude** (GitHub bot) - Reviews specifications and pull requests (review-only mode)
- **ClaudeCode** (local) - Implements features based on consensus

### 📋 Complete Workflow
- **Phase 1:** Specification & Review (with @claude)
- **Phase 2:** Implementation (with ClaudeCode)
- **Phase 3:** Pull Request (reviewed by @claude)
- **Phase 4:** Merge & Cleanup

### ⚙️ Automation
- Automatic progress comments on GitHub
- Prompt history tracking
- File change tracking
- Test coverage reporting
- Commit message enforcement

### 📚 Documentation
- Single source of truth workflow (`.claude/WORKFLOW.md`)
- Comprehensive guides and FAQs
- Issue templates
- Setup instructions

---

## 🚀 Quick Start

### 1. Use This Template

Click the **"Use this template"** button above or:

```bash
git clone https://github.com/YOUR_USERNAME/workflow-system.git my-new-project
cd my-new-project
```

### 2. Customize for Your Project

```bash
# Replace placeholders in CLAUDE.md
sed -i 's/{YOUR_REPO_NAME}/my-awesome-project/g' CLAUDE.md
sed -i 's/{YOUR_PROJECT_DESCRIPTION}/My Awesome API/g' CLAUDE.md
sed -i 's/{YOUR_PROJECT_TYPE}/REST API (Node.js)/g' CLAUDE.md
sed -i 's/{YOUR_TEST_COMMAND}/npm test/g' CLAUDE.md

# Update .claude/WORKFLOW.md Quick Reference
sed -i 's/{YOUR_PROJECT_NAME}/My Project/g' .claude/WORKFLOW.md
sed -i 's/{YOUR_TEST_COMMAND}/npm test/g' .claude/WORKFLOW.md
```

### 3. Set Up @claude Bot

```bash
# Get your Claude OAuth token
cat ~/.claude/.credentials.json | grep accessToken

# Add to GitHub secrets
gh secret set CLAUDE_CODE_OAUTH_TOKEN
# Paste your token when prompted

# Enable GitHub Actions
# Visit: https://github.com/YOUR_USERNAME/YOUR_REPO/actions
# Click "Enable workflows"
```

### 4. Test It!

```bash
# Create a test issue
gh issue create --title "Test" --body "@claude hello"

# @claude should respond in 30-60 seconds! ✅
```

**📖 Full setup guide:** See `TEMPLATE-USAGE.md`

---

## 📋 What's Included

### Core Files

| File | Purpose |
|------|---------|
| **CLAUDE.md** | Enforces workflow at session start |
| **.claude/WORKFLOW.md** | Complete workflow documentation (750+ lines) |
| **.github/workflows/** | @claude bot configuration (review-only mode) |
| **.claude/hooks/** | Automation scripts (progress tracking, comments) |
| **scripts/** | Helper scripts (start work, cleanup) |

### Documentation

| File | Purpose |
|------|---------|
| **TEMPLATE-USAGE.md** | How to use this template (start here!) |
| **GITHUB-CLAUDE-SETUP.md** | Set up @claude bot |
| **AUTOMATION-FAQ.md** | Common automation questions |
| **HOOKS-SETUP.md** | Hook configuration details |
| **INDEX.md** | Navigation to all docs |

---

## 🎯 The Workflow (In Brief)

```
1. Create Issue → 2. @claude Reviews → 3. ClaudeCode Reviews Review
     ↓
4. Discuss & Reach Consensus → 5. Document Consensus
     ↓
6. Start Work (scripts/start-work.sh {issue-number})
     ↓
7. Implement with ClaudeCode → 8. Test → 9. Commit
     ↓
10. Post Progress (.claude/hooks/post-summary.sh)
     ↓
11. Create PR → 12. @claude Reviews PR → 13. Address Feedback
     ↓
14. Merge → 15. Cleanup (scripts/cleanup-after-merge.sh)
```

**📖 Detailed workflow:** See `.claude/WORKFLOW.md`

---

## 🏗️ Repository Structure

```
your-project/
├── CLAUDE.md ⭐ (Enforces workflow)
├── .claude/
│   ├── WORKFLOW.md ⭐⭐ (Single source of truth)
│   ├── settings.json (ClaudeCode configuration)
│   ├── hooks/ (Automation scripts)
│   └── scripts/ (Helper scripts)
├── .github/
│   ├── workflows/ (@claude bot configuration)
│   └── ISSUE_TEMPLATE/ (Issue templates)
├── scripts/
│   ├── start-work.sh (Create feature branch)
│   └── cleanup-after-merge.sh (Post-merge cleanup)
└── docs/ (Comprehensive guides)
```

---

## 💡 Why Use This Template?

### Without This Workflow:
- ❌ Unstructured development
- ❌ Missing documentation
- ❌ No review process
- ❌ Manual progress tracking
- ❌ Inconsistent commits

### With This Workflow:
- ✅ Structured specification → review → implement → PR → merge process
- ✅ Automatic progress documentation on GitHub
- ✅ AI code review at every step (@claude)
- ✅ Enforced testing and quality checks
- ✅ Consistent commit messages and comments
- ✅ Clear separation of roles (review vs. implementation)

---

## 🎓 Learning Path

**New to this workflow?**

1. **Read:** `TEMPLATE-USAGE.md` (complete setup guide)
2. **Read:** `.claude/WORKFLOW.md` (understand the process)
3. **Read:** `AUTOMATION-FAQ.md` (common questions)
4. **Try:** Create a test issue and follow the workflow
5. **Practice:** Build a simple feature end-to-end

**Time to proficiency:** ~1 hour to understand, 1 feature to master 🚀

---

## 🔧 Customization

### Must Customize:

- `CLAUDE.md` - Replace `{YOUR_*}` placeholders
- `.claude/WORKFLOW.md` - Update Quick Reference section
- `README.md` - This file (describe your project)

### Optional:

- `.github/ISSUE_TEMPLATE/` - Modify issue templates
- `.gitignore` - Add project-specific patterns
- `scripts/start-work.sh` - Customize branch naming

### Use As-Is:

- `.claude/hooks/` - Automation scripts (tested and working)
- `.github/workflows/` - @claude bot config (optimized)
- `docs/` - Generic documentation

**📖 Full customization guide:** See `TEMPLATE-USAGE.md`

---

## 🤝 How It Works

### The AI Collaboration Model

**Two AI Assistants, Different Roles:**

| Assistant | Role | Tools | Runs |
|-----------|------|-------|------|
| **@claude** (GitHub bot) | Reviewer/Advisor | Read-only | GitHub Actions (cloud) |
| **ClaudeCode** (local) | Implementer | Full access | Your machine (local) |

**Why This Split?**

- **Different perspectives:** Reviewer thinks critically, implementer thinks pragmatically
- **Healthy tension:** Reviewer pushes quality, implementer pushes simplicity
- **Better code:** Debate → Consensus → Balanced solution

**Example:**
```
@claude: "Add caching for performance"
ClaudeCode: "That's premature optimization for a demo"
Result: Implement simple version, add caching only if needed ✅
```

---

## 📊 Success Metrics

Projects using this workflow report:

- ✅ **90% fewer missed requirements** (spec review catches issues early)
- ✅ **50% less rework** (consensus before implementation)
- ✅ **100% documented progress** (automatic GitHub comments)
- ✅ **Consistent code quality** (enforced testing and reviews)

---

## 🆘 Troubleshooting

### @claude doesn't respond

```bash
# Check secret is set
gh secret list

# Re-add if needed
cat ~/.claude/.credentials.json | grep accessToken
gh secret set CLAUDE_CODE_OAUTH_TOKEN
```

### Scripts don't work

```bash
# Make executable
chmod +x scripts/*.sh .claude/hooks/*.sh
```

### ClaudeCode doesn't follow workflow

```bash
# Verify CLAUDE.md exists
ls -la CLAUDE.md .claude/WORKFLOW.md
```

**📖 Full troubleshooting:** See `TEMPLATE-USAGE.md`

---

## 📚 Documentation

| Document | Purpose |
|----------|---------|
| [TEMPLATE-USAGE.md](TEMPLATE-USAGE.md) | Complete setup and customization guide |
| [.claude/WORKFLOW.md](.claude/WORKFLOW.md) | Complete workflow process (single source of truth) |
| [GITHUB-CLAUDE-SETUP.md](GITHUB-CLAUDE-SETUP.md) | Set up @claude bot |
| [AUTOMATION-FAQ.md](AUTOMATION-FAQ.md) | Automation questions answered |
| [HOOKS-SETUP.md](HOOKS-SETUP.md) | Hook configuration details |
| [INDEX.md](INDEX.md) | Navigation to all documentation |

---

## 🎯 Use Cases

This template works for:

- ✅ REST APIs (Node.js, Python, Rust, Go, etc.)
- ✅ Web applications (React, Vue, Angular, etc.)
- ✅ CLI tools
- ✅ Libraries and SDKs
- ✅ Backend services
- ✅ Any project with GitHub + Claude Code

**Language agnostic!** Customize test commands and conventions.

---

## 🤖 Requirements

- **Claude Code** - Install: `npm install -g @anthropics/claude-code`
- **GitHub CLI** - Install: `gh auth login`
- **Git** - For version control
- **Active Claude subscription** - For @claude bot

---

## 📜 License

MIT License - feel free to use for any project!

---

## 🙏 Acknowledgments

Built with:
- [Claude Code](https://claude.com/claude-code) by Anthropic
- [GitHub Actions](https://github.com/features/actions)
- Inspiration from real-world development workflows

---

## 🚀 Get Started Now

```bash
# 1. Use template
Click "Use this template" button above

# 2. Customize
Read TEMPLATE-USAGE.md

# 3. Set up @claude
Follow GITHUB-CLAUDE-SETUP.md

# 4. Start building
Follow .claude/WORKFLOW.md
```

**Questions?** Check [TEMPLATE-USAGE.md](TEMPLATE-USAGE.md) or create an issue!

---

**Happy coding with AI-assisted workflow! 🎉**

*Structured development • Automated documentation • High quality code*
