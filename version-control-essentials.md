# Version Control Essentials - Advanced Git Operations

## Advanced Git Operations for Professional Development

Following your [Google Engineering Practices](https://google.github.io/eng-practices/) (line 117) and [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/comparing-workflows) (line 11) resources.

## Interactive Rebase (History Cleanup)

### Cleaning Up Feature Branch History
```bash
# View commit history
git log --oneline -10

# Interactive rebase last 4 commits
git rebase -i HEAD~4

# Editor opens with options:
pick a1b2c3d feat(auth): add login component
squash e4f5g6h fix: typo in login form
squash h7i8j9k fix: remove console.log
pick k0l1m2n feat(auth): add logout functionality

# Results in clean commits:
# feat(auth): add login component
# feat(auth): add logout functionality
```

### Rebase vs Merge Strategy
```bash
# Rebase feature branch (clean linear history)
git checkout feature/user-dashboard
git rebase main
git checkout main
git merge feature/user-dashboard --ff-only

# Merge with commit (preserves branch context)
git checkout main
git merge feature/user-dashboard

# Squash merge (single commit)
git merge feature/user-dashboard --squash
git commit -m "feat(dashboard): implement user dashboard system"
```

## Advanced Branch Management

### Working with Remote Branches
```bash
# Fetch all remote branches
git fetch --all

# Track remote branch locally
git checkout -b feature/new-feature origin/feature/new-feature

# Push new branch to remote
git push -u origin feature/new-feature

# Delete remote branch
git push origin --delete feature/completed-feature

# Prune deleted remote branches locally
git remote prune origin
```

### Branch Comparison and Analysis
```bash
# Compare branches
git diff main..feature/user-auth

# See commits unique to feature branch
git log main..feature/user-auth --oneline

# See all branches merged into main
git branch --merged main

# See unmerged branches
git branch --no-merged main

# Branch creation history
git reflog show --all
```

## Conflict Resolution Strategies

### Merge Conflict Resolution
```bash
# When conflicts occur during merge
git status  # Shows conflicted files

# Edit conflicted files, then:
git add conflicted-file.js
git commit  # Completes merge

# Abort merge if needed
git merge --abort
```

### Rebase Conflict Resolution
```bash
# During rebase conflicts
git status  # Shows conflict details

# Resolve conflicts, then:
git add resolved-file.js
git rebase --continue

# Skip problematic commit
git rebase --skip

# Abort rebase entirely
git rebase --abort
```

### Advanced Conflict Tools
```bash
# Use visual merge tool
git mergetool

# Show conflict in three-way format
git show :1:filename  # Base version
git show :2:filename  # Current branch
git show :3:filename  # Incoming branch

# Resolve using specific version
git checkout --ours filename    # Keep current branch version
git checkout --theirs filename  # Use incoming branch version
```

## Git Stash Management

### Stashing Work in Progress
```bash
# Stash current changes
git stash push -m "WIP: implementing user dashboard"

# Stash including untracked files
git stash push -u -m "WIP: new feature with new files"

# List all stashes
git stash list

# Apply specific stash
git stash apply stash@{1}

# Pop most recent stash (apply and remove)
git stash pop

# Drop specific stash
git stash drop stash@{2}

# Show stash contents
git stash show -p stash@{0}
```

### Selective Stashing
```bash
# Stash only specific files
git stash push -m "partial work" src/components/Login.tsx

# Interactive stashing
git stash -p  # Choose hunks to stash

# Create branch from stash
git stash branch feature/stashed-work stash@{1}
```

## Advanced Git History

### Git Reflog (Recovery Operations)
```bash
# View all Git operations
git reflog

# Recover deleted branch
git reflog  # Find commit hash
git checkout -b recovered-branch a1b2c3d

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Recover from hard reset
git reflog
git reset --hard HEAD@{1}
```

### Cherry-picking Commits
```bash
# Apply specific commit to current branch
git cherry-pick a1b2c3d

# Cherry-pick range of commits
git cherry-pick main~4..main~2

# Cherry-pick without committing
git cherry-pick --no-commit a1b2c3d

# Continue after resolving conflicts
git cherry-pick --continue

# Abort cherry-pick
git cherry-pick --abort
```

## Git Hooks for Automation

### Pre-commit Hook (.git/hooks/pre-commit)
```bash
#!/bin/sh
# Run linting before commit
npm run lint
if [ $? -ne 0 ]; then
    echo "❌ Linting failed! Please fix errors before committing."
    exit 1
fi

# Run tests
npm run test
if [ $? -ne 0 ]; then
    echo "❌ Tests failed! Please fix tests before committing."
    exit 1
fi

echo "✅ Pre-commit checks passed!"
```

### Commit Message Hook (.git/hooks/commit-msg)
```bash
#!/bin/sh
# Validate conventional commit format
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

### Using Husky for Hook Management
```bash
# Install husky
npm install --save-dev husky

# Initialize husky
npx husky install

# Add pre-commit hook
npx husky add .husky/pre-commit "npm run lint && npm run test"

# Add commit-msg hook for conventional commits
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit $1'
```

## Git Bisect (Bug Hunting)

### Finding the Commit that Introduced a Bug
```bash
# Start bisect session
git bisect start

# Mark current commit as bad
git bisect bad

# Mark known good commit
git bisect good a1b2c3d

# Git will checkout middle commit
# Test the commit, then:
git bisect good  # If commit is good
git bisect bad   # If commit is bad

# Git continues narrowing down
# When found:
git bisect reset  # Return to original HEAD
```

### Automated Bisect
```bash
# Run automated test during bisect
git bisect start HEAD a1b2c3d
git bisect run npm test

# Git will automatically find the breaking commit
```

## Advanced GitHub Integration

### Working with GitHub CLI
```bash
# Install GitHub CLI
brew install gh  # macOS
# or
npm install -g @github/cli

# Authenticate
gh auth login

# Create PR from command line
gh pr create --title "feat(auth): implement OAuth" --body "Adds OAuth integration"

# View PR status
gh pr status

# Checkout PR locally
gh pr checkout 123

# Merge PR
gh pr merge 123 --merge  # or --squash or --rebase
```

### GitHub Actions Integration
```bash
# Trigger workflow from commit message
git commit -m "feat(api): add new endpoint

[trigger: deploy-staging]"

# Skip CI with commit message
git commit -m "docs: update README [skip ci]"

# Create release tag
git tag -a v1.2.0 -m "Release version 1.2.0"
git push origin v1.2.0
```

## Git Configuration for Teams

### Team Git Configuration
```bash
# Set up team-wide configurations
git config --global user.name "Your Name"
git config --global user.email "your.email@gogentic.ai"

# Set up pull strategy
git config --global pull.rebase true

# Set up default branch
git config --global init.defaultBranch main

# Set up editor
git config --global core.editor "code --wait"

# Set up merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'

# Show branch in prompt
git config --global color.ui auto
```

### Repository-specific Configuration
```bash
# Set up repository templates
git config --global commit.template ~/.gitmessage

# Set up hooks path
git config --global core.hooksPath ~/.git-hooks

# GPG signing (for security)
git config --global user.signingkey YOUR_GPG_KEY
git config --global commit.gpgsign true
```

## Troubleshooting Common Issues

### Large Repository Management
```bash
# Clone with limited history
git clone --depth 1 https://github.com/user/repo.git

# Fetch more history later
git fetch --unshallow

# Clean up repository
git gc --aggressive --prune=now

# Remove large files from history
git filter-branch --tree-filter 'rm -f large-file.zip' HEAD
# Modern alternative:
git filter-repo --path large-file.zip --invert-paths
```

### Submodule Management
```bash
# Add submodule
git submodule add https://github.com/user/repo.git external/repo

# Initialize submodules after clone
git submodule init
git submodule update

# Clone with submodules
git clone --recursive https://github.com/user/main-repo.git

# Update submodules
git submodule update --remote --merge

# Remove submodule
git submodule deinit external/repo
git rm external/repo
```

### Performance Optimization
```bash
# Enable file system monitor for large repos
git config core.fsmonitor true

# Enable parallel processing
git config submodule.fetchJobs 4

# Optimize for large files
git config core.preloadindex true
git config core.fscache true

# Partial clone (Git 2.19+)
git clone --filter=blob:none https://github.com/user/repo.git
```

## Integration with Development Tools

### VS Code Git Integration
```json
// .vscode/settings.json
{
  "git.enableSmartCommit": true,
  "git.autofetch": true,
  "git.confirmSync": false,
  "git.defaultCloneDirectory": "~/code",
  "gitlens.currentLine.enabled": false,
  "gitlens.hovers.currentLine.over": "line"
}
```

### Jira Integration (Lines 36-40)
```bash
# Commit message with Jira ticket
git commit -m "feat(auth): implement SSO integration

Add single sign-on support for enterprise users.
Includes SAML 2.0 and OAuth 2.0 providers.

Closes PROJ-123
Relates to PROJ-456"

# Branch naming with Jira tickets
git checkout -b feature/PROJ-123-sso-integration
```

This comprehensive guide covers all advanced Git operations needed for professional development at Gogentic AI, perfectly aligned with your learning resources and workflow standards!