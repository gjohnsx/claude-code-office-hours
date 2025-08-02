---
created: 2025-08-02T20:00:00.000Z
uid: 202508021007
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/architecture"
  - "#limitation"
---

# Sub-agent State and Persistence

## Core Insight
Sub-agents in Claude Code are completely stateless. Each invocation starts fresh with no memory of previous runs. This "blank slate" approach has both advantages and limitations.

## Current State Model

### Stateless Invocations
- Each sub-agent call is independent
- No built-in memory between invocations
- No persistent identity or state
- Start fresh every time

### What This Means
```python
# This doesn't work:
agent_1_run_1 = "Remember X"
agent_1_run_2 = "What was X?"  # Agent has no memory

# Must do this:
agent_1_run_2 = "Given that X=..., do Y"
```

## Advantages of Statelessness

### 1. Clean Reasoning
From transcript:
> "Because it starts from a blank slate and has a super specific system prompt tied to it, it can be more effective at that niche task"

### 2. No Context Pollution
- Previous errors don't affect new runs
- Each attempt is fresh
- No accumulated confusion

### 3. Predictable Behavior
- Same input → same behavior
- Easier to debug
- No hidden state effects

## Limitations and Workarounds

### No Learning Between Runs
Agents can't:
- Remember user preferences
- Learn from previous attempts  
- Build up knowledge over time

### Workaround Patterns

#### 1. Parent as Memory Holder
```yaml
Parent maintains context:
- User preferences
- Previous results
- Accumulated knowledge

Passes relevant history to each sub-agent
```

#### 2. File System Persistence
```bash
# Agent writes state
echo '{"last_run": "2024-01-15", "preferences": {...}}' > agent_state.json

# Next invocation reads state
cat agent_state.json
```

#### 3. Structured Context Passing
```yaml
description: "Reviewer agent. Always provide: previous review results if this is a re-review, user style preferences, and project conventions"
```

## Future Considerations (From Discussion)

### Persistent Agent Concepts
- "Always on" agents monitoring for changes
- Agents with memory/learning capabilities
- Long-running background agents

### Fire-and-Forget Patterns
User suggestion from transcript:
> "A subagent that forks your current main agent thread... something that just like you spin it off and it just goes and does its thing"

### Async Persistence Needs
- Agents running in background
- Accumulating insights over time
- Building user/project models

## Practical Implications

### Design Considerations
1. Don't rely on agent memory
2. Pass full context each time
3. Use parent agent for continuity
4. Consider file-based state for complex workflows

### Anti-patterns to Avoid
- Expecting agents to "remember" conversations
- Incremental learning without explicit state
- Assuming context carries between invocations

## Key Quote
> "Each agent invocation is stateless. You will not be able to send additional messages to the agent, nor will the agent be able to communicate with you outside of its final report."

## Related Notes
- [[Sub-agent Context Management]]
- [[Sub-agent Communication Patterns]]
- [[File System as Agent Communication Layer]]
- [[Agent Orchestration Patterns]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Discussion of stateless nature and future persistence possibilities