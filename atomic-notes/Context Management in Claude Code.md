---
created: 2025-08-02T21:00:00.000Z
uid: 202508022003
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#pattern/context-management"
  - "#pattern/best-practices"
---

# Context Management in Claude Code

## Core Insight
Claude Code uses a 200k token context window that accumulates during sessions. Effective context management is crucial for long productive sessions, with two primary strategies: clearing and compacting.

## Context Accumulation

### How Context Builds
From Cal:
> "Claude is an agent and when it calls these tools, the context builds up and up over time"

Each action adds to context:
- Tool calls and results
- File contents read
- Search results
- Conversation history

### Visual Indicators
- Bottom-right warning when approaching limit
- Progressive alerts as context fills
- Clear indication of remaining space

## Management Strategies

### 1. /clear Command
- **Effect**: Complete context reset
- **Preserves**: Only claude.md file
- **Use when**: Starting completely new task
- **Loses**: All previous work context

### 2. /compact Command
**How it works:**
> "A user message is inserted and it just says something like, 'Hey, I need to go summarize everything we've been up to. I'm gonna give this to another developer and they're gonna pick up where I left off.'"

**Benefits:**
- Maintains continuity
- Preserves key insights
- Enables long sessions
- Seeds next session with summary

**Team focus:**
> "We spend a lot of time tuning this compact functionality so that as you max out the context window and then run compact, you can start back over and keep going."

## Context Optimization Techniques

### 1. Strategic File Reading
- Read only necessary files
- Use search to find relevant sections
- Avoid reading entire large files
- Let Claude decide what's needed

### 2. Efficient Tool Usage
- Batch related operations
- Avoid redundant searches  
- Use targeted file paths
- Leverage Claude's memory within session

### 3. Planning Before Execution
Reduce context waste by planning:
> "Hey, I have this bug. Can you search around, figure out what's causing it, and just tell me a plan how we're gonna fix it?"

Planning uses less context than trial-and-error.

## Multi-Session Patterns

### Continuous Work
Using /compact for multi-session work:
1. Work until context warning
2. Run /compact
3. Continue with summarized context
4. Repeat as needed

### Task Switching
Using /clear for new tasks:
1. Complete current task
2. Run /clear
3. Start fresh with new task
4. claude.md provides baseline context

## Advanced Context Management

### State Preservation
For complex multi-session work:
```markdown
# Write state to file before compact
"Hey Claude, write our current progress to progress.md before we compact"

# After compact
"Read progress.md to understand where we left off"
```

### Selective Context
Guide Claude on what to preserve:
```markdown
"Focus the summary on:
- Implementation decisions made
- Remaining tasks
- Key file locations
- Important findings"
```

## Context-Aware Workflows

### 1. Batching Related Work
Group similar tasks to maximize context reuse:
- All refactoring together
- All tests together
- All documentation together

### 2. Progressive Exploration
Start broad, narrow focus:
1. Initial exploration (low context)
2. Identify key areas
3. Deep dive on specifics
4. Compact if needed

### 3. Context Budgeting
Mental model for context usage:
- Search operations: Low cost
- File reading: Medium cost
- Large file edits: High cost
- Tool errors/retries: Wasteful

## Common Pitfalls

### 1. Context Explosion
- Opening too many files early
- Unguided exploration
- Redundant operations
- Not using search effectively

### 2. Premature Clearing
- Losing valuable context
- Having to re-explore
- Missing previous decisions
- Breaking workflow momentum

### 3. Ignoring Warnings
- Working past context limits
- Degraded performance
- Potential failures
- Lost work

## Best Practices Checklist

- [ ] Monitor context indicator regularly
- [ ] Use /compact over /clear when possible
- [ ] Plan before executing
- [ ] Batch related operations
- [ ] Write progress to files for long tasks
- [ ] Use search before reading files
- [ ] Clear context between unrelated tasks

## Related Notes
- [[Claude.md State Management]]
- [[Context Window Optimization]]
- [[Long Session Workflows]]
- [[Search-First Development]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Detailed context management section