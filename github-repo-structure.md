# GitHub Work Repository Structure

## Setup Time: 15 minutes

### Repository Creation
**Repository Name**: `gogentic-work-projects`
**Description**: Personal workspace for development projects at Gogentic AI
**Visibility**: Private (recommended for work projects)

## Professional Folder Structure

```
gogentic-work-projects/
├── frontend/
│   ├── components/
│   ├── pages/
│   ├── utils/
│   └── tests/
├── backend/
│   ├── api/
│   ├── models/
│   ├── utils/
│   └── tests/
├── docs/
│   └── meeting-notes/
├── scripts/
└── .github/
    └── workflows/
```

## Essential Files to Create

### .gitignore
```
# Dependencies
node_modules/
__pycache__/
*.pyc

# Environment
.env
.env.local

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Build
dist/
build/
*.log
```

### README.md
```markdown
# Gogentic AI Work Projects

Personal workspace for development projects at Gogentic AI.

## Structure
- `frontend/` - React/TypeScript components and pages
- `backend/` - Python API and services
- `docs/` - Documentation and meeting notes
- `scripts/` - Utility scripts

## Getting Started
```bash
# Frontend setup
cd frontend && npm install

# Backend setup  
cd backend && pip install -r requirements.txt
```

## Branch Workflow
- `main` - production ready code
- `feature/[task-name]` - feature development
- `fix/[issue-name]` - bug fixes

## Development Guidelines
- Write clear commit messages
- Create feature branches for all changes
- Test before pushing to main
- Document significant changes
```

### Basic GitHub Actions (.github/workflows/basic-ci.yml)
```yaml
name: Basic CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
        working-directory: ./frontend
      - run: npm test
        working-directory: ./frontend
```

## Branch Workflow Best Practices

### Creating Feature Branches
```bash
# Create new feature branch
git checkout -b feature/user-authentication

# Work on feature, commit changes
git add .
git commit -m "Add user login component"

# Push and create PR
git push -u origin feature/user-authentication
```

### Commit Message Format
```
type: brief description

- More detailed explanation if needed
- Use bullet points for multiple changes
- Reference JIRA ticket: PWT-123
```

**Types**: feat, fix, docs, style, refactor, test, chore

## Quick Setup Commands
```bash
# Initialize repository
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/[username]/gogentic-work-projects.git
git push -u origin main
```