---
created: 2025-08-02T21:00:00.000Z
uid: 202508022004
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#pattern/workflow"
  - "#pattern/orchestration"
---

# Multi-Claude Orchestration

## Core Insight
Advanced users run multiple Claude Code instances simultaneously, orchestrating them to work on different aspects of a project. This multiplies productivity but requires coordination strategies.

## The Multi-Claude Pattern

### Cal's Experience
> "I know people at Anthropic and a few customers that run four Claudes at the same time... I can only do two, but I know people that do four."

### Implementation Methods
- Terminal multiplexers (tmux)
- Multiple terminal tabs
- VS Code integrated terminals
- Separate IDE instances

## Coordination Strategies

### 1. File-Based Communication
Most common pattern for agent coordination:

**Agent Communication Example:**
```bash
# Agent 1 writes instructions
"Hey, write some stuff in ticket.md for another developer"

# Agent 2 reads instructions  
"Hey, read ticket.md. Another developer left this note for you."
```

### 2. Shared State Files
Central files for coordination:
- `progress.md` - Current status
- `tasks.md` - Work distribution
- `decisions.md` - Architectural choices
- `blockers.md` - Issues for other agents

### 3. Work Division Patterns

#### Horizontal Split
Different features/modules:
- Agent 1: Frontend components
- Agent 2: API endpoints
- Agent 3: Database migrations
- Agent 4: Tests

#### Vertical Split
Different layers:
- Agent 1: UI implementation
- Agent 2: Business logic
- Agent 3: Data layer
- Agent 4: Infrastructure

#### Pipeline Pattern
Sequential processing:
- Agent 1: Research and planning
- Agent 2: Implementation
- Agent 3: Testing
- Agent 4: Documentation

## Context Sharing Techniques

### Question from Audience
> "Can you make it so that agents two and three use the context from agent one, maybe agent four uses the context from agent two?"

### Cal's Solution
> "Ask all your agents to probably write to a shared markdown file... so they can all check in and communicate"

### Implementation Example
```markdown
# shared-context.md

## Agent 1 Findings
- Identified performance bottleneck in API
- Files: /api/users.js, /db/queries.js

## Agent 2 Implementation  
- Optimized query structure
- Added caching layer
- Files modified: /api/cache.js

## Agent 3 Testing
- Performance improved by 70%
- All tests passing
- New tests added: /tests/performance.test.js
```

## Orchestration Best Practices

### 1. Clear Work Boundaries
- Define each agent's scope explicitly
- Avoid overlapping responsibilities
- Use different directories when possible
- Coordinate file access

### 2. Communication Protocols
Establish patterns:
```markdown
## Status Updates
- STARTED: Beginning work on [task]
- BLOCKED: Need [resource] from [agent]
- COMPLETED: Finished [task], results in [file]
```

### 3. Synchronization Points
Regular check-ins:
- After major milestones
- Before starting new phases
- When blocked or confused
- At natural boundaries

## Advanced Patterns

### Dynamic Work Assignment
Agents can assign work to each other:
```markdown
# Agent 1 writes in tasks.md
"Agent 2: Please implement the user service based on the interface in /api/interfaces/user.ts"
```

### Conflict Resolution
Handling overlapping work:
- Use git branches per agent
- Coordinate through lock files
- Implement merge strategies
- Regular synchronization

### Load Balancing
Distribute work based on:
- Complexity of tasks
- Agent availability
- Dependencies
- Estimated time

## Common Challenges

### 1. Context Isolation
- Agents don't share memory
- Must explicitly communicate
- Can miss important updates
- Requires discipline

### 2. Coordination Overhead
- Time spent on communication
- Potential for conflicts
- Synchronization delays
- Complexity management

### 3. Debugging Multi-Agent Work
- Tracking which agent did what
- Understanding interaction bugs
- Reproducing issues
- Maintaining coherent logs

## Tools and Techniques

### Terminal Management
- **tmux**: Session management, pane synchronization
- **GNU Screen**: Persistent sessions
- **Terminal tabs**: Simple separation
- **VS Code**: Integrated terminal management

### File Watching
Agents can monitor shared files:
```bash
# Watch for updates from other agents
watch -n 1 cat shared-status.md
```

### Git Integration
- Separate branches per agent
- Regular commits
- Clear commit messages with agent ID
- Automated merging strategies

## Success Metrics
- Reduced wall-clock time
- Increased throughput
- Better task parallelization
- Maintained code quality

## Related Notes
- [[File-Based Agent Communication]]
- [[Context Sharing Strategies]]
- [[Parallel Development Workflows]]
- [[Agent Coordination Patterns]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Discussion of multiple Claude instances and coordination