# JIRA Setup Guide

## Setup Time: 20 minutes

### Initial Project Setup

1. **Project Creation**:
   - **Project Name**: "Personal Work Tracking"
   - **Project Type**: "Kanban" (simplest for beginners)
   - **Project Key**: "PWT"
   - **Access**: Team-managed project

2. **Board Configuration**:
   Create these columns (in order):
   - **Backlog** - New tasks from team
   - **To Do** - Ready to start
   - **In Progress** - Currently working (limit to 2-3 items)
   - **Code Review** - Awaiting feedback
   - **Done** - Completed

## Story Templates

### 📋 Development Task Template
```
Summary: [Brief description of what needs to be done]

Description:
**Goal:** What needs to be accomplished

**Acceptance Criteria:**
- [ ] Criterion 1 (specific, measurable)
- [ ] Criterion 2 (specific, measurable)
- [ ] Code is tested
- [ ] Code is reviewed

**Technical Notes:** 
- Any implementation details
- Dependencies or blockers
- Relevant documentation links

**Definition of Done:**
- [ ] Code written and tested
- [ ] Code reviewed and approved
- [ ] Deployed to appropriate environment
- [ ] Documentation updated if needed

Labels: frontend, backend, feature, enhancement
Story Points: 1, 2, 3, 5, 8 (Fibonacci sequence)
Assignee: [Your name]
```

### 🐛 Bug Report Template
```
Summary: [Brief bug description]

Description:
**Steps to Reproduce:**
1. Navigate to...
2. Click on...
3. Enter...
4. Observe...

**Expected Result:** 
What should happen

**Actual Result:** 
What actually happens

**Environment:** 
- Browser: Chrome/Safari/Firefox
- OS: macOS/Windows/Linux
- Version: 
- Device: Desktop/Mobile

**Screenshots/Logs:** 
[Attach relevant images or error logs]

**Impact:** 
How this affects users/functionality

Priority: High/Medium/Low
Labels: bug, frontend/backend
```

### 📚 Learning/Research Task Template
```
Summary: Research [topic/technology]

Description:
**Learning Goal:** 
What specific knowledge/skill to acquire

**Success Criteria:**
- [ ] Understand key concepts
- [ ] Can explain to team member
- [ ] Can implement basic example
- [ ] Document learnings

**Resources:**
- Documentation links
- Tutorial suggestions
- Team members to consult

**Deliverable:**
- Brief summary document
- Code examples
- Recommendations for team

Labels: learning, research
Story Points: 2, 3, 5
```

## Sprint Planning Setup

### Sprint Configuration
- **Sprint Length**: 1 week (perfect for 20hrs/week schedule)
- **Sprint Capacity**: 8-12 story points max
- **Sprint Goal**: Focus on 3-5 small to medium tasks

### Weekly Sprint Routine

**Monday - Sprint Planning (30 mins)**:
- Review backlog
- Select 8-12 points of work
- Break down large tasks
- Set weekly goal

**Wednesday - Mid-Sprint Check (15 mins)**:
- Update task progress
- Flag any blockers
- Adjust scope if needed

**Friday - Sprint Review (15 mins)**:
- Move completed tasks to Done
- Note what went well/poorly
- Plan next sprint

## JIRA Best Practices for New Developers

### Task Management
1. **Only work on 1-2 tasks at a time**
2. **Update status daily** (even if no progress)
3. **Add comments** for significant updates or blockers
4. **Use time tracking** to understand your velocity
5. **Link related tasks** using JIRA relationships

### Communication in JIRA
- **@mention team members** for questions
- **Tag relevant people** on important updates  
- **Be specific** in comments and descriptions
- **Use labels** consistently for easy filtering

### Estimation Guidelines
- **1 point**: Simple config change, minor text update
- **2 points**: Small component update, simple bug fix
- **3 points**: New small component, medium complexity bug
- **5 points**: Feature component, complex integration
- **8 points**: Major feature, significant refactor

## Quick Setup Checklist
- [ ] Create Kanban project with 5 columns
- [ ] Save story templates
- [ ] Set up first sprint (current week)
- [ ] Create 2-3 practice tasks to test workflow
- [ ] Configure notifications (daily digest recommended)
- [ ] Set up filters for "My Issues" and "Recently Updated"

## Integration Tips
- **Link GitHub commits**: Include JIRA key (PWT-123) in commit messages
- **Connect with Notion**: Link JIRA tasks in daily dashboard
- **Slack notifications**: Set up for task assignments and mentions