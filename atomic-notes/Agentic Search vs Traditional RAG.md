---
created: 2025-08-02T21:00:00.000Z
uid: 202508022005
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#pattern/architecture"
  - "#concept/search"
---

# Agentic Search vs Traditional RAG

## Core Insight
Claude Code deliberately avoids traditional RAG (Retrieval-Augmented Generation) approaches with indexing and embeddings. Instead, it uses agentic search - the same tools a developer would use to explore a codebase.

## Traditional RAG Approach

### What Most Would Build
Cal's observation:
> "If you're gonna build a coding agent a year ago, you'd probably have ideas like, 'Well, I'll need to figure out which files are relevant. So maybe I'll index the whole code base and embed it and do this fancy RAG retrieval thing.'"

### RAG Characteristics
- Pre-index entire codebase
- Generate embeddings for code
- Vector similarity search
- Retrieve "relevant" chunks
- Static understanding

## Agentic Search Approach

### Claude Code's Method
> "That is not how Claude Code works. We don't do any sort of indexing. Instead, Claude explores and understands the code base how you... would explore a code base, through agentic search."

### Key Components
- **Tools Used**: grep, glob, find, ls
- **No Preprocessing**: Works immediately
- **Dynamic Exploration**: Adapts to findings
- **Iterative Refinement**: Multiple search rounds

## How Agentic Search Works

### The Search Loop
From Cal's explanation:
> "The model can go, do some searches, and then look at the results and it can say, 'Hmm. Maybe I need to figure out a few more things. I'm gonna go do some more searching and then come back.'"

### Example Flow
1. Initial broad search: `grep -r "UserAuth"`
2. Find relevant files
3. Read key files for context
4. Refined search: `grep -r "login.*token"`
5. Trace through dependencies
6. Build understanding progressively

## Advantages of Agentic Search

### 1. No Stale Index
- Always searches current code
- No rebuild needed after changes
- Immediate availability
- No maintenance overhead

### 2. Context-Aware
- Searches based on understanding
- Refines based on findings
- Follows code patterns
- Adapts to project structure

### 3. Human-Like Exploration
- Uses familiar developer tools
- Transparent process
- Debuggable approach
- Learnable patterns

### 4. Zero Setup
- Works on any codebase
- No preprocessing time
- No storage requirements
- No configuration needed

## Disadvantages vs Solutions

### Potential RAG Advantages
- Faster initial retrieval
- Semantic similarity matching
- Cross-file relationships
- Pre-computed relevance

### Why Agentic Search Wins
- Model intelligence compensates
- Real-time adaptation
- Better handling of context
- More accurate results

## Search Patterns in Practice

### Progressive Narrowing
```bash
# Start broad
grep -r "payment"

# Find payment service
grep -r "class.*Payment"

# Trace usage
grep -r "PaymentService"

# Find specific method
grep -r "processPayment"
```

### Cross-Reference Search
```bash
# Find definition
grep -r "function authenticate"

# Find usages
grep -r "authenticate("

# Find tests
find . -name "*test*" | xargs grep "authenticate"
```

### Pattern Recognition
Claude learns project patterns:
- Naming conventions
- Directory structures
- File organizations
- Import patterns

## Performance Implications

### Speed Trade-offs
- Initial search may be slower
- But more accurate results
- Fewer false positives
- Better context understanding

### Scalability
- Works on any size codebase
- No memory requirements
- Linear search complexity
- Optimized by tool choice

## Best Practices for Agentic Search

### 1. Project Structure
Help Claude search efficiently:
```markdown
# claude.md
## Project Structure
- Source code: /src
- Tests: /tests
- Configs: /config
```

### 2. Naming Conventions
Consistent names improve search:
- Clear file names
- Descriptive function names
- Organized directories
- Logical groupings

### 3. Search Hints
Guide initial searches:
```markdown
"The authentication logic is in the /auth directory"
"Look for files ending in .service.ts"
```

## Future Implications

### Model Improvements
As models improve:
- Faster search strategies
- Better pattern recognition
- Smarter exploration
- More efficient paths

### Tool Evolution
Potential enhancements:
- Specialized search tools
- Codebase-aware grep
- Intelligent caching
- Search optimization

## Related Notes
- [[Claude Code Architecture]]
- [[Search-First Development]]
- [[Code Exploration Patterns]]
- [[Terminal-Centric Development]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Architecture discussion and search explanation