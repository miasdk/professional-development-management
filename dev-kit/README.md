# Dev-Kit - Epic-Based Project Bootstrap

Copy this entire folder into any new project for instant professional structure with epic-based project management.

## Quick Start

```bash
# 1. Copy dev-kit to your new project
cp -r dev-kit/ /path/to/new-project/

# 2. Fill out project context (2 minutes)
vim SETUP.md

# 3. Initialize project structure
./scripts/init-project.sh "My Project Name"

# 4. Start coding with epic management ready
```

## What You Get

### Scripts (Automation)
- `init-project.sh` - Bootstrap project structure
- `create-epics.sh` - Generate GitHub epics/issues  
- `daily-update.sh` - Update progress on GitHub issues

### Templates (Copy & Customize)
- `README-PROJECT.md` - Professional portfolio README
- `epic-template.md` - Sprint/epic structure
- `pr-template.md` - Pull request format
- `daily-update.md` - Progress tracking format
- `.gitignore` - Essential ignore patterns
- `.env.example` - Environment variables template

### Quick Reference (Look Up Fast)
- `git-guide.md` - Essential commands + conventional commits
- `learning-resources.md` - Curated learning links

## Daily Workflow

```bash
# Morning: Check current epic
gh issue view 1

# Throughout day: Code...

# End of day: Update progress  
./scripts/daily-update.sh 1 "3h" "Built auth system, added tests"
```

## Project Structure After Init

```
my-project/
├── README.md              # Professional portfolio README
├── .gitignore            # Essential ignore patterns
├── .env.example          # Environment template
├── SETUP.md              # Project context for AI agents
└── dev-kit/              # This folder (keep for reference)
```

Copy, fill SETUP.md, run scripts, start coding. That's it.