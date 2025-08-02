---
created: 2025-08-02T20:00:00.000Z
uid: 202508021009
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/workflow"
  - "#pattern/best-practices"
---

# Sub-agent Workflow Best Practices

## Core Insight
Effective sub-agent workflows require careful orchestration, clear role definition, and strategic context management. Sid's production workflow demonstrates a mature pattern for complex tasks.

## Sid's Five-Agent Workflow

### 1. Feature Analyzer Agent
```yaml
role: "Read code specific to feature"
model: Sonnet (could be Haiku)
input: Target feature files
output: Code structure and abstraction analysis
```

### 2. Code Architect Agent
```yaml
role: "Design implementation approach"  
model: Opus (critical for quality)
input: Analysis + requirements + developer hints
output: Multiple implementation options
```

### 3. Implementation Agent
```yaml
role: "Execute the chosen plan"
model: Sonnet
input: Selected architecture plan + files
output: Implemented code
mode: "YOLO mode" (auto-accept edits)
```

### 4. Code Reviewer Agent
```yaml
role: "Review implementation quality"
model: Sonnet
input: New code + standards
output: Issues and suggestions
```

### 5. Code Simplifier Agent
```yaml
role: "Optimize without changing functionality"
model: Sonnet  
input: Reviewed code
output: Simplified, cleaner code
```

## Key Principles

### 1. Progressive Refinement
Start broad → narrow focus → implement → review → optimize

### 2. Clear Role Boundaries
Each agent has ONE primary responsibility:
- Analyzer: Understand existing code
- Architect: Plan new approach
- Implementer: Write code
- Reviewer: Find issues
- Simplifier: Improve quality

### 3. Context Staging
From transcript:
> "The first thing I do is call the feature analyzer agent... it reports that back to the parent thread... then the code architect will take the information"

Each stage builds on previous results.

### 4. Model-Task Matching
- Complex reasoning → Opus
- Mechanical tasks → Haiku  
- Standard coding → Sonnet

## Workflow Patterns

### Sequential Pipeline
Best for: Complex features requiring multiple stages
```
Analyze → Plan → Build → Review → Optimize
```

### Focused Specialist
Best for: Specific tasks like testing
```yaml
test-runner:
  model: haiku
  role: "Run tests and summarize"
  context: minimal (just commands)
```

### Decision Tree
Best for: Conditional workflows
```
Analyzer → {
  if needs_architecture: → Architect
  else: → Direct Implementation
}
```

## Context Management Strategies

### 1. Explicit Context Requirements
```yaml
description: "Architecture agent. ALWAYS needs: feature analysis results, project conventions, available design patterns"
```

### 2. Summary-Based Handoffs
Keep inter-agent communication concise:
```yaml
system_prompt: "Summarize findings in 3-5 bullet points focusing on what the next agent needs to know"
```

### 3. Progressive Context Building
- Start with minimal context
- Each agent adds its insights
- Final agents see accumulated wisdom

## Common Pitfalls to Avoid

### 1. Over-Broad Agents
❌ "General helper agent"
✅ "SQL query optimizer agent"

### 2. Circular Dependencies
❌ Agent A needs B's output, B needs A's output
✅ Clear directional flow

### 3. Context Overload
❌ Passing entire codebase to each agent
✅ Focused, relevant context only

## Practical Tips

### Custom Slash Commands
From transcript:
> "I also have some slash commands that set up the context when I'm creating a new feature... I just say 'slash new feature' and Claude knows what's going to happen next"

### Proactive Planning
Use agents for ideation:
> "Planning and just asking questions to the model with Claude Code is underrated"

### Workflow Evolution
> "My workflow with Claude Code has been completely changing every three or four weeks"

Be ready to adapt as you learn.

## Key Success Metric
From transcript on latency vs effectiveness:
> "I would argue that if it gives you better results but takes longer... if you zoom out, it's probably going to take you lesser time even with the overhead"

## Related Notes
- [[Sub-agent Context Management]]
- [[Model Selection for Different Agent Tasks]]
- [[Sid's Production Agent Workflow]]
- [[Progressive Refinement Pattern]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Detailed walkthrough of Sid's five-agent workflow