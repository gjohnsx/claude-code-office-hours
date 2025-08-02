---
created: 2025-08-02T20:00:00.000Z
uid: 202508021010
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/control"
  - "#limitation"
---

# Agent Interruption and Control

## Core Insight
Current sub-agent interruption in Claude Code is abrupt - it "kills" the agent without graceful handling. This is acknowledged as a limitation that needs improvement.

## Current State

### What Happens Now
From transcript:
> "Our interruption flow right now is not great, to be honest. When you interrupt a sub-agent, it just kind of kills it"

### Problems with Current Approach:
- No graceful shutdown
- No partial results saved
- No cleanup operations
- Abrupt termination

## Why Interruption Matters

### User Control
- Long-running agents need stop capability
- Wrong direction detection
- Resource management
- Emergency stops

### Workflow Flexibility
- Pivoting mid-task
- Correcting misunderstandings
- Adjusting approach
- Time management

## Desired Interruption Patterns

### 1. Graceful Shutdown
```
User: [Interrupts]
Agent: "Stopping current task. Here's what I completed:
        - ✓ Analysis phase
        - ⚠ Partial implementation
        - ✗ Testing not started"
```

### 2. Checkpoint and Resume
```
Interrupt → Save State → Option to Resume Later
```

### 3. Partial Results
Return what's been accomplished:
- Completed analyses
- Partial code changes
- Discovered insights

## Challenges with Agent-to-Agent Interruption

From transcript:
> "Interruption in general, especially when it comes to agent to agent stuff, it's kind of tricky"

### Complex Scenarios:
- Parent interrupting child
- Cascading interruptions
- Mid-transaction stops
- Dependent agent chains

## Workaround Strategies

### 1. Shorter Agent Tasks
Break work into smaller chunks:
- More interruption points
- Natural checkpoints
- Reduced loss on interrupt

### 2. Explicit Checkpoints
```yaml
system_prompt: "After each major step, summarize progress so far before continuing"
```

### 3. Time-Boxed Operations
```yaml
description: "Analyzer that works for max 2 minutes then returns findings"
```

## Future Considerations

### Message Queuing
Mentioned concept:
> "You can queue up messages"

Could enable:
- Deferred interruptions
- Message-based control
- Async command handling

### Fork on Interrupt
> "You can fork the thread if you really need to"

Possibilities:
- Save current state
- Start new direction  
- Preserve both paths

## Best Practices Given Current Limitations

### 1. Design Interruptible Workflows
- Small, atomic tasks
- Clear phase boundaries
- Regular status updates

### 2. Set User Expectations
- Warn before long operations
- Indicate non-interruptible sections
- Provide progress indicators

### 3. Manual Progress Tracking
Since agents don't save state:
- Parent tracks progress
- Log completed steps
- Enable manual recovery

## Community Feedback
From transcript:
> "I think a lot of users have also said that [interruption flow isn't great]"

This is a known pain point with active consideration for improvement.

## Key Quote
> "We want to make that better and hopefully we will soon"

## Related Notes
- [[Sub-agent State and Persistence]]
- [[Agent Error Handling Patterns]]
- [[User Control in Agent Systems]]
- [[Graceful Degradation in AI Workflows]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Discussion of interruption limitations and future improvements