---
created: 2025-08-02T20:00:00.000Z
uid: 202508021008
tags:
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#type/permanent-note"
  - "#pattern/architecture"
  - "#pattern/workflow"
---

# Async vs Sync Agent Workflows

## Core Insight
Claude Code currently supports only synchronous sub-agent execution, but there's significant discussion about async patterns. The synchronous model provides predictability but limits parallelization opportunities.

## Current Model: Synchronous Sequential

### How It Works Now
```
Parent Agent
  ├─→ Sub-agent A (waits for completion)
  ├─→ Sub-agent B (waits for completion)  
  └─→ Sub-agent C (waits for completion)
```

### Characteristics
- One agent at a time
- Parent waits for each result
- Clear execution order
- No parallel work

## Desired Async Patterns

### 1. Parallel Independent Tasks
```
Parent Agent
  ├─→ Sub-agent A ──┐
  ├─→ Sub-agent B ──┼─→ Merge Results
  └─→ Sub-agent C ──┘
```

Use case: Running tests, linting, and security scans simultaneously

### 2. Fire-and-Forget
From transcript suggestion:
> "A subagent that forks your current main agent thread... something that just you spin it off and it just goes and does its thing. You don't really care if it comes back"

Use cases:
- Background monitoring
- Notification sending
- Log processing

### 3. Event-Driven Chains
```
File Change → Triggers Test Agent → Triggers Deploy Agent
                                  ↘ Triggers Notify Agent
```

## Challenges with Async (From Discussion)

### File System Conflicts
Key concern from transcript:
> "If you give write access to sub-agents and they're going in parallel, you have to deal with conflicts that arise from that"

### Solutions Being Considered:
- Conflict resolution strategies
- File locking mechanisms
- Merge strategies
- Transaction-like operations

### Context Synchronization
- How to merge parallel agent insights
- Handling contradictory conclusions
- Maintaining coherent state

## Current Workarounds

### 1. Multiple Work Trees
Sid's approach:
> "I have like four git work trees... I can work on like four things"

Each tree can have its own agent working sequentially.

### 2. Manual Orchestration
```bash
# Start multiple terminal sessions
# Run different agents in each
# Manually merge results
```

### 3. Background Processes
Using system tools:
```bash
# Agent writes script
echo "npm test" > background_test.sh
# Execute in background
nohup ./background_test.sh &
```

## Future Parallelization Potential

From transcript insight:
> "I think it's going to get increasingly more parallel, right? As models get better at understanding things and being more agentic without needing to steer them"

### Enabling Factors:
- Better autonomous agents
- Improved conflict resolution
- Smarter context merging
- Lower need for human steering

## Design Considerations

### When Sync is Better:
- Dependent tasks
- Shared resource access
- Need strict ordering
- Debugging/transparency

### When Async Would Help:
- Independent analyses
- Multiple test suites
- Parallel searches
- Background monitoring

## Key Quote on Performance Impact
> "It adds more perceived latency to your task, right? Because now your sub-agent needs to spin up... But that's also its super power in some ways"

Trade-off: Latency vs effectiveness

## Related Notes
- [[Sub-agent Communication Patterns]]
- [[Agent Orchestration Patterns]]
- [[Parallel Software Engineering with AI]]
- [[Git Worktree Strategy for Parallel Development]]

## Source
- [[Claude Code Office Hours - Sub-agents and Context]]
- Extensive discussion on async agents and parallelization challenges