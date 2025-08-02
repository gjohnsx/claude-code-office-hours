---
created: 2025-08-02T21:00:00.000Z
uid: 202508022007
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#pattern/communication"
  - "#pattern/orchestration"
---

# File-Based Agent Communication

## Core Insight
Since Claude Code has no built-in memory or agent-to-agent communication, file-based communication emerges as the primary pattern for coordinating multiple agents and preserving state between sessions.

## Basic Communication Pattern

### Cal's Example
> "Sometimes I'll be working with Claude and I'll just say, 'Hey, I need you to write some stuff in ticket.md for another developer,' and then I'll fire up another Claude Code and I'll be like, 'Hey, read ticket.md. Another developer left this note for you.'"

### File as Message
Files serve as:
- Asynchronous messages
- Shared state storage
- Task assignments
- Progress tracking

## Communication File Types

### 1. Task Assignment Files
```markdown
# tasks.md
## For Frontend Agent
- Implement user dashboard component
- Use existing API endpoints in /api/user
- Follow design in /designs/dashboard.png

## For Backend Agent  
- Create user statistics endpoint
- Cache results for 5 minutes
- Return format: { daily: [], weekly: [], monthly: [] }
```

### 2. Status Update Files
```markdown
# status.md
## Backend Agent - 2:45 PM
- ✅ Created statistics endpoint
- ✅ Added caching layer
- ⚠️ Need frontend to handle empty data case
- 📍 Files: /api/stats.js, /cache/redis.js

## Frontend Agent - 3:10 PM
- ✅ Dashboard component structure
- 🔄 Integrating with stats API
- ❌ Blocked: Need error format from backend
```

### 3. Shared Context Files
```markdown
# context.md
## Architecture Decisions
- Using Redis for caching (decided by Agent 1)
- JWT tokens in httpOnly cookies (Agent 2)
- Component library: shadcn/ui (Agent 3)

## Key Files
- Auth: /services/auth.js
- API Base: /api/base.js
- Types: /types/index.ts
```

## Advanced Patterns

### 1. Lock Files for Coordination
Prevent conflicts:
```markdown
# editing.lock
Currently editing: /src/components/Dashboard.jsx
Agent: Frontend-Agent-1
Started: 2024-01-20 14:30:00
```

### 2. Message Queues
```markdown
# message-queue.md
## Messages
1. [Backend -> Frontend] API endpoint ready at /api/stats
2. [Frontend -> Backend] Need pagination support
3. [Backend -> Frontend] Pagination added, use ?page=1&limit=10
```

### 3. Structured Communication
```json
// agent-communication.json
{
  "messages": [
    {
      "from": "agent-1",
      "to": "agent-2",
      "timestamp": "2024-01-20T10:30:00Z",
      "type": "task-complete",
      "data": {
        "task": "api-setup",
        "files": ["/api/users.js"],
        "next": "please-add-tests"
      }
    }
  ]
}
```

## State Preservation Patterns

### Session Handoff
Before ending session:
```markdown
# session-state.md
## Current State
- Working on: User authentication flow
- Completed: Database schema, API endpoints
- Next steps: Frontend forms, validation
- Blockers: Need design approval

## Key Decisions
- Using bcrypt for passwords
- Session timeout: 24 hours
- Email verification required
```

### Progress Tracking
```markdown
# progress.md
## Project: User Management System

### Completed
- [x] Database schema
- [x] User model
- [x] Authentication endpoints
- [x] Basic tests

### In Progress
- [ ] Admin panel (50% - Agent 2 working)
- [ ] Email service (30% - Agent 3 blocked)

### Pending
- [ ] Documentation
- [ ] Deployment scripts
```

## Best Practices

### 1. Clear File Naming
Use descriptive names:
- `agent-tasks.md` - Task assignments
- `shared-decisions.md` - Architecture choices
- `blockers.md` - Current issues
- `handoff.md` - Session transitions

### 2. Consistent Formats
Standardize structure:
```markdown
## [Agent Name] - [Timestamp]
### Status: [Working|Blocked|Complete]
### Current Task: [Description]
### Files Modified: [List]
### Notes: [Any important information]
```

### 3. Regular Updates
- Update before switching tasks
- Document decisions immediately
- Clear completed items
- Flag urgent issues

## Integration with Git

### Branch Coordination
```markdown
# branches.md
## Active Branches
- feature/auth - Agent 1 (auth system)
- feature/ui - Agent 2 (frontend)
- fix/performance - Agent 3 (optimization)

## Merge Order
1. feature/auth (base functionality)
2. fix/performance (applies to auth)
3. feature/ui (depends on both)
```

### Commit Coordination
```markdown
# commit-plan.md
## Next Commits
- Agent 1: "Add JWT authentication"
- Agent 2: "Implement login form"
- Agent 3: "Optimize database queries"
```

## Limitations and Workarounds

### No Real-Time Updates
- Agents must poll files
- Use timestamps for ordering
- Clear old messages
- Implement "read receipts"

### No Built-In Locking
- Create manual lock files
- Use git branches for isolation
- Coordinate through conventions
- Clear communication protocols

### Context Limits
- Keep files concise
- Archive old communications
- Summary files for history
- Link to detailed logs

## Future Possibilities

From audience question about agent context sharing:
> "Probably what's going to happen is if you wanted to do that, you would ask all your agents to write to a shared markdown file"

Potential evolution:
- Native agent communication
- Shared memory spaces
- Event-driven updates
- Built-in coordination

## Related Notes
- [[Multi-Claude Orchestration]]
- [[Claude.md State Management]]
- [[Agent Coordination Patterns]]
- [[Stateless Agent Workarounds]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Discussion of multi-agent coordination and file-based communication