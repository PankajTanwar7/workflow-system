# 🔄 Prompt Compatibility Guide

**How GitHub @claude Issue Planning and PR Review Prompts Work Together**

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [The Two Prompts](#the-two-prompts)
3. [How They Work Together](#how-they-work-together)
4. [Complete Workflow Example](#complete-workflow-example)
5. [Compatibility Matrix](#compatibility-matrix)
6. [Viewing Prompts](#viewing-prompts)
7. [Best Practices](#best-practices)
8. [Troubleshooting](#troubleshooting)

---

## 🎯 Overview

This workflow system uses **two distinct but complementary prompts** for @claude:

1. **Issue Planning Prompt** - Architecture and design advice (Phase 1)
2. **PR Review Prompt** - Code quality verification (Phase 4)

These prompts are **designed to work together** as part of a closed feedback loop where:
- @claude suggests architecture → You implement → @claude validates implementation

This creates a **self-consistent workflow** where the same AI that designed the architecture also reviews the implementation against that design.

---

## 🎨 The Two Prompts

### Prompt 1: Issue Planning (@claude in GitHub Issues)

**Purpose:** Get architecture advice and design recommendations before coding

**Location:** Manually triggered by mentioning @claude in issue comments

**Format:** Free-form question and answer

**Example Issue Template:**
```markdown
## 🏗️ Architecture Discussion (@claude)

@claude Please help design the architecture for this task manager API:

**Questions:**
1. What's the best structure for a simple Node.js REST API?
2. Should we use Express.js or another framework?
3. How should we structure the project folders?
4. What about error handling and validation?

**Constraints:**
- Tech stack: Node.js (simple, no database for now)
- Performance requirements: Basic REST API
- Security considerations: Input validation
```

**What @claude Provides:**
- ✅ Framework recommendations (e.g., "Use Express.js")
- ✅ Architecture patterns (e.g., "Layered architecture: routes → controllers → models")
- ✅ Project structure (folder organization)
- ✅ Security recommendations (e.g., "Use helmet, XSS sanitization")
- ✅ Error handling strategies
- ✅ Testing approach
- ✅ Best practices for your specific use case

**Workflow File:** `.github/workflows/claude.yml`

---

### Prompt 2: PR Review (@claude in Pull Requests)

**Purpose:** Verify implementation quality, security, and adherence to best practices

**Location:** Automatically triggered on every PR push (or manually via @claude mention)

**Format:** Structured template with specific review sections

**Prompt Template:**
```yaml
prompt: |
  REPOSITORY: ${{ github.repository }}
  PR NUMBER: ${{ github.event.pull_request.number }}
  AUTHOR: @${{ github.event.pull_request.user.login }}
  TITLE: ${{ github.event.pull_request.title }}

  Please review this pull request and provide structured feedback.

  Use the repository's CLAUDE.md file (if it exists) for project-specific guidance on:
  - Code style and conventions
  - Testing requirements
  - Security standards
  - Performance expectations

  Provide your review in this format:

  ## 📋 Summary
  [Brief overview of what this PR does and overall assessment]

  ## ✅ What's Good
  - [Highlight positive aspects and good practices]

  ## ⚠️ Issues Found

  ### 🔴 Critical (Must Fix)
  - [Security vulnerabilities, bugs, breaking changes]

  ### 🟡 Important (Should Fix)
  - [Performance issues, code quality, best practices]

  ### 🟢 Nice-to-have (Consider)
  - [Minor improvements, style suggestions]

  ## 💡 Suggestions
  [Specific improvements with code examples where helpful]

  ## ✅ Checklist
  - [ ] Tests added/updated appropriately
  - [ ] Documentation updated if needed
  - [ ] No obvious security vulnerabilities
  - [ ] Performance is acceptable
  - [ ] Code follows project conventions

  ## 📚 Additional Notes
  [Any other observations or recommendations]
```

**What @claude Checks:**
- ✅ Did you follow the architecture I suggested?
- ✅ Are security best practices implemented?
- ✅ Is code quality acceptable?
- ✅ Are tests comprehensive?
- ✅ Does it meet acceptance criteria?
- ✅ Are there any bugs or vulnerabilities?

**Workflow File:** `.github/workflows/claude-code-review.yml`

---

## 🔄 How They Work Together

### The Complete Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    PHASE 1: PLANNING                        │
│                  (GitHub Issue @claude)                     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │  Issue #1: "Add task creation endpoint"  │
    │                                           │
    │  Contains:                                │
    │  • Feature description                    │
    │  • Acceptance criteria                    │
    │  • Architecture questions for @claude     │
    └───────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │   @claude responds with ARCHITECTURE:     │
    │                                           │
    │   • Use Express.js framework              │
    │   • Layered architecture pattern          │
    │   • express-validator for validation      │
    │   • Security: helmet, CORS, XSS           │
    │   • Error handling strategy               │
    │   • Testing approach                      │
    └───────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              PHASE 2: IMPLEMENTATION                        │
│                  (Claude Code - Developer)                  │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │  Developer runs: ./start-work.sh 1        │
    │                                           │
    │  Script generates prompt with:            │
    │  • Issue details and acceptance criteria  │
    │  • @claude's architecture advice          │
    │  • CLAUDE.md project guidelines           │
    └───────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │   Developer implements code following:    │
    │                                           │
    │   ✓ @claude's architecture advice         │
    │   ✓ Acceptance criteria from Issue #1     │
    │   ✓ Security best practices               │
    │   ✓ Project conventions from CLAUDE.md    │
    └───────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                PHASE 3: CODE REVIEW                         │
│          (GitHub PR @claude automatic review)               │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │  PR created, workflow triggers @claude    │
    │                                           │
    │  @claude receives:                        │
    │  • Structured review prompt (template)    │
    │  • All file changes (diff)                │
    │  • CLAUDE.md (project standards)          │
    │  • PR metadata (title, author, number)    │
    │  • Original issue context                 │
    └───────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │   @claude reviews code against:           │
    │                                           │
    │   ✓ Architecture it originally suggested  │
    │   ✓ Acceptance criteria from Issue #1     │
    │   ✓ Security best practices               │
    │   ✓ Code quality standards                │
    │   ✓ Test coverage expectations            │
    │   ✓ Project conventions (CLAUDE.md)       │
    └───────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │   @claude posts STRUCTURED REVIEW:        │
    │                                           │
    │   📋 Summary & recommendation             │
    │   ✅ What's good                          │
    │   ⚠️  Issues (Critical/Important/Nice)    │
    │   💡 Suggestions with code examples       │
    │   ✅ Checklist verification               │
    │   📚 Additional notes                     │
    └───────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │   Developer addresses feedback:           │
    │                                           │
    │   • Fix critical issues immediately       │
    │   • Address important issues              │
    │   • Consider nice-to-have suggestions     │
    │   • Push fixes to same branch             │
    └───────────────────────────────────────────┘
                            │
                            ▼
    ┌───────────────────────────────────────────┐
    │   Automatic re-review triggers:           │
    │                                           │
    │   • @claude reviews fixes                 │
    │   • Verifies issues are resolved          │
    │   • Approves when quality meets standards │
    └───────────────────────────────────────────┘
                            │
                            ▼
                       MERGE PR ✅
```

### The Compatibility Magic

**The key insight:** The same AI (@claude) that provides architecture advice in Phase 1 also validates the implementation in Phase 3. This creates a **closed feedback loop** where:

1. **@claude suggests** architecture patterns
2. **You implement** following those patterns
3. **@claude validates** you followed the patterns correctly

This is far more consistent than:
- ❌ One person designs, another reviews
- ❌ Different review standards each time
- ❌ Misalignment between design and review

---

## 📊 Compatibility Matrix

| Aspect | Issue Planning (@claude) | PR Review (@claude) | How They Connect |
|--------|-------------------------|---------------------|------------------|
| **Purpose** | Architecture design & planning | Code quality verification | Review validates implementation matches design |
| **When** | Before coding starts | After code is written | Sequential workflow |
| **Trigger** | Manual @claude mention | Automatic on PR push | Planned → Implemented → Reviewed |
| **Format** | Free-form Q&A | Structured template | Design becomes reference for review |
| **Focus** | "How should we build this?" | "Did we build it correctly?" | Design → Implementation → Validation |
| **Output** | Architecture recommendations, file structure, tech choices | Security issues, code quality, best practices | Design principles checked in review |
| **Context** | Issue description, acceptance criteria | All code changes + CLAUDE.md + original architecture | Full project context |
| **Human Role** | Ask questions, gather requirements | Fix issues, improve code | Developer stays in control |
| **AI Role** | Advisory (suggests approaches) | Evaluative (checks quality) | Consistent standards throughout |

---

## 🎯 Complete Workflow Example

### Real Example: Task Manager API

Let's walk through a complete example to see how the prompts work together.

#### Step 1: Issue Planning

**Issue #1 Created:**
```markdown
# Feature: Add Task Creation Endpoint

## 📋 Feature Description
Create a REST API endpoint to add new tasks to our task manager.

## 🎯 Acceptance Criteria
- [ ] POST /api/tasks endpoint accepts { title, description }
- [ ] Tasks are stored in memory (array) for now
- [ ] Endpoint returns created task with auto-generated ID
- [ ] Input validation (title is required)
- [ ] Proper HTTP status codes (201 for success, 400 for validation errors)

## 🏗️ Architecture Discussion (@claude)

@claude Please help design the architecture for this task manager API:

**Questions:**
1. What's the best structure for a simple Node.js REST API?
2. Should we use Express.js or another framework?
3. How should we structure the project folders?
4. What about error handling and validation?

**Constraints:**
- Tech stack: Node.js (simple, no database for now)
- Performance requirements: Basic REST API
- Security considerations: Input validation
```

#### Step 2: @claude's Architecture Response

**@claude responds in Issue #1:**
```markdown
### 🏗️ Architecture Recommendations

#### 1. Best Structure
I recommend a **layered architecture** with clear separation of concerns:

src/
├── routes/           # API route definitions
├── controllers/      # Business logic handlers
├── models/          # Data models and operations
├── middleware/      # Validation, error handling
└── utils/           # Helper functions

#### 2. Framework Choice: Express.js ✅
**Recommendation: Use Express.js**

Reasons:
- ✅ Industry standard (14M+ weekly downloads)
- ✅ Simple & lightweight for REST APIs
- ✅ Great middleware ecosystem
- ✅ Easy to learn, minimal boilerplate

#### 3. Error Handling & Validation
- Use **express-validator** for input validation
- Implement **centralized error handler middleware**
- Use **consistent error response format**

#### 4. Security Recommendations
- ✅ Add **helmet** for security headers
- ✅ Use **express-rate-limit** to prevent abuse
- ✅ Implement **XSS sanitization** on inputs
- ✅ Enable **CORS** appropriately

#### 5. Testing
- Use **Jest + Supertest** for API testing
- Aim for 80%+ code coverage
- Test both happy paths and error cases
```

#### Step 3: Implementation

**Developer runs:**
```bash
./scripts/start-work.sh 1
```

**Script generates prompt file with:**
- Issue #1 details
- Acceptance criteria
- @claude's architecture advice
- CLAUDE.md project guidelines

**Developer implements:**
- ✅ Express.js with layered architecture
- ✅ express-validator for validation
- ✅ Centralized error handler
- ✅ Helmet + rate limiting + XSS protection
- ✅ Jest + Supertest tests (14 tests)

#### Step 4: PR Created

**PR #2 opened:**
```markdown
# feat: implement task creation endpoint

Implements the task creation API endpoint as specified in #1

## Changes
- Added Express.js server with layered architecture
- Implemented CRUD operations for tasks
- Added input validation with express-validator
- Added security middleware (helmet, rate limiting, XSS)
- Added comprehensive test suite (14 tests)
- Added centralized error handling

## Testing
- ✅ All tests passing
- ✅ Input validation working
- ✅ Security middleware active

Closes #1
```

#### Step 5: Automatic Review Triggers

**@claude reviews the PR automatically and receives:**
- The structured review prompt (from workflow)
- All 14 files changed
- CLAUDE.md project standards
- PR metadata

**@claude's review checks:**
- ✅ "Did they use Express.js like I suggested?" → YES
- ✅ "Is the layered architecture implemented?" → YES
- ✅ "Is express-validator used?" → YES
- ✅ "Are security measures in place?" → Found XSS issue
- ✅ "Is error handling centralized?" → YES
- ✅ "Are tests comprehensive?" → YES

**@claude posts review:**
```markdown
## 📋 Summary
This PR implements a complete RESTful Task Manager API with Express.js,
following the layered architecture I recommended. Overall excellent work!

**Recommendation:** ✅ Approve with minor fixes

## ✅ What's Good
- ✅ **Excellent security practices** - Helmet, rate limiting, validation
- ✅ **Clean architecture** - Clear separation: routes → controllers → models
- ✅ **Comprehensive tests** - 14 test cases covering all scenarios

## ⚠️ Issues Found

### 🔴 Critical (Must Fix)
1. **XSS vulnerability** - Need to sanitize HTML in user inputs
   File: src/middleware/validation.js:8

### 🟡 Important (Should Fix)
1. **Boolean validation issue** - String "true" not converted to boolean
2. **Missing empty update validation** - PUT with {} succeeds but does nothing

### 🟢 Nice-to-have (Consider)
1. **Add API versioning** - Consider /api/v1/tasks for future flexibility
2. **Add pagination** - For production use with many tasks
```

#### Step 6: Developer Fixes Issues

**Developer addresses all feedback:**
- ✅ Added XSS sanitization using `xss` package
- ✅ Fixed boolean validation with `.toBoolean()`
- ✅ Added empty update body validation
- ✅ Enhanced tests for all fixes

**Pushes fixes to same PR branch**

#### Step 7: Automatic Re-review

**@claude automatically reviews the fixes:**
```markdown
## 📋 Summary
All issues from the previous review have been addressed. The implementation
now follows all the architecture recommendations and security best practices.

**Recommendation:** ✅ **APPROVED** - Ready to merge

## ✅ What's Good
- ✅ All critical security issues fixed
- ✅ XSS sanitization properly implemented
- ✅ Validation working correctly
- ✅ Tests updated and passing

## ⚠️ Issues Found
### 🔴 Critical (Must Fix)
**None** - All critical issues resolved! 🎉
```

#### Step 8: Merge

✅ **PR merged to main**

---

## 🔍 Viewing the Prompts

### Where to See Issue Planning Prompt

**In the issue itself:**
1. Go to your GitHub issue (e.g., Issue #1)
2. Read your @claude mention comment
3. See @claude's response

**Example URL:**
```
https://github.com/your-org/your-repo/issues/1
```

### Where to See PR Review Prompt

There are **3 ways** to view the PR review prompt:

#### Method 1: Workflow File (Template)

**File:** `.github/workflows/claude-code-review.yml`
**Lines:** 91-139 (approximately)

```bash
# View the prompt template
cat .github/workflows/claude-code-review.yml | sed -n '91,139p'
```

This shows the **template** with variables like:
- `${{ github.repository }}` → `your-org/your-repo`
- `${{ github.event.pull_request.number }}` → `2`
- `${{ github.event.pull_request.user.login }}` → `username`

#### Method 2: GitHub Actions UI (Actual Prompt Sent)

1. Go to **Actions** tab in your repository
2. Click on the workflow run (e.g., "feat: implement task creation endpoint")
3. Click on the job **"claude-review"**
4. Expand the step **"Run Claude Code Review"**
5. Scroll to see the full prompt that was sent to @claude

**Example URL:**
```
https://github.com/your-org/your-repo/actions/runs/19545389108
```

#### Method 3: Command Line (After Run Completes)

```bash
# List recent workflow runs
gh run list --workflow=claude-code-review.yml --limit 5

# View logs from a specific run
gh run view 19545389108 --log

# Search for the prompt in logs
gh run view 19545389108 --log | grep -A 50 "REPOSITORY:"
```

### Example of Actual Prompt Sent

For PR #2 in `PankajTanwar7/task-manager-demo`, the actual prompt sent was:

```
REPOSITORY: PankajTanwar7/task-manager-demo
PR NUMBER: 2
AUTHOR: @PankajTanwar7
TITLE: feat: implement task creation endpoint

Please review this pull request and provide structured feedback.

Use the repository's CLAUDE.md file (if it exists) for project-specific guidance on:
- Code style and conventions
- Testing requirements
- Security standards
- Performance expectations

Provide your review in this format:

## 📋 Summary
[Brief overview of what this PR does and overall assessment]

## ✅ What's Good
- [Highlight positive aspects and good practices]

... (rest of structured template)
```

Plus @claude has access to:
- All PR file changes (diff)
- CLAUDE.md file (project-specific guidelines)
- PR description and metadata
- Commit history

---

## ✅ Best Practices

### For Issue Planning (@claude)

**Do:**
- ✅ Ask specific architecture questions
- ✅ Provide context (tech stack, constraints, requirements)
- ✅ Include acceptance criteria
- ✅ Mention performance/security needs
- ✅ Ask for project structure recommendations

**Don't:**
- ❌ Ask vague questions ("How do I build an API?")
- ❌ Forget to mention constraints
- ❌ Skip acceptance criteria
- ❌ Ask for implementation details (that's for Phase 2)

**Example Good Question:**
```markdown
@claude Help design authentication for a Node.js API

**Requirements:**
- JWT tokens with refresh mechanism
- Password hashing with bcrypt
- Session management (Redis)
- Rate limiting on login attempts

**Constraints:**
- Max 100ms response time
- Must support 1000 concurrent users
- Security: OWASP top 10 compliance

**Questions:**
1. What's the best JWT library for Node.js?
2. How should I structure the auth middleware?
3. What's the recommended token expiry strategy?
4. How to handle token refresh securely?
```

### For PR Reviews (@claude)

**Do:**
- ✅ Keep CLAUDE.md file updated with project standards
- ✅ Address critical issues immediately
- ✅ Consider important suggestions seriously
- ✅ Discuss nice-to-have items with team
- ✅ Push fixes to trigger re-review
- ✅ Reference specific file paths in responses

**Don't:**
- ❌ Ignore critical issues
- ❌ Merge without approval
- ❌ Skip re-review after major fixes
- ❌ Argue with valid security concerns

### For Both

**Maintain consistency:**
- ✅ Use same terminology in issues and PRs
- ✅ Reference the original issue in PR description
- ✅ Keep CLAUDE.md in sync with architecture decisions
- ✅ Document major decisions in issues

---

## 🔧 Troubleshooting

### Issue: @claude's Review Doesn't Match Its Design Advice

**Problem:** @claude suggested Express.js in the issue but criticized it in the review.

**Solution:**
1. Check if you actually followed @claude's advice
2. Verify CLAUDE.md doesn't contradict issue advice
3. If still inconsistent, mention this to @claude:
   ```markdown
   @claude In Issue #1 you recommended Express.js, but now you're suggesting
   Fastify. Can you clarify which is better for our use case?
   ```

### Issue: @claude Doesn't Remember Issue Context

**Problem:** PR review seems to ignore the architecture discussion from the issue.

**Solution:**
1. Link the issue in PR description: `Closes #1`
2. Add context in PR description:
   ```markdown
   ## Architecture
   Following @claude's recommendations from #1:
   - Express.js framework
   - Layered architecture (routes → controllers → models)
   - express-validator for validation
   ```
3. Update CLAUDE.md with key decisions

### Issue: Workflow Doesn't Trigger

**Problem:** Pushed to PR but no automatic review appeared.

**Solutions:**
1. Check workflow file exists in main branch:
   ```bash
   git ls-tree main -- .github/workflows/claude-code-review.yml
   ```
2. Check PR size didn't exceed threshold (default: 2000 lines)
3. Check workflow run logs:
   ```bash
   gh run list --workflow=claude-code-review.yml --limit 5
   gh run view <run-id>
   ```
4. Verify `CLAUDE_CODE_OAUTH_TOKEN` secret is set:
   ```bash
   gh secret list
   ```

### Issue: Prompts Are Out of Sync

**Problem:** @claude reviews don't align with project standards.

**Solution:**
1. Update CLAUDE.md with latest standards
2. Update workflow prompt template if needed
3. Add project-specific guidelines to CLAUDE.md:
   ```markdown
   ## Our Specific Standards
   - Always use TypeScript (not JavaScript)
   - 100% test coverage required
   - All API endpoints must have OpenAPI docs
   ```

---

## 📚 Additional Resources

### Related Documentation
- [WORKFLOW.md](./WORKFLOW.md) - Complete workflow guide
- [GITHUB-CLAUDE-SETUP.md](./GITHUB-CLAUDE-SETUP.md) - Setting up @claude
- [CLAUDE-MD-GUIDE.md](./CLAUDE-MD-GUIDE.md) - Customizing CLAUDE.md
- [QUICKREF.md](./QUICKREF.md) - Quick command reference

### Workflow Files
- `.github/workflows/claude.yml` - Manual @claude mentions
- `.github/workflows/claude-code-review.yml` - Automatic PR reviews
- `CLAUDE.md` - Project-specific guidelines for @claude

### Scripts
- `scripts/start-work.sh` - Generate implementation prompt from issue

---

## 🎉 Summary

The magic of this system is the **closed feedback loop**:

```
@claude designs → You implement → @claude validates → You fix → @claude approves
```

Both prompts work together because:
1. **Same AI** provides advice and reviews
2. **Shared context** through CLAUDE.md and issue links
3. **Consistent standards** applied throughout
4. **Sequential workflow** ensures design matches implementation
5. **Automatic re-review** ensures fixes are verified

This creates a **self-consistent development workflow** where architecture decisions are automatically validated during code review.

**Result:** Higher quality code, fewer architectural mismatches, and consistent standards across your entire codebase.

---

**Last Updated:** 2025-11-21

---

*Questions? Ask @claude in a GitHub issue or check [WORKFLOW.md](./WORKFLOW.md) for more details!*
