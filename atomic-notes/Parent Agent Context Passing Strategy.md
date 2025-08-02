---
created: 2025-08-02T20:00:00.000Z
uid: 202508021003
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/context-management"
---

# Parent Agent Context Passing Strategy

## Core Insight
The parent agent acts as a smart context filter, deciding what information to pass to sub-agents based on the sub-agent's description and the current conversation state. This decision-making is automatic but can be influenced through careful description writing.

## Context Selection Process

### What Parent Agent Considers:
1. **Sub-agent description** - Primary signal for context needs
2. **Current conversation history** - What's been discussed
3. **Available context** - Files, previous results, user requests
4. **Task relevance** - What seems related to the sub-agent's purpose

### Default Behavior:
- Parent does NOT pass everything automatically
- Tends to pass what seems "relevant" based on description
- May omit context if description doesn't indicate need
- Prefers passing less context for efficiency

## Strategies for Ensuring Context

### 1. Explicit Requirements
```yaml
description: "Feature analyzer that examines code structure. ALWAYS NEEDS: all file paths currently in context, file contents for imported modules, package.json"
```

### 2. Context Triggers
```yaml
description: "Architecture reviewer. When reviewing React components, needs: component files, test files, and style files. When reviewing APIs, needs: route definitions and middleware."
```

### 3. Negative Requirements
```yaml
description: "Performance profiler. Needs execution logs but NOT source code contents (only file paths)."
```

## Advanced Pattern: Context Negotiation
Some users request features like:
- `include_context: true/false` flags
- Explicit context manifests
- Parent-child context contracts

Currently, this is handled through description prompting rather than configuration.

## Practical Example from Transcript
When Sid uses his multi-agent workflow:
1. Feature analyzer gets specific feature files (based on description)
2. Code architect gets analyzer results + more context
3. Implementation agent gets architect plan + full file access

Each stage's description ensures proper context flow.

## Related Notes
- [[Sub-agent Context Management]]
- [[Sub-agent Description Field Controls Context]]
- [[Context Window Optimization for Multi-Agent Systems]]
- [[Sub-agent Communication Patterns]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Discussion of how parent agents decide what to pass down