---
created: 2025-08-02T20:00:00.000Z
source: "twitter_1951037643061600710_transcript"
title: "Claude Code Office Hours - Sub-agents and Context Management"
speakers: ["Tariq", "Sid"]
tags:
  - "#source/youtube/anthropic"
  - "#type/index"
  - "#topic/tech/ai/claude-code"
  - "#concept/agents/sub-agents"
  - "#tool/claude-code"
---

# Claude Code Office Hours - Sub-agents and Context Management

## Overview
This office hours session with Tariq and Sid from the Claude Code team focused on sub-agents, context management, and building email agents using the Claude Code SDK.

## Key Announcements
1. **Model Selection for Sub-agents** - You can now select which model (Opus/Sonnet/Haiku) each sub-agent uses
2. **Improved Agent Invocation** - New "add agent" syntax makes it easier to use agents

## Core Topics Covered

### 1. [[Sub-agent Context Management]]
- How context flows between parent and sub-agents
- The critical role of the description field
- Context window optimization strategies

### 2. [[Sub-agent Architecture]]
- System prompt vs description field
- When sub-agents spin up and die
- Stateless agent invocations

### 3. [[Practical Sub-agent Workflows]]
- Feature analyzer → Code architect → Implementation flow
- Code reviewer and simplifier agents
- Managing multiple work trees

### 4. [[Building Agents with Claude Code SDK]]
- Local-first email agent architecture
- General tools vs specific constraints
- File-based vs database approaches

## Related Atomic Notes
- [[Sub-agent Description Field Controls Context]]
- [[Parent Agent Context Passing Strategy]]
- [[Model Selection for Different Agent Tasks]]
- [[Async vs Sync Agent Workflows]]
- [[Context Window Management Best Practices]]
- [[Agent Interruption Patterns]]
- [[File Selection and Context Persistence]]

## Key Quotes
- "The description field is what the parent thread gets to figure out when and how to call into the sub-agents"
- "Sub-agents start from a blank slate with a super specific system prompt"
- "You have a lot of control over both context passing and return values just by prompting"

## Practical Insights
- Keep total context under 100k tokens for optimal performance
- Use Haiku for simple tasks like running tests
- Opus for planning, Sonnet for execution
- Description field can enforce context requirements

## Source
- Original transcript: [[twitter_1951037643061600710_transcript]]