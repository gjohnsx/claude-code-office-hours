---
created: 2025-08-02T20:00:00.000Z
uid: 202508021001
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/context-management"
---

# Sub-agent Context Management

## Core Insight
Sub-agents in Claude Code receive context through a two-field system: the **description field** (controls what parent passes) and the **system prompt** (guides sub-agent behavior). The parent agent decides context based on the description, not the system prompt.

## How Context Flows

### Parent → Sub-agent
1. Parent agent reads the sub-agent's **description field**
2. Based on description + conversation history, parent decides what context to pass
3. Sub-agent receives this filtered context + its system prompt
4. Sub-agent starts with a "blank slate" - no automatic context inheritance

### Sub-agent → Parent
1. Sub-agent determines what to return based on its **system prompt**
2. The system prompt guides what information is relevant to send back
3. Parent receives only what sub-agent chooses to return

## Controlling Context Flow

### Via Description Field
```yaml
description: "Analyzes code architecture. Always needs: current file paths, project structure, and recent changes"
```
This ensures the parent will pass file paths and project context.

### Via System Prompt
```yaml
system_prompt: "You are a code reviewer. Return only critical issues and suggested fixes. Do not include full file contents in your response."
```
This controls what gets sent back to parent.

## Key Quote from Transcript
> "If you want to be like, okay, like I always want the sub-agents to get the file paths of all the files that the parent agent has, you can specify that in the description, and this parent agent will then follow that whenever it calls into it."

## Practical Implications
- Sub-agents DON'T automatically see all parent context
- Description field is NOT just documentation - it's functional
- You can create focused sub-agents by limiting context
- Context control happens through prompting, not configuration

## Related Notes
- [[Sub-agent Description Field Controls Context]]
- [[Parent Agent Context Passing Strategy]]
- [[Sub-agent System Prompt Best Practices]]
- [[Context Window Optimization for Multi-Agent Systems]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Timestamp: Discussion throughout, particularly focused section on context management