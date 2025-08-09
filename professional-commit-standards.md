# Professional Commit Standards

## Conventional Commits Specification

### Commit Message Format
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Required Elements

**Type** (Required):
```
feat     # New feature for the user
fix      # Bug fix for the user  
docs     # Documentation changes
style    # Formatting, missing semi colons, etc (no code change)
refactor # Refactoring production code
test     # Adding missing tests, refactoring tests
chore    # Updating build tasks, package manager configs, etc
```

**Description** (Required):
- Use imperative mood ("add" not "added" or "adds")
- Don't capitalize first letter
- No period at the end
- Maximum 50 characters

### Examples

**Basic Commits:**
```bash
feat: add user authentication system
fix: resolve login form validation error
docs: update API endpoint documentation
style: format code according to style guide
refactor: extract user service into separate module
test: add unit tests for payment processing
chore: update dependencies to latest versions
```

**With Scope:**
```bash
feat(auth): implement JWT token refresh
fix(ui): resolve navigation menu overflow issue
docs(api): add authentication examples
test(user): add integration tests for user service
```

**With Body and Footer:**
```bash
feat(auth): implement OAuth 2.0 integration

Add support for Google and GitHub OAuth providers.
Users can now sign in using their existing accounts
from these platforms, improving user experience
and reducing friction in the registration process.

Closes #123
Co-authored-by: Jane Smith <jane@example.com>
```

## Advanced Commit Types

### Breaking Changes
```bash
feat!: redesign authentication API

BREAKING CHANGE: The authentication endpoint has been
redesigned. The old POST /auth/login is now POST /v2/auth
and requires different request parameters.

Old format: { username, password }
New format: { email, password, remember }
```

### Work in Progress
```bash
# Temporary commits (should be squashed before merge)
wip: implement user dashboard layout
wip: add search functionality (incomplete)
```

### Dependency Updates  
```bash
chore(deps): bump react from 17.0.2 to 18.2.0
chore(deps-dev): bump eslint from 8.0.0 to 8.52.0
```

### Security Fixes
```bash
fix(security): patch XSS vulnerability in comment system

Sanitize user input in comment rendering to prevent
script injection attacks.

CVE-2023-1234
```

## Commit Message Best Practices

### ✅ Good Commit Messages
```bash
feat(user): implement user profile editing
fix(auth): resolve token expiration handling
docs: add installation instructions to README
refactor(api): extract database connection logic
test(payment): add edge cases for payment processing
perf(search): optimize database queries for search
```

### ❌ Poor Commit Messages
```bash
update stuff
fix bug
more changes
WIP
asdf
quick fix
commit
changes
update
```

### Multi-line Commit Template
```bash
# Title: summarize change in 50 characters or less

# Explain what this commit does and why (wrap at 72 chars)
# - What was the problem?
# - How does this solve it?
# - Any side effects or considerations?

# List any breaking changes or important notes
# Reference any relevant issues or tickets

# Co-authored-by: name <email>
# Closes #issue-number
```

## Commit Organization Strategies

### Atomic Commits
Each commit should represent **one logical change**:

```bash
# ✅ Good - Single purpose commits
feat(auth): add login form component
feat(auth): implement login API integration  
feat(auth): add error handling for failed login
feat(auth): add loading state to login form

# ❌ Poor - Mixed purposes in one commit
feat(auth): add login form, fix navigation bug, update README
```

### Logical Grouping
```bash
# User Management Feature
feat(user): create user model and database schema
feat(user): implement user registration API
feat(user): add user profile creation form
feat(user): implement user profile validation
test(user): add comprehensive user service tests
docs(user): document user management API endpoints
```

### Progressive Enhancement
```bash
feat(dashboard): create basic dashboard layout
feat(dashboard): add data visualization components
feat(dashboard): implement real-time data updates
feat(dashboard): add filtering and search capabilities
perf(dashboard): optimize dashboard rendering performance
```

## Advanced Git Commit Patterns

### Squashing Commits for Clean History
```bash
# Before squashing (messy development history)
fix: typo in login form
feat: add login functionality  
fix: resolve linting errors
fix: another typo
feat: improve login validation
fix: remove debug console.logs

# After squashing (clean feature commit)
feat(auth): implement user login with validation

Added complete login functionality including:
- Email/password authentication
- Client-side and server-side validation
- Error handling and user feedback
- Loading states and accessibility features

Closes #456
```

### Interactive Rebase for Commit Cleanup
```bash
git rebase -i HEAD~4

# Interactive editor opens:
pick a1b2c3d feat(auth): add login form
squash e4f5g6h fix: typo in form validation  
squash h7i8j9k fix: remove console.log statements
pick k0l1m2n feat(auth): implement logout functionality

# Results in clean commits:
# feat(auth): add login form
# feat(auth): implement logout functionality
```

