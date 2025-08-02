---
created: 2025-08-02T20:00:00.000Z
uid: 202508021002
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/context-management"
---

# Sub-agent Description Field Controls Context

## Core Insight
The description field in custom sub-agents is the primary mechanism for controlling what context the parent agent passes down. It's not just documentation - it actively influences parent agent behavior.

## How It Works
1. Parent agent reads all available sub-agent descriptions
2. Based on current task + descriptions, parent decides which sub-agent to invoke
3. Description content influences what context parent includes in the call
4. More specific descriptions = more predictable context passing

## Example Descriptions for Context Control

### Explicit File Path Requirements
```yaml
description: "Code architecture analyzer. Requires: all currently open file paths, project root structure, and package.json contents"
```

### Minimal Context
```yaml
description: "Test runner that only needs the test command. No file contents required."
```

### Conditional Context
```yaml
description: "Security reviewer for authentication code. When called, needs: all auth-related files, environment variable names (not values), and recent git changes to auth modules"
```

## Best Practices
1. **Be explicit** about context needs in description
2. **List required inputs** clearly
3. **Specify format** if needed (e.g., "file paths as absolute paths")
4. **Indicate optional vs required** context

## Common Pitfall
Putting context requirements only in system prompt won't guarantee the parent passes that context. The description field is what the parent agent actually reads when deciding what to send.

## Related Notes
- [[Sub-agent Context Management]]
- [[Parent Agent Context Passing Strategy]]
- [[Sub-agent Invocation Patterns]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Key insight from Sid's explanation of the two-field system