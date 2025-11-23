# 📘 CLAUDE.md Guide

**How to use and customize your project's CLAUDE.md file**

---

## 🎯 What is CLAUDE.md?

`CLAUDE.md` is a special file that provides context and guidelines to Claude (both Claude Code and GitHub @claude) when working on your project.

**Think of it as:**
- Instructions manual for AI assistants
- Project-specific coding standards
- Context that helps Claude give better suggestions

---

## ✨ Benefits

### For Development
- ✅ Claude follows your project's conventions
- ✅ More relevant code suggestions
- ✅ Consistent code reviews
- ✅ Better architecture recommendations

### For Your Team
- ✅ Documents your standards in one place
- ✅ Helps onboard new developers
- ✅ Creates shared understanding
- ✅ Reduces back-and-forth in reviews

---

## 🚀 Quick Start

### 1. Copy the Template

```bash
# Copy CLAUDE.md to your project
cp ~/workflow-system/CLAUDE.md ~/your-project/

# Commit it
cd ~/your-project
git add CLAUDE.md
git commit -m "docs: add CLAUDE.md for AI-assisted development"
git push
```

### 2. Customize for Your Project

Edit the file and fill in:
- Project description
- Your tech stack
- Your coding standards
- Your testing requirements

### 3. Test It

Create an issue or PR and tag @claude:
```markdown
@claude Please review this code following our project standards.
```

Claude will reference your CLAUDE.md automatically!

---

## 📝 What to Include

### Essential Sections (Must Have)

1. **Project Overview**
   - What the project does
   - Tech stack
   - Architecture basics

2. **Code Style**
   - Naming conventions
   - File organization
   - Comment guidelines

3. **Testing Standards**
   - How to write tests
   - Coverage requirements
   - What to test

### Important Sections (Should Have)

4. **Security Standards**
   - Security checklist
   - Common vulnerabilities to avoid
   - Authentication patterns

5. **Performance Guidelines**
   - Performance targets
   - Best practices
   - Optimization tips

### Nice-to-Have Sections

6. **Development Workflow**
   - Branching strategy
   - Commit message format
   - PR process

7. **Common Patterns**
   - Preferred code patterns
   - Error handling
   - API structure

---

## 🎨 Customization Examples

### Example 1: Node.js API Project

```markdown
## Tech Stack
- **Backend:** Node.js 20 + Express.js
- **Database:** PostgreSQL with Prisma ORM
- **Testing:** Jest + Supertest
- **Validation:** Zod

## Code Style
- Use ES modules (not CommonJS)
- Async/await only (no callbacks)
- Prefer functional programming
```

### Example 2: React Frontend Project

```markdown
## Tech Stack
- **Framework:** React 18 with TypeScript
- **State:** Zustand
- **Styling:** Tailwind CSS
- **Testing:** Vitest + React Testing Library

## Code Style
- Functional components only (no classes)
- Use custom hooks for logic reuse
- Prefer composition over prop drilling
```

### Example 3: Python FastAPI Project

```markdown
## Tech Stack
- **Framework:** FastAPI 0.100+
- **Database:** PostgreSQL with SQLAlchemy
- **Testing:** pytest
- **Validation:** Pydantic

## Code Style
- Type hints required
- Follow PEP 8
- Use async def for endpoints
```

---

## 💡 Pro Tips

### Tip 1: Be Specific

**Bad:**
```markdown
## Code Style
Write good code.
```

**Good:**
```markdown
## Code Style
- Functions: camelCase (`getUserData`)
- Classes: PascalCase (`TaskManager`)
- Files: kebab-case (`task-manager.js`)
- Max line length: 100 characters
```

### Tip 2: Include Examples

**Bad:**
```markdown
Use proper error handling.
```

**Good:**
```markdown
### Error Handling
```javascript
try {
  await operation();
} catch (error) {
  logger.error('Operation failed', { error });
  throw new AppError('User-friendly message', 500);
}
```
```

### Tip 3: Explain "Why"

**Bad:**
```markdown
Don't use library X.
```

**Good:**
```markdown
Don't use library X - it has known security vulnerabilities.
Use library Y instead (maintained, secure, better performance).
```

### Tip 4: Keep It Updated

```markdown
**Last Updated:** 2025-01-20
**Next Review:** 2025-03-01

Update this file when:
- New conventions adopted
- Tech stack changes
- New security requirements
```

---

## 🔍 How Claude Uses CLAUDE.md

### In Automatic PR Reviews

```yaml
# claude-code-review.yml
prompt: |
  Use the repository's CLAUDE.md for guidance on:
  - Code style and conventions
  - Testing requirements
  - Security standards
```

When @claude reviews your PR, it:
1. Reads your CLAUDE.md
2. Checks code against your standards
3. Provides feedback aligned with your project

