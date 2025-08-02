---
created: 2025-08-02T21:00:00.000Z
uid: 202508022006
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#feature/claude-4"
  - "#pattern/reasoning"
---

# Think Hard Between Tool Calls

## Core Insight
Claude 4 introduces the ability to "think" between tool calls, showing its reasoning process in light gray text. This represents a significant improvement in problem-solving capability, especially for complex debugging and exploration tasks.

## The Evolution

### Previous Limitation
Cal explains:
> "With our past models, we wouldn't let our model think between tool calls, and that's probably when the thinking matters most."

### Claude 4 Enhancement
> "Starting with Claude 4, our models now think between tool calls, and we can watch this happen."

## How It Works

### Visual Indication
- Light gray text shows thinking
- Appears between tool calls
- Shows reasoning process
- Indicates deeper analysis

### Triggering Extended Thinking
```
"think hard about this"
"think step by step"
"reason through this carefully"
```

### Example Flow
From Cal's demo:
1. User: "Figure out what's in this project, think hard"
2. Claude shows thinking (gray text)
3. Calls file reading tool
4. More thinking about findings
5. Calls search tool based on reasoning
6. Continues pattern

## Benefits of Inter-Tool Thinking

### 1. Better Tool Selection
Claude can reason about:
- Which tool to use next
- What parameters to pass
- How to interpret results
- When to stop searching

### 2. Improved Debugging
- Reasons through error messages
- Connects disparate clues
- Forms hypotheses
- Tests assumptions

### 3. Smarter Exploration
- Builds mental model progressively
- Adjusts strategy based on findings
- Avoids redundant operations
- Finds non-obvious connections

## Practical Applications

### Complex Bug Hunting
```
"Find why users are getting logged out randomly, think hard about possible causes"
```
Claude will:
- Reason about authentication flow
- Search strategically
- Connect timeout settings to session management
- Form comprehensive hypothesis

### Architecture Understanding
```
"Understand how the payment system works, think carefully about the flow"
```
Claude will:
- Map out component relationships
- Reason about data flow
- Identify key integration points
- Build complete mental model

### Performance Analysis
```
"Figure out why this endpoint is slow, reason through possible bottlenecks"
```
Claude will:
- Analyze code paths
- Reason about database queries
- Consider caching implications
- Identify optimization opportunities

## Best Practices

### 1. When to Request Thinking
Use for:
- Complex debugging tasks
- Architecture exploration
- Non-obvious problems
- Multi-step reasoning

### 2. Combining with Planning
```
"Think hard about this problem, then give me a plan before implementing"
```

### 3. Observing Thinking Patterns
Watch for:
- Hypothesis formation
- Strategy adjustment
- Connection making
- Dead-end recognition

## Impact on Workflow

### Reduced Trial and Error
- Less random searching
- More targeted exploration
- Fewer wasted operations
- Better first attempts

### Improved Accuracy
- Catches edge cases
- Considers alternatives
- Validates assumptions
- Double-checks logic

### Enhanced Learning
Users can:
- See Claude's reasoning
- Learn problem-solving patterns
- Understand decision making
- Improve own skills

## Technical Details

### Model Capability
- Only available in Claude 4+
- Requires model support
- Not retroactively available
- Performance overhead acceptable

### UI Integration
- Thinking shown inline
- Different visual style
- Can be lengthy
- Provides transparency

## Common Thinking Patterns

### 1. Hypothesis Testing
```
"Hmm, if the issue is authentication, I should check:
- Token expiration
- Session management
- Cookie settings"
```

### 2. Strategic Planning
```
"I need to understand the data flow, so I'll:
1. Find the entry point
2. Trace through middleware
3. Check database queries"
```

### 3. Error Analysis
```
"This error suggests a type mismatch. Let me:
- Check the interface definition
- Find where it's implemented
- Verify the data source"
```

## Future Implications

### Cognitive Architecture
- More sophisticated reasoning
- Better problem decomposition
- Advanced strategy formation
- Human-like thought processes

### Tool Usage Evolution
- Smarter tool selection
- Optimal parameter choices
- Efficient search strategies
- Reduced context usage

## Related Notes
- [[Claude 4 Model Improvements]]
- [[Debugging with Claude Code]]
- [[Extended Thinking Patterns]]
- [[Tool Selection Strategies]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Live demonstration of thinking between tool calls