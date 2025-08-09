# Git Workflow Guide - Aligned with Gogentic AI Standards

## Primary Workflow: GitHub Flow

Following your [GitHub Flow Guide](https://docs.github.com/en/get-started/quickstart/github-flow) (line 6) and [Atlassian Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) (line 12).

### GitHub Flow (Your Primary Workflow)
**Best for**: Continuous deployment, small-medium teams, web applications

```
main (always deployable)
├── feature/add-user-profiles
├── feature/improve-search
├── bugfix/login-error
└── hotfix/security-patch
```

**Simple Workflow**:
1. Create feature branch from `main`
2. Work on feature with regular commits
3. Open Pull Request when ready
4. Code review and discussion
5. Deploy to staging for testing
6. Merge to `main` and deploy to production

**GitHub Flow Commands**:
```bash
# Create and switch to feature branch
git checkout -b feature/user-profiles

# Regular development
git add .
git commit -m "feat: add user profile creation form"
git push -u origin feature/user-profiles

# Create PR via GitHub UI, then after approval:
git checkout main
git pull origin main
git branch -d feature/user-profiles
```

### Alternative: Feature Branch Workflow (Atlassian)
**Best for**: Teams wanting structured branching without complexity

Following [Atlassian's Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow):

```
main (central repository)
├── feature/user-authentication
├── feature/dashboard-redesign
├── fix/login-validation
└── docs/api-documentation
```

**Key Principles**:
- All features developed in dedicated branches
- Never commit directly to `main`
- Use Pull Requests for code review
- Maintain linear, clean history

## Branch Naming Conventions

### Standard Prefixes
```bash
feature/    # New features
bugfix/     # Bug fixes  
hotfix/     # Critical production fixes
release/    # Release preparation
chore/      # Maintenance tasks
docs/       # Documentation updates
test/       # Adding or updating tests
refactor/   # Code refactoring
style/      # Code style changes
```

### Naming Best Practices
```bash
# ✅ Good examples
feature/user-authentication
feature/payment-integration
bugfix/login-form-validation
hotfix/security-vulnerability-CVE-2023-1234
chore/update-dependencies
docs/api-endpoint-documentation

# ❌ Poor examples  
feature/stuff
fix/bug
my-feature
test123
```

### Branch Name Format
```
<type>/<short-description>
<type>/<ticket-number>-<short-description>
<type>/<scope>/<description>

Examples:
feature/user-profile-creation
bugfix/PROJ-123-login-error
feature/auth/password-reset
```

## Merge Strategies

### 1. Merge Commit (Default)
**Pros**: Preserves complete history, shows branch context
**Cons**: Can create complex history graphs

```bash
git checkout main
git merge feature/user-auth
# Creates merge commit with both parent commits
```

**Result**:
```
* Merge branch 'feature/user-auth' into main
|\
| * feat: add password validation
| * feat: implement login form
|/
* Previous commit on main
```

### 2. Squash and Merge
**Pros**: Clean linear history, combines related commits
**Cons**: Loses individual commit history from feature branch

```bash
git checkout main
git merge --squash feature/user-auth
git commit -m "feat: implement user authentication system"
```

**Result**:
```
* feat: implement user authentication system
* Previous commit on main
```

### 3. Rebase and Merge
**Pros**: Linear history, preserves individual commits
**Cons**: Rewrites history, can be complex for beginners

```bash
git checkout feature/user-auth
git rebase main
git checkout main  
git merge feature/user-auth --ff-only
```

**Result**:
```
* feat: add password validation
* feat: implement login form  
* Previous commit on main
```

## Pull Request Best Practices

Following [GitHub's Pull Request Best Practices](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/getting-started/best-practices-for-pull-requests) (line 8) and [Google's Code Review Practices](https://google.github.io/eng-practices/review/) (line 13).

### PR Title Format
```
<type>(<scope>): <description>

Examples:
feat(auth): implement user registration system
fix(ui): resolve navigation menu overflow issue  
docs(api): update authentication endpoint documentation
```

### PR Description Template
```markdown
## Summary
Brief description of what this PR accomplishes.

## Changes Made
- [ ] Specific change 1
- [ ] Specific change 2
- [ ] Specific change 3

## Type of Change
- [ ] 🐛 Bug fix (non-breaking change)
- [ ] ✨ New feature (non-breaking change)  
- [ ] 💥 Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] 📝 Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed
- [ ] Cross-browser testing (if applicable)

## Screenshots/Videos
[Include relevant screenshots or GIFs demonstrating the changes]

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Code is commented where necessary
- [ ] Documentation updated
- [ ] No new warnings introduced

## Related Issues
Closes #123
Relates to #456
```

### Code Review Guidelines

**For Authors**:
- Keep PRs small (< 400 lines of changes)
- Write clear, descriptive titles and descriptions
- Test your changes thoroughly
- Respond to feedback promptly and professionally
- Update the PR based on feedback

**For Reviewers**:
- Review within 24-48 hours
- Focus on logic, security, performance, and maintainability
- Be constructive and specific in feedback
- Approve when ready, request changes when needed
- Consider the bigger picture and architectural implications

**Review Checklist**:
- [ ] Does the code solve the intended problem?
- [ ] Is the code readable and well-documented?
- [ ] Are there any obvious bugs or edge cases?
- [ ] Does it follow team coding standards?
- [ ] Are there adequate tests?
- [ ] Could this impact performance or security?
- [ ] Is the approach consistent with existing patterns?

## Advanced Git Workflows

### Feature Flags with Git
```bash
# Long-running feature branch
git checkout -b feature/new-dashboard
# Regular commits with feature flag protection
git commit -m "feat: add dashboard component (behind feature flag)"

# Merge early, enable feature later
git checkout main
git merge feature/new-dashboard
# Feature remains disabled until flag is toggled
```

### Release Branches
```bash
# Create release branch from develop
git checkout develop
git checkout -b release/v2.1.0

# Bug fixes and final preparations
git commit -m "fix: resolve critical issue for v2.1.0"

# Merge to both main and develop
git checkout main
git merge release/v2.1.0
git tag v2.1.0

git checkout develop  
git merge release/v2.1.0
```

### Emergency Hotfix Workflow
```bash
# Create hotfix from main
git checkout main
git checkout -b hotfix/security-patch

# Fix critical issue
git commit -m "fix: patch security vulnerability CVE-2023-1234"

# Deploy and test
git push origin hotfix/security-patch

# Merge to main and develop
git checkout main
git merge hotfix/security-patch
git tag v1.2.1

git checkout develop
git merge hotfix/security-patch
```

## Team Collaboration Patterns

### Daily Development Workflow
```bash
# Start of day - sync with remote
git checkout main
git pull origin main

# Create feature branch
git checkout -b feature/improve-search

# Work with regular commits
git add .
git commit -m "feat: add search filters"
git push -u origin feature/improve-search

# End of day - push progress
git add .
git commit -m "wip: implement search suggestions"
git push origin feature/improve-search
```

### Handling Merge Conflicts
```bash
# When conflict occurs during merge/rebase
git status  # Shows conflicted files

# Resolve conflicts in editor, then:
git add conflicted-file.js
git commit -m "resolve: merge conflict in search component"

# For rebase conflicts:
git add conflicted-file.js  
git rebase --continue
```

### Collaborative Feature Development
```bash
# Multiple developers on same feature
git checkout -b feature/payment-system

# Developer A pushes changes
git push origin feature/payment-system

# Developer B syncs and contributes
git fetch origin
git checkout feature/payment-system
git pull origin feature/payment-system
# Make changes
git push origin feature/payment-system
```

## Workflow Selection for Gogentic AI

### GitHub Flow (Recommended - Your Primary Choice)
**Perfect for Gogentic AI because:**
- Educational AI startup environment
- React/TypeScript + Python tech stack
- 20hrs/week remote development
- Fast iteration on educational features
- Simple CI/CD with GitHub Actions (lines 17-20)
- Integrates with Jira project management (lines 36-40)

### When to Use Feature Branch Workflow:
- Complex educational features requiring isolation
- Compliance-sensitive changes (FERPA/COPPA - lines 94-98)
- Multi-developer collaboration on large features
- AI agent development requiring extensive testing (lines 69-85)

## Common Anti-Patterns to Avoid

### ❌ Poor Practices
```bash
# Long-lived branches without syncing
git checkout feature/big-feature
# Works for weeks without merging main

# Unclear commit messages
git commit -m "fix stuff"
git commit -m "more changes"

# Direct commits to main
git checkout main
git commit -m "quick fix"

# Large, unfocused PRs
# 50+ files changed across multiple features
```

### ✅ Best Practices
```bash
# Regular syncing with main
git checkout feature/user-auth
git merge main  # or rebase main

# Clear, descriptive commits  
git commit -m "feat(auth): implement JWT token validation"
git commit -m "fix(login): resolve password reset email issue"

# Feature branch workflow
git checkout -b feature/specific-feature
# Work, commit, push, create PR

# Small, focused PRs
# 1-5 files, single responsibility, clear purpose
```