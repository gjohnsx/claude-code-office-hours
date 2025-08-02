# Claude Code Office Hours - Sub-agents and Context Management

This repository contains comprehensive notes from the Claude Code Office Hours session focusing on sub-agents and context management in Claude Code.

## Contents

### Main Index
- [Claude Code Office Hours - Sub-agents and Context](./Claude%20Code%20Office%20Hours%20-%20Sub-agents%20and%20Context.md) - Overview and index of all topics

### Deep Dive
- [Context Management Deep Dive](./Context%20Management%20Deep%20Dive.md) - Comprehensive guide to sub-agent context management

### Atomic Notes
Located in the `atomic-notes/` directory:

- **Sub-agent Context Management** - Core concepts of how context flows between agents
- **Sub-agent Description Field Controls Context** - Critical insight on the description field's role
- **Parent Agent Context Passing Strategy** - How parent agents decide what context to share
- **Context Window Optimization** - Managing token limits in multi-agent systems
- **Sub-agent Communication Patterns** - Current and future agent-to-agent communication
- **Model Selection for Different Agent Tasks** - Opus vs Sonnet vs Haiku selection strategy
- **Sub-agent State and Persistence** - Understanding stateless agents and workarounds
- **Async vs Sync Agent Workflows** - Current limitations and future possibilities
- **Sub-agent Workflow Best Practices** - Production patterns from the Claude Code team
- **Agent Interruption and Control** - Current limitations and workarounds

## Key Insights

1. **The Description Field is Functional**: It's not just documentation - it controls what context the parent agent passes to sub-agents
2. **Context Doesn't Auto-Transfer**: Parent agents don't automatically pass all context; you must be explicit in descriptions
3. **Model Selection Matters**: Use Haiku for simple tasks, Sonnet for implementation, Opus for complex planning
4. **100k Token Target**: Keep context under 100k tokens for optimal performance
5. **Blank Slate Advantage**: Sub-agents starting fresh can be more focused and effective

## Source
These notes are based on the Claude Code Office Hours livestream transcript, featuring Tariq and Sid from the Claude Code team discussing sub-agents, context management, and building email agents with the Claude Code SDK.