### Commit Message Templates

**Feature Development Template:**
```bash
feat(<scope>): <brief description>

## What
- Brief explanation of what was implemented

## Why  
- Problem this solves or value it provides

## How
- Key implementation details or approach

## Testing
- How this was tested
- Any edge cases considered

Closes #<issue-number>
```

**Bug Fix Template:**
```bash
fix(<scope>): <brief description>

## Problem
- Description of the bug
- Steps to reproduce (if not obvious)

## Solution
- How the fix works
- Why this approach was chosen

## Impact
- Who/what is affected
- Any side effects or considerations

Fixes #<issue-number>
```

## Team Standards and Enforcement

### Git Hooks for Commit Standards
**Pre-commit Hook (.git/hooks/pre-commit):**
```bash
#!/bin/sh
# Check commit message format
commit_msg_file=$1
commit_msg=$(cat $commit_msg_file)

# Conventional commit pattern
pattern="^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .{1,50}$"

if ! echo "$commit_msg" | grep -qE "$pattern"; then
    echo "❌ Invalid commit message format!"
    echo "Expected: <type>[optional scope]: <description>"
    echo "Example: feat(auth): add user authentication"
    exit 1
fi
```

**Commit Message Template (.gitmessage):**
```bash
# <type>[optional scope]: <description>
# 
# [optional body]
#
# [optional footer]

# Type must be one of:
# feat: A new feature
# fix: A bug fix  
# docs: Documentation only changes
# style: Changes that don't affect meaning of code
# refactor: Code change that neither fixes bug nor adds feature
# test: Adding missing tests
# chore: Changes to build process or auxiliary tools
```

### Enforcing Standards with Tools

**commitizen** - Interactive commit message creation:
```bash
npm install -g commitizen
npm install -g cz-conventional-changelog

# Use instead of git commit
git cz
```

**commitlint** - Lint commit messages:
```bash
npm install --save-dev @commitlint/{config-conventional,cli}

# .commitlintrc.js
module.exports = {extends: ['@commitlint/config-conventional']};
```

**husky** - Git hooks made easy:
```bash
npm install --save-dev husky
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit $1'
```

## Repository-Specific Standards

### Monorepo Commit Standards
```bash
feat(web): add user dashboard component
feat(api): implement user authentication endpoint
feat(mobile): add push notification support
fix(shared): resolve date formatting utility bug
```

### Microservices Commit Standards
```bash
feat(user-service): implement user registration
feat(payment-service): add Stripe integration
fix(notification-service): resolve email delivery issue
chore(infrastructure): update Docker configurations
```

### Documentation Standards
```bash
docs: add getting started guide
docs(api): update authentication endpoint examples  
docs(contributing): add commit message guidelines
docs(deployment): update production deployment steps
```

## Advanced Commit Strategies

### Semantic Versioning Integration
```bash
# Patch version bump (1.0.0 -> 1.0.1)
fix(auth): resolve password validation issue

# Minor version bump (1.0.0 -> 1.1.0)  
feat(dashboard): add data export functionality

# Major version bump (1.0.0 -> 2.0.0)
feat!: redesign authentication system
BREAKING CHANGE: Auth API endpoints have changed
```

### Release Commits
```bash
chore(release): bump version to 2.1.0

## Features
- feat(auth): implement OAuth 2.0 support
- feat(ui): add dark mode toggle
- feat(api): add user preferences endpoint

## Bug Fixes  
- fix(login): resolve session timeout issue
- fix(ui): correct responsive layout problems

## Breaking Changes
- feat!: update API response format for user data
```

### Hotfix Commits
```bash
fix(security): patch critical XSS vulnerability

Immediate security patch for user-generated content
rendering. All user inputs are now properly sanitized
before display to prevent script injection.

This affects all user-facing content areas including:
- Comments
- Profile descriptions  
- Post titles

CVE-2023-5678
Priority: Critical
```

## Commit History Analysis

### Generating Changelogs from Commits
```bash
# Using conventional-changelog
npm install -g conventional-changelog-cli
conventional-changelog -p angular -i CHANGELOG.md -s

# Using git-cliff
git cliff --output CHANGELOG.md
```

### Useful Git Log Commands
```bash
# Beautiful one-line format
git log --oneline --decorate --graph

# Filter by type
git log --grep="feat:" --oneline

# Show commits by author
git log --author="John Doe" --oneline

# Commits in date range
git log --since="2023-01-01" --until="2023-12-31" --oneline
```

This comprehensive guide ensures your commits are professional, traceable, and contribute to excellent project documentation!