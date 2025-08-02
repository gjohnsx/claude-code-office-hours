---
created: 2025-08-02T21:30:00.000Z
uid: 202508022100
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/synthesis"
  - "#pattern/context-management"
  - "#resource/master-guide"
---

# Context Management Master Guide - Claude Code

## Overview
This guide synthesizes context management insights from multiple Claude Code sessions, covering both sub-agent context sharing and general Claude Code context optimization.

## Context Types in Claude Code

### 1. Session Context (Main Claude)
- **Size**: 200k tokens
- **Accumulates**: Tool calls, file reads, conversations
- **Management**: /clear, /compact commands
- **Persistence**: None between sessions

### 2. Sub-agent Context
- **Size**: Fresh window per agent
- **Controlled by**: Description field (what parent sends)
- **Returns via**: System prompt instructions
- **Persistence**: None - stateless invocations

### 3. Persistent Context (claude.md)
- **Size**: Minimal (loaded every session)
- **Scope**: Project, directory, or global
- **Purpose**: Instructions, commands, conventions
- **Persistence**: File-based, version controlled

## Context Flow Patterns

### Linear Accumulation (Single Claude)
```
Start (claude.md) → Search → Read files → Edit → Test → Accumulate
                                                           ↓
                                                    /compact → Continue
```

### Parent-Child Context Flow (Sub-agents)
```
Parent Context (100k)
    ↓ (filtered by description)
Sub-agent 1 (20k) → Returns summary
    ↓
Parent Context (105k)
    ↓ (filtered by description)
Sub-agent 2 (25k) → Returns summary
```

### Multi-Agent Shared Context
```
Agent 1 → writes → shared.md
                      ↓
Agent 2 → reads → shared.md → writes → status.md
                                           ↓
Agent 3 → reads → shared.md + status.md
```

## Context Optimization Strategies

### 1. Token Budget Management

**From Cal (Claude Code Best Practices):**
- Monitor bottom-right indicator
- Use /compact vs /clear strategically
- Plan operations to minimize waste

**From Sid (Sub-agents):**
- Keep under 100k tokens per agent
- Use minimal context for simple tasks
- Progressive context building

### 2. Search-First Approach

**Agentic Search Benefits:**
- Low context cost
- Targeted file reading
- No wasted tokens on irrelevant files
- Progressive understanding

**Search Before Read Pattern:**
```bash
# Good: Targeted search first
grep -r "authenticate" --include="*.js"
# Then read only relevant files

# Bad: Reading everything
cat src/**/*.js  # Wastes context
```

### 3. Model-Based Optimization

**Task-Model-Context Matching:**
| Task Type | Model | Context Needs |
|-----------|-------|---------------|
| Planning | Opus | Can handle large context |
| Implementation | Sonnet | Moderate context |
| Simple tasks | Haiku | Minimal context |

## Advanced Context Patterns

### 1. Context Staging Pipeline
```yaml
Stage 1 - Discovery:
  - Minimal context
  - Search operations
  - Identify targets

Stage 2 - Analysis:
  - Read key files
  - Build understanding
  - Moderate context

Stage 3 - Implementation:
  - Focused context
  - Specific files only
  - Preserve tokens

Stage 4 - Validation:
  - Test results
  - Minimal new context
  - Reuse knowledge
```

### 2. Context Preservation Strategies

**File-Based Memory:**
```markdown
# Before /compact
"Write our current state to progress.md"

# After /compact
"Read progress.md to restore context"
```

**Structured Handoffs:**
```markdown
## Context Summary
- Working on: Auth system
- Key files: /auth/*, /middleware/*
- Decisions: JWT, 24hr timeout
- Next: Frontend integration
```

### 3. Context Sharing Patterns

**Sub-agent Context Control:**
```yaml
# Description field - controls input
description: "Needs: file paths, recent changes, NOT file contents"

# System prompt - controls output  
system_prompt: "Return only: decisions made, files to modify (max 500 words)"
```

## Context Anti-Patterns

### 1. Context Explosion
❌ Reading entire directories
❌ Accumulating failed attempts
❌ Redundant file reads
❌ Keeping irrelevant history

### 2. Context Starvation
❌ Not providing enough context to sub-agents
❌ Over-aggressive clearing
❌ Missing key dependencies
❌ Incomplete handoffs

### 3. Context Waste
❌ Retrying without clearing errors
❌ Reading generated files
❌ Duplicating information
❌ Verbose sub-agent returns

## Practical Context Recipes

### Recipe 1: Long Feature Development
```bash
1. Start with planning (low context)
2. /compact after planning complete
3. Implement in stages
4. /compact between major milestones
5. Use files for state between sessions
```

### Recipe 2: Multi-Agent Architecture
```yaml
Coordinator (Parent):
  - Manages overall context
  - Dispatches to specialists
  - Aggregates results

Specialists (Sub-agents):
  - Minimal focused context
  - Specific expertise
  - Concise returns
```

### Recipe 3: Debugging Session
```bash
1. Describe bug symptoms
2. Let Claude search (low context)
3. Read only suspect files
4. Test hypotheses
5. /clear after fix confirmed
```

## Context Monitoring Tools

### Built-in Indicators
- Bottom-right token counter
- Context warnings
- Performance degradation
- Tool failures

### Mental Model
```
Empty context = Fast, exploratory
Half full = Normal development
Nearly full = Time to compact
Full = Degraded performance
```

## Future of Context Management

### Discussed Improvements
- Async agent communication
- Shared context spaces
- Persistent agent memory
- Context versioning
- Selective context transfer

### Current Workarounds
- File-based communication
- Structured handoffs
- Clear documentation
- Team conventions
- Tool strategies

## Quick Reference

### Commands
- `/clear` - Full reset
- `/compact` - Summarize and continue
- `/model` - Check current model
- `Shift+Tab` - Auto-accept mode
- `Escape x2` - Jump back in conversation

### Context Costs
- **Low**: Search, list, grep
- **Medium**: Read file, edit file
- **High**: Large file reads, failed operations
- **Expensive**: Retrying without clearing

### Best Practices Checklist
- [ ] Use claude.md for persistent context
- [ ] Search before reading
- [ ] Compact instead of clear
- [ ] Plan before implementing
- [ ] Monitor token usage
- [ ] Structure sub-agent communication
- [ ] Use appropriate models
- [ ] Clear between unrelated tasks

## Related Master Guides
- [[Sub-agent Context Management]]
- [[Claude.md State Management]]
- [[Multi-Agent Orchestration]]
- [[Search-First Development]]

## Sources
- [[Claude Code Office Hours - Sub-agents and Context]]
- [[Claude Code Best Practices - Cal Rueb]]