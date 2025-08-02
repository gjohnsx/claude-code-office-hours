---
created: 2025-08-02T20:00:00.000Z
uid: 202508021004
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/performance"
  - "#pattern/context-management"
---

# Context Window Optimization for Multi-Agent Systems

## Core Insight
Each sub-agent invocation has its own context window, starting fresh. This provides both opportunities for optimization and challenges for context continuity. The goal is to balance comprehensive context with token efficiency.

## Token Management Strategies

### 1. Progressive Context Reduction
```
Parent (100k tokens) 
  → Feature Analyzer (20k tokens - only relevant files)
    → Code Architect (40k tokens - analysis + more files)
      → Implementation (30k tokens - plan + specific files)
```

### 2. Model-Based Optimization
- **Haiku** for simple tasks (test running, linting) - minimal context needed
- **Sonnet** for implementation - moderate context
- **Opus** for planning/architecture - can handle more context effectively

### 3. Context Compression via Summaries
Sub-agents return summaries, not full analysis:
```yaml
system_prompt: "Return a concise summary of findings (max 500 words) focusing on actionable insights. Do not include full code blocks unless critical."
```

## Key Insights from Transcript

### The 100k Token Target
- Aim to keep context under 100k tokens for optimal performance
- Parent agent should monitor total context size
- Sub-agents can work with focused subsets

### "Blank Slate" Advantage
> "Because it starts from a blank slate and has a super specific system prompt tied to it, it can be more effective at that niche task"

Starting fresh allows:
- Focused attention on specific task
- No context pollution from unrelated discussions
- Cleaner reasoning chains

## Practical Patterns

### 1. Context Staging
```yaml
# Feature Analyzer
description: "Needs only: target feature files and immediate dependencies"

# Code Architect  
description: "Needs: feature analysis results + broader codebase context"

# Implementation
description: "Needs: architecture plan + specific files to modify"
```

### 2. Selective Context Return
Configure sub-agents to return only essential information:
- Decisions made
- Files to modify
- Key insights
- NOT: Full analysis process, redundant information

### 3. Context Caching Pattern
While not explicitly supported, users discuss patterns like:
- File-based context storage between agents
- Summary accumulation strategies
- Context inheritance chains

## Performance Implications
- Smaller context = faster responses
- Focused context = better reasoning
- But: May miss important connections
- Trade-off: Completeness vs efficiency

## Related Notes
- [[Sub-agent Context Management]]
- [[Model Selection for Different Agent Tasks]]
- [[Sub-agent Performance Optimization]]
- [[Context Passing Anti-patterns]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Discussion of token limits and optimization strategies