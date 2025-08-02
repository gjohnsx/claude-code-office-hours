---
created: 2025-08-02T21:00:00.000Z
source: "youtube_2025-07-31_Claude_Code_best_practices_elevenlabs"
title: "Claude Code Best Practices"
speaker: "Cal Rueb"
event: "Code w/ Claude San Francisco"
date: 2025-05-22
tags:
  - "#source/youtube/anthropic"
  - "#type/presentation"
  - "#topic/tech/ai/claude-code"
  - "#pattern/best-practices"
  - "#tool/claude-code"
---

# Claude Code Best Practices - Cal Rueb

## Overview
Cal Rueb, Member of Technical Staff at Anthropic and core contributor to Claude Code, presents best practices for using Claude Code effectively. He covers the tool's architecture, use cases, and practical tips from both internal use and customer feedback.

## Speaker Background
- Joined Anthropic 1.5 years ago on Applied AI team
- Helps customers build products on Claude
- Became top internal user of Claude Code over a weekend
- Now core contributor focusing on prompting, tools, and evaluation

## Key Topics Covered

### 1. [[Claude Code Architecture]]
- Pure agent design philosophy
- Tools and agentic search approach
- No indexing or RAG - uses terminal tools
- Lightweight UI and permission layer

### 2. [[Claude.md File Best Practices]]
- Primary state management mechanism
- Project-specific instructions
- Team sharing capabilities
- Placement strategies

### 3. [[Context Management in Claude Code]]
- 200k token context window
- /clear vs /compact strategies
- Context accumulation patterns
- Efficient session management

### 4. [[Multi-Agent Workflows]]
- Running multiple Claude instances
- State sharing between agents
- Orchestration patterns
- File-based communication

### 5. [[Advanced Claude Code Techniques]]
- Think hard / extended thinking
- IDE integrations
- Permission management
- Tool expansion with MCPs

## Related Atomic Notes
- [[Claude Code as Pure Agent]]
- [[Agentic Search vs Traditional RAG]]
- [[Claude.md State Management]]
- [[Context Window Management Strategies]]
- [[Multi-Claude Orchestration]]
- [[Permission Management Best Practices]]
- [[Think Hard Between Tool Calls]]
- [[File-Based Agent Communication]]

## Key Insights
- Claude Code is "like that coworker that does everything on the terminal"
- No memory between sessions - claude.md is the state mechanism
- Agentic search outperforms traditional indexing for code understanding
- Context management is crucial for long sessions
- Multiple Claude instances can be orchestrated for complex tasks

## Practical Takeaways
1. Always use claude.md files for project context
2. Configure permissions for faster workflows
3. Use /compact instead of /clear for continuity
4. Install CLI tools over MCPs when available
5. Use planning before implementation
6. Monitor todo lists for course correction
7. Escape is your best friend (press twice to jump back)

## Source
- Original file: [[youtube_2025-07-31_Claude_Code_best_practices_elevenlabs]]