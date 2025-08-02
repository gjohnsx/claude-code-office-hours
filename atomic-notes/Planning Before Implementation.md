---
created: 2025-08-02T21:00:00.000Z
uid: 202508022009
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#pattern/workflow"
  - "#pattern/best-practices"
---

# Planning Before Implementation

## Core Insight
Using Claude Code as a thought partner for planning before implementation significantly improves outcomes and reduces wasted effort. This underutilized pattern leverages Claude's reasoning abilities before committing to code changes.

## The Planning Pattern

### Cal's Recommendation
> "One thing you can use Claude Code for, and I think this is underrated, is instead of just diving in and starting to work, you can use Claude Code as a thought partner."

### How to Request Planning
Instead of:
```
"Fix the authentication bug"
```

Use:
```
"I have this authentication bug. Can you search around, figure out what's causing it, and just tell me a plan how we're gonna fix it?"
```

## Benefits of Planning First

### 1. Validation Before Action
From Cal:
> "This can save you a lot of time because you can verify, you can read Claude's plan and you can verify what it's going to do."

### 2. Multiple Options
Example request:
```
"I'm thinking about implementing this feature. Can you search around and figure out how we would do it and report back with two or three different options? Don't start writing any files yet."
```

### 3. Reduced Context Usage
- Planning uses less context than trial-and-error
- Avoids accumulating failed attempts
- Cleaner context for implementation
- More room for actual work

## Planning Patterns

### 1. Bug Investigation Plan
```
"This bug is happening: [description]. Search the codebase and create a plan to fix it, including:
1. Root cause analysis
2. Files that need changes
3. Potential side effects
4. Testing approach"
```

### 2. Feature Implementation Plan
```
"We need to add [feature]. Explore the codebase and suggest:
1. Where to add the code
2. Existing patterns to follow
3. Integration points
4. 2-3 implementation approaches"
```

### 3. Refactoring Plan
```
"This code needs refactoring. Analyze it and propose:
1. Current problems
2. Refactoring strategy
3. Order of operations
4. Risk assessment"
```

## Integration with Todo Lists

### Cal's Observation
> "Often when Claude's working on a big task, it'll create a to-do list. And if you're paying attention, you can watch this to-do list, and if you see anything weird or something that doesn't make sense, that's when you can press Escape"

### Todo List Benefits
- Visual progress tracking
- Early error detection
- Intervention points
- Clear task breakdown

### Managing Todo Lists
```
"Hey Claude, let's change the to-do list. I think you're on the wrong path."
```

## Planning Best Practices

### 1. Be Specific About Constraints
```
"Create a plan considering:
- We can't modify the database schema
- Must maintain backward compatibility
- Should complete in under 2 hours"
```

### 2. Request Trade-offs
```
"For each approach, explain:
- Pros and cons
- Time estimates
- Complexity level
- Long-term implications"
```

### 3. Incremental Planning
Start broad, then narrow:
```
1. "What are the main approaches?"
2. "Let's go with option 2, plan the details"
3. "Break down step 3 into subtasks"
```

## When to Plan vs When to Act

### Always Plan For:
- Complex features
- Bug fixes in unfamiliar code
- Architecture changes
- Performance optimizations
- Security-related changes

### Direct Action OK For:
- Simple typo fixes
- Adding comments
- Formatting changes
- Well-defined small tasks
- Repetitive operations

## Planning Output Formats

### Structured Plan Request
```
"Provide a plan with:
# Summary
# Affected Files
# Step-by-Step Implementation
# Testing Strategy
# Rollback Plan"
```

### Decision Matrix Format
```
"Compare approaches using:
| Approach | Complexity | Time | Risk | Recommendation |
|----------|-----------|------|------|----------------|"
```

## Common Planning Mistakes

### 1. Too Vague
❌ "Plan how to make this better"
✅ "Plan how to improve performance by reducing database calls"

### 2. No Constraints
❌ "How should we implement auth?"
✅ "How should we implement JWT auth using existing user table?"

### 3. Skipping Exploration
❌ "Plan based on what you know"
✅ "Search the codebase first, then plan based on findings"

## Advanced Planning Techniques

### 1. Risk-First Planning
```
"Before planning implementation, identify:
- What could break?
- Security implications?
- Performance impacts?
- User experience changes?"
```

### 2. Iterative Refinement
```
Round 1: "High-level approaches"
Round 2: "Detailed plan for chosen approach"
Round 3: "Edge cases and error handling"
```

### 3. Planning Validation
```
"Here's my understanding of your plan: [summary]. 
Is this correct? Any adjustments needed?"
```

## Measuring Planning Success

### Good Plans Have:
- Clear steps
- Identified files
- Risk assessment
- Time estimates
- Success criteria

### Warning Signs:
- Vague descriptions
- Missing edge cases
- No testing strategy
- Unclear dependencies
- Optimistic estimates

## Related Notes
- [[Think Hard Between Tool Calls]]
- [[Context Management in Claude Code]]
- [[Todo List Workflow]]
- [[Efficient Claude Code Workflows]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Multiple sections on planning and thought partnership