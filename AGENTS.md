# Multi-Agent Team Workflow

This project uses OpenCode with a team of specialized agents working together.

## Quick Start

```bash
cd ~/Desktop/super-agent
opencode
```

First run: use `/connect` to set up a free model provider (Zen or GitHub Copilot).

## Agent Team

| Agent | Invoke | Role |
|-------|--------|------|
| @architect | `@architect` | System design, architecture |
| @coder | `@coder` | Code implementation |
| @reviewer | `@reviewer` | Code review |
| @debugger | `@debugger` | Bug fixing |
| @explorer | `@explorer` | Code search/analysis |

## Workflow Examples

### New Feature
```
@architect design a payment system
```
→ Review the architecture, then:
```
@coder implement the payment module per the architecture plan
```
→ After implementation:
```
@reviewer review the new payment code
```

### Debugging
```
@explorer find all places where we handle webhook events
```
Then:
```
@debugger fix the duplicate webhook processing bug
```

## Tips
- Primary agents (Tab to switch): Build (default, full access), Plan (read-only)
- Subagents are invoked via @mention
- `build` agent automatically delegates to subagents when appropriate
- Run `/agents` to list all available agents
