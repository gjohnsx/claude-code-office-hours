# Claude Code Slash Commands from Claude Code Office Hours

This command is from the [Claude Code Office Hours](https://x.com/trq212/status/1951037643061600710) session presented by developer [Sid Bidasaria](https://x.com/sidbidasaria).

## /new-feature Command

The `/new-feature` command is designed to streamline the feature implementation workflow in Claude Code. 

### How it Works

1. **Initial Summary**: When invoked, the command summarizes the new feature request you're working on
2. **Confirmation**: You confirm the feature summary is accurate
3. **Next Steps**: After confirmation, the workflow should continue with the Feature Analyzer agent

### Uncertainty About Agent Orchestration

**Note**: It's currently unclear whether the subagent orchestration is built into the `/new-feature` slash command itself or if it requires manual invocation. Specifically:

- **Option 1**: The command might automatically invoke the Feature Analyzer agent after you confirm the feature summary
- **Option 2**: You might need to manually tag the `@feature-analyzer` agent yourself after the `/new-feature` command completes

I'll definitely be testing both approaches. 

### Recommended Workflow

Based on the multi-agent workflow discussed in the same Office Hours session, after using `/new-feature`, the typical progression would be:

1. `/new-feature` - Summarize and confirm the feature
2. `@feature-analyzer` - Analyze codebase architecture (either automatic or manual)
3. `@code-architect` - Design implementation approaches
4. Implementation phase
5. `@code-reviewer` - Review the implementation
6. `@code-simplifier` - Simplify if needed (optional)
7. Test runners - Validate the implementation