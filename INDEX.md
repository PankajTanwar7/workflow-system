# 📚 Workflow System - Document Index

**Quick navigation to all documentation**

---

## 🚀 Getting Started (Read in Order)

1. **[README.md](README.md)** - Start here!
   - What is this system?
   - Quick start guide
   - Prerequisites and setup
   - FAQ

2. **[VISUAL-SUMMARY.md](VISUAL-SUMMARY.md)** - See the big picture
   - Diagrams and flowcharts
   - 5-minute example
   - Tool selection matrix
   - Learning path

3. **[WORKFLOW.md](WORKFLOW.md)** - Complete guide
   - Full step-by-step example
   - Phase-by-phase breakdown
   - Best practices
   - Troubleshooting

4. **[QUICKREF.md](QUICKREF.md)** - Daily reference
   - Copy-paste commands
   - Common operations
   - Shell aliases
   - Emergency procedures

---

## 📂 System Components

### Documentation
- `README.md` - Main entry point
- `WORKFLOW.md` - Complete workflow guide (24KB)
- `QUICKREF.md` - Quick reference (7KB)
- `VISUAL-SUMMARY.md` - Visual guide (17KB)
- `GITHUB-CLAUDE-SETUP.md` - @claude GitHub integration guide
- `CLAUDE.md` - Project guidelines template for Claude
- `CLAUDE-MD-GUIDE.md` - How to customize CLAUDE.md
- `PROMPT-COMPATIBILITY.md` - How @claude prompts work together ✨ NEW!
- `HOOKS-SETUP.md` - Automatic prompt logging setup guide ✨ NEW!
- `INDEX.md` - This file

### Automation
- `.claude/hooks/prompt-logger.js` - Auto-logging hook (5KB)
- `scripts/start-work.sh` - Helper script to start work on issues (10KB)

### Templates
- `.github/ISSUE_TEMPLATE/feature.md` - Feature issue template
- `.github/ISSUE_TEMPLATE/bug.md` - Bug issue template
- `.github/workflows/claude.yml` - @claude manual mentions workflow (Enhanced!)
- `.github/workflows/claude-code-review.yml` - Automatic PR reviews ✨ NEW!

### Output
- `docs/dev-logs/` - Auto-generated development logs
- `docs/dev-logs/README.md` - Auto-generated index

---

## 🎯 Quick Access by Use Case

### "I want to understand the workflow"
→ Read: [VISUAL-SUMMARY.md](VISUAL-SUMMARY.md)
→ Then: [WORKFLOW.md](WORKFLOW.md) sections 1-2

### "I want to understand how @claude prompts work together"
→ Read: [PROMPT-COMPATIBILITY.md](PROMPT-COMPATIBILITY.md)
→ Then: See the complete example in the doc

### "I want to set up automatic prompt logging"
→ Read: [HOOKS-SETUP.md](HOOKS-SETUP.md)
→ Then: Follow the Quick Setup section

### "I want to set it up"
→ Read: [README.md](README.md) "Quick Start" section
→ Then: Run setup commands

### "I want to start working on an issue"
→ Read: [QUICKREF.md](QUICKREF.md) "Starting Work" section
→ Then: `./scripts/start-work.sh <issue-number>`

### "I need a specific command"
→ Open: [QUICKREF.md](QUICKREF.md)
→ Find: Your use case and copy-paste

### "I want to customize it"
→ Read: [WORKFLOW.md](WORKFLOW.md) "Configuration" section
→ Edit: `.claude/hooks/prompt-logger.js` or templates

### "Something isn't working"
→ Read: [README.md](README.md) "Troubleshooting" section
→ Or: [WORKFLOW.md](WORKFLOW.md) "Troubleshooting" section

### "I want to see a real example"
→ Read: [WORKFLOW.md](WORKFLOW.md) "Complete Example"
→ Or: [VISUAL-SUMMARY.md](VISUAL-SUMMARY.md) "5 Minutes Example"

---

## 📖 Documentation by Size

**Quick reads (< 5 minutes):**
- README.md (10KB) - Overview and setup
- QUICKREF.md (7KB) - Command reference

**Medium reads (10-15 minutes):**
- VISUAL-SUMMARY.md (17KB) - Diagrams and examples

**Complete guide (30+ minutes):**
- WORKFLOW.md (24KB) - Full workflow with detailed example

---

## 🔧 File Organization

```
workflow-system/
├── 📘 Documentation
│   ├── INDEX.md              ← You are here
│   ├── README.md             ← Start here
│   ├── WORKFLOW.md           ← Complete guide
│   ├── QUICKREF.md           ← Quick reference
│   └── VISUAL-SUMMARY.md     ← Visual guide
│
├── 🔧 Automation
│   ├── .claude/
│   │   └── hooks/
│   │       └── prompt-logger.js
│   └── scripts/
│       └── start-work.sh
│
├── 📋 Templates
│   └── .github/
│       └── ISSUE_TEMPLATE/
│           ├── feature.md
│           └── bug.md
│
└── 📁 Output
    └── docs/
        └── dev-logs/
            ├── README.md     (auto-generated)
            ├── issue-XX.md   (auto-generated)
            └── ...           (auto-generated)
```

