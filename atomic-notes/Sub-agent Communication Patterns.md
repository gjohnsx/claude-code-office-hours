---
created: 2025-08-02T20:00:00.000Z
uid: 202508021005
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/architecture"
  - "#pattern/communication"
---

# Sub-agent Communication Patterns

## Core Insight
Sub-agents in Claude Code currently communicate through a parent-mediated pattern. Direct agent-to-agent communication isn't supported, but several patterns emerge for coordinating multi-agent workflows.

## Current Communication Model

### Sequential Parent-Mediated
```
User → Parent Agent
       ├→ Sub-agent A (returns result)
       ├→ Sub-agent B (gets A's result via parent)
       └→ Sub-agent C (gets A+B results via parent)
```

**Characteristics:**
- Parent controls all communication
- No direct agent-to-agent channels
- Results passed through parent's context
- Sequential execution only

## Emerging Patterns

### 1. Pipeline Pattern (Sid's Workflow)
```yaml
1. Feature Analyzer → extracts relevant code
2. Code Architect → uses analysis to plan
3. Implementation → executes the plan
4. Code Reviewer → validates results
5. Code Simplifier → optimizes output
```

### 2. File System as Message Bus
Users experiment with agents communicating via files:
```bash
# Agent A writes analysis
echo "Analysis results" > /tmp/agent_analysis.json

# Agent B reads when invoked
cat /tmp/agent_analysis.json
```

### 3. Context Accumulation
Parent accumulates sub-agent outputs:
```python
context = {}
context['analysis'] = feature_analyzer_result
context['plan'] = architect_result  
context['implementation'] = coder_result
# Each subsequent agent sees accumulated context
```

## Future Patterns (Discussed)

### Async Agent Communication
- Fire-and-forget agents
- Parallel execution with result merging
- Event-driven agent triggering

### Direct Communication Protocols
- Agent-to-agent messaging
- Shared memory/context spaces
- Pub/sub patterns for agent events

## Current Limitations

### No Parallel Execution
- Agents run sequentially
- Can't spawn multiple agents simultaneously
- No work distribution patterns

### No Persistent Agent State
- Each invocation is stateless
- No memory between calls
- Context must be explicitly passed

### No Direct Channels
- All communication through parent
- No peer-to-peer agent protocols
- No broadcast mechanisms

## Workarounds and Best Practices

### 1. Explicit Context Forwarding
```yaml
description: "Code reviewer. Needs: implementation results from previous agent, original requirements, and modified files"
```

### 2. Summary-Based Communication
Keep passed context concise:
```yaml
system_prompt: "Summarize your findings in 3-5 bullet points for the next agent"
```

### 3. Structured Output Formats
Standardize how agents return data:
```json
{
  "agent": "feature_analyzer",
  "status": "complete",
  "findings": [...],
  "next_agent_needs": [...]
}
```

## Key Quote from Transcript
> "How agents communicate with each other, when do they spin up? What triggers them? When do they die, if at all they die? Or are they always present? There's a lot of different ways of doing it"

## Related Notes
- [[Sub-agent Context Management]]
- [[Async vs Sync Agent Workflows]]
- [[Agent Orchestration Patterns]]
- [[File System as Agent Communication Layer]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Extensive discussion on agent communication patterns and future possibilities