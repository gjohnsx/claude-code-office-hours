---
created: 2025-08-02T21:00:00.000Z
uid: 202508022001
tags:
  - "#topic/tech/ai/claude-code"
  - "#type/permanent-note"
  - "#pattern/architecture"
  - "#concept/agents"
---

# Claude Code Architecture

## Core Insight
Claude Code is designed as a "pure agent" - instructions + powerful tools + loop until done. This simple architecture enables complex behaviors without heavyweight scaffolding.

## Architecture Components

### 1. Pure Agent Design
From Cal's definition:
> "When we talk about agents, what we really mean is some instructions, some powerful tools, and you let them all just run in a loop until it decides it's done."

### 2. Tool Suite
- **File Operations**: Create, edit, read files
- **Terminal Access**: Full bash capabilities
- **Search Tools**: grep, glob, find
- **MCP Integration**: Extensible tool system

### 3. No Indexing or RAG
Key architectural decision:
> "We don't do any sort of indexing. Instead, Claude explores and understands the code base how you... would explore a code base, through agentic search."

### 4. Lightweight Layers
- **UI Layer**: Watch Claude work in real-time
- **Permission System**: Human-in-the-loop safety
- **Security**: Cloud provider integrations (AWS, GCP)

## Why This Architecture Works

### Simplicity
- No complex preprocessing
- No index maintenance
- No embedding databases
- Direct tool usage

### Flexibility
- Works on any codebase immediately
- No setup required
- Adapts to different project structures
- Scales with codebase size

### Natural Exploration
Claude explores codebases like a human would:
1. Start with high-level structure
2. Search for relevant files
3. Read and understand patterns
4. Make targeted changes

## Agentic Search Pattern

### How It Works
> "The model can go, do some searches, and then look at the results and say, 'Hmm. Maybe I need to figure out a few more things. I'm gonna go do some more searching and then come back.'"

### Tools Used
- `glob` - file pattern matching
- `grep` - content searching  
- `find` - file system navigation
- Custom search iterations

### Advantages Over RAG
- No stale indexes
- Real-time exploration
- Context-aware searching
- Progressive refinement

## Security and Deployment

### Provider Flexibility
- Anthropic API (default)
- AWS Bedrock
- Google Cloud Vertex AI
- On-premise options

### Lightweight Nature
> "Because Claude Code is just such a lightweight layer on top of the model... it's very easy and native to point Claude Code at one of these other services"

## Key Design Principle
From Anthropic philosophy:
> "We try to always do what we call the simple thing that works"

This manifests as:
- Minimal abstraction
- Direct tool access
- No complex state management
- Trust in model capabilities

## Related Notes
- [[Claude Code as Pure Agent]]
- [[Agentic Search vs Traditional RAG]]
- [[Claude Code Tool Design]]
- [[Simple Architecture Principles]]

## Source
- [[Claude Code Best Practices - Cal Rueb]]
- Architecture explanation section of the talk