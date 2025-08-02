---
created: 2025-08-02T20:00:00.000Z
uid: 202508021006
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/performance"
  - "#pattern/cost-optimization"
---

# Model Selection for Different Agent Tasks

## Core Insight
Different sub-agent tasks benefit from different models. The new model selection feature allows optimizing for cost, latency, and capability based on task complexity.

## Model Characteristics

### Haiku
- **Best for:** Simple, mechanical tasks
- **Examples:** Running tests, linting, file operations
- **Advantages:** Fast, cheap, reliable for simple tasks
- **Context needs:** Minimal

### Sonnet (Default)
- **Best for:** General implementation, code writing
- **Examples:** Feature implementation, bug fixes, refactoring
- **Advantages:** Good balance of capability and speed
- **Context needs:** Moderate

### Opus
- **Best for:** Complex planning, architecture decisions
- **Examples:** System design, code architecture, complex problem solving
- **Advantages:** Best reasoning capability
- **Context needs:** Can handle large contexts effectively

## Sid's Production Workflow

```yaml
1. Feature Analyzer: Sonnet (could be Haiku)
   - Simple code reading task
   
2. Code Architect: Opus ⭐
   - Complex planning requires best model
   
3. Implementation: Sonnet
   - Executing plan doesn't need Opus
   
4. Code Reviewer: Sonnet
   - Pattern matching and rule checking
   
5. Test Runner: Haiku ⭐
   - Just running commands and summarizing
```

## Decision Framework

### Use Haiku when:
- Task is well-defined and mechanical
- No complex reasoning required
- Speed/cost is priority
- Examples: `npm run test`, formatting, simple searches

### Use Sonnet when:
- Standard coding tasks
- Moderate complexity
- Good default choice
- Examples: Writing functions, fixing bugs, refactoring

### Use Opus when:
- Architecture decisions needed
- Complex problem solving
- Multiple solution paths exist
- Examples: System design, optimization problems, architectural refactoring

## Cost/Performance Trade-offs

From transcript insight:
> "For smaller tasks, like running tests or like running kind of more menial things, you can use Haiku, which can be a big token saver. And also latency can be a big win."

### Latency Comparison (approximate):
- Haiku: Fastest responses
- Sonnet: Moderate latency  
- Opus: Slowest but most thorough

### Token Cost (approximate):
- Haiku: Cheapest
- Sonnet: Moderate
- Opus: Most expensive

## Practical Example

```yaml
agents:
  - name: "test-runner"
    model: "haiku"
    description: "Runs test commands and summarizes results"
    
  - name: "architect" 
    model: "opus"
    description: "Designs system architecture and makes technology decisions"
    
  - name: "implementer"
    model: "sonnet"  
    description: "Implements features based on architectural plans"
```

## Key Quote
> "I find that consistently [Opus] performs better... for the part that's actually executing the plan, I don't think you need Opus. Sonnet is more than good enough for that."

## Related Notes
- [[Sub-agent Context Management]]
- [[Context Window Optimization for Multi-Agent Systems]]
- [[Cost Optimization Strategies for Multi-Agent Systems]]
- [[Sub-agent Performance Patterns]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Model selection feature announcement and Sid's workflow discussion