---

## 📊 Document Details

| Document | Size | Read Time | Purpose |
|----------|------|-----------|---------|
| README.md | 10KB | 5 min | Overview, setup, FAQ |
| WORKFLOW.md | 24KB | 30 min | Complete guide with example |
| QUICKREF.md | 7KB | 3 min | Copy-paste commands |
| VISUAL-SUMMARY.md | 17KB | 15 min | Diagrams and visuals |
| INDEX.md | 3KB | 2 min | Navigation (this file) |

**Total documentation:** ~61KB, ~55 minutes to read everything

---

## 🎓 Recommended Reading Path

### For First-Time Users
```
1. README.md (Quick Start section)
2. VISUAL-SUMMARY.md (Complete Workflow Diagram)
3. Follow setup instructions
4. WORKFLOW.md (Phase 1-2 only)
5. Try it yourself!
6. QUICKREF.md (bookmark for daily use)
```

### For Experienced Developers
```
1. VISUAL-SUMMARY.md (scan diagrams)
2. README.md (setup only)
3. QUICKREF.md (bookmark this)
4. Start using immediately
5. Refer to WORKFLOW.md as needed
```

### For Team Leaders
```
1. README.md (full read)
2. WORKFLOW.md ("Benefits" section)
3. VISUAL-SUMMARY.md ("Team Collaboration")
4. Customize templates for your team
5. Share QUICKREF.md with team
```

---

## 🔍 Find Information Quickly

### By Topic

**Architecture & Design**
- WORKFLOW.md → "Phase 1: Planning"
- VISUAL-SUMMARY.md → "Tool Selection Matrix"

**Implementation**
- WORKFLOW.md → "Phase 2-3: Implementation"
- QUICKREF.md → "Claude Code Prompts"

**Git & GitHub**
- QUICKREF.md → "Git Operations"
- WORKFLOW.md → "Phase 4: Code Review"

**Automation**
- README.md → "Configure Claude Code Hook"
- WORKFLOW.md → "Hook System"

**Examples**
- WORKFLOW.md → "Complete Example: Step-by-Step"
- VISUAL-SUMMARY.md → "5 Minutes from Issue to PR"

**Commands**
- QUICKREF.md → All sections
- README.md → "Quick Start"

**Troubleshooting**
- README.md → "Troubleshooting"
- WORKFLOW.md → "Troubleshooting"

**Customization**
- README.md → "Configuration"
- WORKFLOW.md → "Advanced Usage"

---

## 💡 Pro Tips

### Tip 1: Bookmark These
- Keep [QUICKREF.md](QUICKREF.md) open in a terminal
- Pin [VISUAL-SUMMARY.md](VISUAL-SUMMARY.md) for reference
- Share [README.md](README.md) with new team members

### Tip 2: Search Documentation
```bash
# Find specific topic across all docs
grep -r "authentication" *.md

# Find specific command
grep -r "gh pr create" *.md

# Find all examples
grep -r "Example:" *.md
```

### Tip 3: Print Quick Reference
```bash
# Convert to PDF for offline reference
pandoc QUICKREF.md -o quickref.pdf

# Or keep markdown on second monitor
less QUICKREF.md
```

### Tip 4: Progressive Learning
- Day 1: Just README.md + setup
- Week 1: Add QUICKREF.md commands
- Month 1: Read full WORKFLOW.md
- Month 2: Master advanced features

---

## 🔄 Document Updates

This documentation is complete and stable. Updates you might make:

- **Project-specific examples** in WORKFLOW.md
- **Custom commands** in QUICKREF.md
- **Team guidelines** in README.md
- **Additional templates** in .github/ISSUE_TEMPLATE/

Keep this INDEX.md updated if you add new documentation files.

---

## 📞 Need Help?

1. **Check documentation first:**
   - Search this INDEX.md for your topic
   - Check QUICKREF.md for commands
   - Read WORKFLOW.md troubleshooting

2. **Ask Claude Code:**
   ```
   "How do I [task] using this workflow system?"
   "Debug: [describe problem]"
   ```

3. **Ask @claude in GitHub:**
   ```markdown
   @claude I'm having trouble with [issue]
   ```

---

## ✅ Checklist: Did I Read Everything?

Use this to track your progress:

- [ ] README.md - Overview and setup
- [ ] VISUAL-SUMMARY.md - Diagrams and big picture
- [ ] WORKFLOW.md - Complete guide with example
- [ ] QUICKREF.md - Daily commands
- [ ] Tried the workflow myself
- [ ] Bookmarked QUICKREF.md
- [ ] Shared with my team (if applicable)

---

**🎉 Ready to start? Go to [README.md](README.md) for setup instructions!**
