---
created: 2025-08-02T20:00:00.000Z
uid: 202508021100
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/synthesis"
  - "#pattern/context-management"
---

# Context Management Deep Dive - Claude Code Sub-agents

## The Two-Field System

### Description Field (Parent-Facing)
- **Purpose**: Tells parent agent when/how to invoke sub-agent
- **Controls**: What context parent passes to sub-agent
- **Key Insight**: This is NOT just documentation - it's functional

### System Prompt (Sub-agent Behavior)
- **Purpose**: Guides sub-agent's internal behavior
- **Controls**: What sub-agent returns to parent
- **Scope**: Only seen by sub-agent, not parent

## How Context Actually Flows

### 1. Parent → Sub-agent Context Passing

**The Decision Process:**
```
Parent reads: Sub-agent descriptions
Parent considers: Current conversation + Available context
Parent decides: What context to include
Parent sends: Filtered context to sub-agent
```

**Key Point**: Parent does NOT automatically pass everything!

### 2. Controlling What Gets Passed

**Through Description Field:**
```yaml
# Explicit Requirements
description: "Code analyzer. ALWAYS needs: all open file paths, project structure, package.json"

# Conditional Context
description: "Security reviewer. When reviewing auth code, needs: auth files, env var names, recent git changes"

# Minimal Context
description: "Test runner. Only needs: test command. No file contents required."
```

### 3. Sub-agent → Parent Returns

**Controlled by System Prompt:**
```yaml
system_prompt: |
  Return only:
  - Critical findings (max 5)
  - Specific files to modify
  - Recommended next steps
  Do NOT include: Full analysis, code contents, verbose explanations
```

## Context Window Optimization

### The 100k Token Target
- Keep parent context under 100k tokens
- Each sub-agent starts fresh (blank slate)
- Sub-agents can work with focused subsets

### Progressive Context Pattern
```
Parent (100k) 
  → Analyzer (20k - only relevant files)
    → Architect (40k - analysis + more context)  
      → Implementer (30k - plan + specific files)
```

### Model-Based Optimization
- **Haiku**: Minimal context tasks (test running)
- **Sonnet**: Moderate context (implementation)
- **Opus**: Can handle large context effectively

## Practical Context Patterns

### 1. The Pipeline Pattern
Each agent adds to context:
```python
context = {}
context['analysis'] = analyzer_result
context['plan'] = architect_result
context['implementation'] = implementation_result
# Each sees accumulated context
```

### 2. Selective Context Forward
```yaml
description: "Implementation agent. Needs: architecture plan, files to modify, NOT the full analysis history"
```

### 3. Summary-Based Handoffs
```yaml
system_prompt: "Summarize in 3-5 bullets what next agent needs to know"
```

## Common Context Mistakes

### ❌ Don't Do This:
- Put context needs only in system prompt
- Assume parent passes everything
- Send full file contents when paths suffice
- Let context grow unbounded

### ✅ Do This:
- Explicit context needs in description
- Request minimum viable context
- Use summaries for handoffs
- Monitor token usage

## Advanced Context Control

### File System as Shared Context
```bash
# Agent A writes
echo "Analysis results" > /tmp/shared_context.json

# Agent B reads
cat /tmp/shared_context.json
```

### Structured Context Requests
```yaml
description: |
  Feature implementer. Required context:
  - architecture_plan: object
  - files_to_modify: string[]
  - test_requirements: string[]
  - user_requirements: string
```

## Key Insights from Production Use

### 1. "Blank Slate" is a Feature
> "Because it starts from a blank slate... it can be more effective at that niche task"

Fresh context = Focused reasoning

### 2. Description Field is Critical
> "If you want the sub-agents to get file paths... specify that in the description, and the parent agent will follow that"

### 3. Context is Expensive
- Token costs add up
- Latency increases with context
- But: Better context = better results

## Future Context Features (Discussed)

### User Requests:
- `include_context: true/false` flags
- Explicit context manifests  
- Direct agent-to-agent context sharing
- Persistent context between invocations

### Team Considerations:
- Async context sharing
- Context versioning
- Conflict resolution
- Memory management

## Practical Checklist

When designing sub-agents:
- [ ] Write explicit context needs in description
- [ ] Design minimal system prompts for returns
- [ ] Plan context flow through agent pipeline
- [ ] Consider token budget for each stage
- [ ] Use appropriate model for context size
- [ ] Design summaries for inter-agent handoffs
- [ ] Monitor total context growth
- [ ] Test with minimal context first

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Complete synthesis of context management discussion