### In Issue Discussions

When you ask @claude for help:
```markdown
@claude How should I implement user authentication?
```

Claude will:
1. Check your CLAUDE.md for tech stack
2. Follow your preferred patterns
3. Suggest code in your style
4. Consider your security standards

---

## 📊 Real-World Examples

### Scenario 1: Code Review

**Without CLAUDE.md:**
```markdown
@claude Review this code.

Claude: "This looks fine, but consider using TypeScript."
You: "We use vanilla JavaScript in this project."
```

**With CLAUDE.md:**
```markdown
# In CLAUDE.md
Tech Stack: JavaScript (no TypeScript)

@claude Review this code.

Claude: "Code looks good! Follows your JavaScript patterns.
Suggestion: Add JSDoc comments for better documentation."
```

### Scenario 2: Architecture Help

**Without CLAUDE.md:**
```markdown
@claude How should I structure the auth system?

Claude: "I recommend JWT with Redis..."
You: "We don't use Redis, we have PostgreSQL only."
```

**With CLAUDE.md:**
```markdown
# In CLAUDE.md
Database: PostgreSQL only (no Redis)

@claude How should I structure the auth system?

Claude: "For PostgreSQL-only setup, store refresh tokens
in a `tokens` table with indexed user_id and expiry..."
```

---

## 🛠️ Maintenance

### Monthly Review

Check if CLAUDE.md needs updates:
- [ ] New libraries added to project?
- [ ] Coding standards changed?
- [ ] New security requirements?
- [ ] Performance targets adjusted?

### After Major Changes

Update CLAUDE.md when:
- ✅ Tech stack upgrade (e.g., Node 18 → 20)
- ✅ New framework adopted
- ✅ Security policy changes
- ✅ Team standards evolve

### Version Control

```bash
# Track changes
git log -- CLAUDE.md

# See what changed
git diff HEAD~1 CLAUDE.md
```

---

## 🎯 Best Practices

### Do ✅

- ✅ Keep it concise (2-3 pages max)
- ✅ Use code examples
- ✅ Be specific and actionable
- ✅ Update regularly
- ✅ Version control it

### Don't ❌

- ❌ Copy-paste generic advice
- ❌ Make it too long (50+ pages)
- ❌ Forget to update it
- ❌ Include secrets or credentials
- ❌ Duplicate existing docs (link instead)

---

## 📚 Templates for Different Project Types

### Node.js API Template
```markdown
## Tech Stack
- Node.js 20 + Express
- PostgreSQL + Prisma
- Jest

## Standards
- ES modules
- Async/await
- RESTful APIs
```

### React SPA Template
```markdown
## Tech Stack
- React 18 + TypeScript
- Vite
- Tailwind CSS
- Vitest

## Standards
- Functional components
- Custom hooks
- Composition
```

### Python API Template
```markdown
## Tech Stack
- Python 3.11+ FastAPI
- PostgreSQL + SQLAlchemy
- pytest

## Standards
- Type hints required
- PEP 8 compliance
- Async endpoints
```

---

## 🤝 Team Collaboration

### Getting Buy-in

**Present to team:**
```markdown
CLAUDE.md Benefits:
1. Claude gives better suggestions (saves review time)
2. Documents our standards (helps onboarding)
3. Consistent AI assistance (everyone gets same quality)
4. Living document (evolves with project)
```

### Collaborative Editing

```bash
# Create PR to update CLAUDE.md
git checkout -b docs/update-claude-md
# Edit CLAUDE.md
git commit -m "docs: update code style guidelines"
gh pr create --title "Update CLAUDE.md with new conventions"
```

### Review Process

- **Minor updates:** Direct commit to main
- **Major changes:** PR with team review
- **New sections:** Discuss in team meeting first

---

## 🎓 Learning Resources

### Examples from Real Projects

- [Anthropic Claude Code Action](https://github.com/anthropics/claude-code-action) - See their docs
- [Next.js](https://github.com/vercel/next.js) - Check their contributing guide
- [Prisma](https://github.com/prisma/prisma) - See their style guide

### Best Practices

- Keep it project-specific (not generic)
- Show, don't just tell (use examples)
- Make it scannable (headings, bullets)
- Link to detailed docs (don't duplicate)

---

## ✅ Checklist: Is Your CLAUDE.md Ready?

- [ ] Project overview complete
- [ ] Tech stack listed
- [ ] Code style documented
- [ ] Testing standards defined
- [ ] Security guidelines included
- [ ] Examples provided
- [ ] File is concise (< 500 lines)
- [ ] Committed to repository
- [ ] Team has reviewed it

---

**🎉 You're Ready!**

Your CLAUDE.md will help Claude provide better, more relevant assistance for your project!

---

*Part of the Ultimate Development Workflow System*
