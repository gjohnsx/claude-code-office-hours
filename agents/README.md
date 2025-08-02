# Claude Code Sub-Agent Workflow from Claude Code Office Hours

This workflow is from the [Claude Code Office Hours](https://x.com/trq212/status/1951037643061600710) session presented by developer [Sid Bidasaria](https://x.com/sidbidasaria). 

**Note**: These agents were created using Claude Code's built-in agent generation function (`/agents` builder) and don't necessarily reflect exactly what Sid uses in practice. Sid recommends using the `/agents` builder as a starting point, then testing extensively and making your own edits and tweaks until you're satisfied with the performance.

## Agent Workflow Overview

### 1. Feature Analyzer (`/feature-analyzer`)
**Purpose**: Understand the codebase architecture before implementation  
**When to use**: Always run first when implementing new features  
**What it does**:
- Reads code specific to the feature being built
- Analyzes abstraction layers and architectural patterns
- Reports findings back to parent thread for context

### 2. Code Architect (`/code-architect`)
**Purpose**: Design implementation approaches  
**Model**: Requires Opus (only agent that does)  
**When to use**: After feature analysis is complete  
**What it does**:
- Takes feature analyzer's findings as input
- Accepts detailed requirements and implementation preferences
- Reads additional code to understand broader context
- Outputs multiple implementation options
- User selects preferred approach with modifications

**Workflow tip**: Enable "yolo mode" (--dangerously-skip-permissions) to accept all file edits after selecting an approach

### 3. Code Reviewer (`/code-reviewer`)
**Purpose**: Ensure code quality and catch issues  
**When to use**: After implementation is complete  
**What it does**:
- Reviews the implemented code
- Identifies potential bugs or issues
- Suggests improvements

### 4. Code Simplifier (`/code-simplifier`) *[Optional]*
**Purpose**: Improve code readability without changing functionality  
**When to use**: After code review, if complexity can be reduced  
**What it does**:
- Maintains all features and functionality
- Simplifies complex code patterns
- Improves readability and maintainability

### 5. Test Runners (various sub-agents)
**Purpose**: Validate implementation  
**Model**: Can use Haiku for cost efficiency  
**What it does**:
- Execute `npm run test` or equivalent
- Summarize test results
- Report failures back to parent
