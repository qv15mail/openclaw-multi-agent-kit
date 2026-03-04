# Scaling Your Team

How to add new agents and teams to your OpenClaw setup.

## Adding a New Agent

### 1. Define the Role

Before creating anything, answer:
- What does this agent DO? (specific scope)
- What does it NOT do? (boundaries)
- Which team does it belong to?
- Who does it escalate to?

### 2. Create the Bot

Go to @BotFather, create a new bot, add it to your supergroup.

### 3. Create the Workspace

```bash
mkdir -p ~/.openclaw/workspace/agents/[name]/
```

Copy and customize templates:
- `SOUL.md` — from the closest matching template
- `IDENTITY.md` — fill in the details

### 4. Update openclaw.json

Add to `agents.list`:
```json
{
  "id": "[name]",
  "workspace": "/home/USER/.openclaw/workspace/agents/[name]/",
  "model": "anthropic/claude-sonnet-4-6"
}
```

Add binding:
```json
{ "agentId": "[name]", "match": { "channel": "telegram", "accountId": "[name]" } }
```

Add channel account with bot token and topic config.

### 5. Update Shared Docs

- Update SUPERGROUP-MAP.md
- Update AGENTS.md (orchestrator workspace)
- Update team SOUL.md files to reference the new teammate

### 6. Restart and Test

```bash
openclaw restart
```

## Adding a New Team

1. Create a new topic in the supergroup
2. Designate a primary agent (requireMention: false)
3. Add secondary agents (requireMention: true)
4. Document the workflow in each agents SOUL.md
5. Update SUPERGROUP-MAP.md

## Model Selection Tips

- **Orchestrator:** Use a strong model (claude-sonnet-4-6 or better)
- **Primary team agents:** Match model to task complexity
- **Secondary/support agents:** Can use lighter models (haiku) to save costs
- **Coding agents:** Use the strongest model you can afford
- **Triage/ops agents:** Lighter models work fine
