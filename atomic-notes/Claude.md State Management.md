---
created: 2025-08-02T21:00:00.000Z
uid: 202508022002
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#pattern/state-management"
  - "#pattern/best-practices"
---

# Claude.md State Management

## Core Insight
Claude Code has no built-in memory between sessions. The claude.md file serves as the primary state management mechanism, providing persistent context and instructions across sessions and team members.

## How claude.md Works

### Loading Mechanism
From Cal's explanation:
> "When we start Claude, if there's this claude.md file in the working directory, it's just plopped into context, it's plopped into the prompt, and basically what it says is, 'Hey Claude, by the way, these are important instructions the developer left for you.'"

### File Locations (Priority Order)
1. **Project Directory** - Most specific, project context
2. **Sub-directories** - Read when discovered during search
3. **Home Directory** - Global preferences and settings

## What to Include in claude.md

### Project Structure
```markdown
## Project Layout
- `/src` - Main application code
- `/tests` - Unit and integration tests
- `/docs` - Documentation
- `/scripts` - Build and utility scripts
```

### Development Commands
```markdown
## Commands
- Run tests: `npm test`
- Build: `npm run build`
- Type check: `npm run typecheck`
- Lint: `npm run lint`
```

### Style Guidelines
```markdown
## Code Style
- Use TypeScript strict mode
- Prefer functional components
- No inline comments explaining "what"
- Focus comments on "why"
```

### Team Conventions
```markdown
## Conventions
- All new features need unit tests
- Use conventional commits
- PR descriptions should include "Why" section
```

## Advanced claude.md Features

### File References
New feature for including other files:
```markdown
# Include other documentation
@architecture.md
@style-guide.md
@team-conventions.md
```

### Context Management
- Not all subdirectory claude.md files are auto-loaded
- Prevents context explosion in monorepos
- Claude discovers and reads relevant ones during search

## Best Practices

### 1. Keep It Focused
- Project-specific information only
- Avoid generic programming advice
- Focus on unique aspects of your codebase

### 2. Update Regularly
From Cal:
> "You can build these things up over time"

Add information as you discover Claude needs it.

### 3. Team Sharing
- Check claude.md into version control
- Ensure consistent behavior across team
- Document team decisions and patterns

### 4. Model-Specific Adjustments
With Claude 4's better instruction following:
> "It might be a good chance to go look in your claude.md and decide, do I still need this stuff? Maybe I can take some of it out."

## Common Use Cases

### 1. Test Running
```markdown
## Testing
Always run `npm test` after making changes
Test files are in `__tests__` directories
```

### 2. Architecture Decisions
```markdown
## Architecture
We use Redux for state management
API calls go through /api service layer
Components should be pure when possible
```

### 3. Security Requirements
```markdown
## Security
Never commit .env files
Use environment variables for secrets
All user input must be sanitized
```

## Limitations and Workarounds

### No Dynamic State
- claude.md is static between sessions
- Can't store runtime information
- Use file system for dynamic state

### Model Compliance
Some models follow instructions better:
- Claude 3.7 had issues with comment instructions
- Claude 4 follows claude.md more closely

## Related Notes
- [[Context Management in Claude Code]]
- [[File-Based Agent Communication]]
- [[Project Configuration Best Practices]]
- [[Team Knowledge Sharing]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Extensive discussion of claude.md throughout the talk