## Starting Context

### Resetting Your Config
1. Go to your `settings.json` file and rename it as `settings-backup.json` - this is a backup of your settings before you start the course.
2. Rename your `skills` directory to `skills-backup` as well.
### What's In Your Baseline –```context```

| Category                                                                   | Tokens   |
| -------------------------------------------------------------------------- | -------- |
| [System prompt](https://www.aihero.dev/ai-coding-dictionary/system-prompt) | 3k       |
| System tools                                                               | 17.9k    |
| MCP tools (deferred)                                                       | 24.5k    |
| System tools (deferred)                                                    | 16.9k    |
| Skills                                                                     | 2k       |
| Messages                                                                   | 8        |
| **Total**                                                                  | **~23k** |
![[fresh-context-example.png|Terminal output showing /context command results with 22.9k tokens used by default configuration]]
## My Optimisation
## Claude Code Context Optimisation Baseline

### Baseline

| Item | Before | After | Change / Notes |
|---|---:|---:|---|
| Claude Code version | v2.1.277 | v2.1.277 | Same version |
| Model | Sonnet 5 | Sonnet 5 | Same model |
| Context window | 200k | 200k | Hard context ceiling |
| Fresh-session context | ~43.0k | **25.3k** | ~41% reduction |
| System prompt | ~8.7k | **8.7k** | Essentially unchanged |
| System tools | 12.7k | **9.7k** | Reduced by removing large always-loaded tool schemas |
| Skills | 2.6k | **2.0k** | Reduced via skill trimming / `name-only` |
| MCP tools | Claude Docs + Top-Rated Online + IDE | **2 IDE tools, 0 tokens** | Claude.ai connectors disabled; remaining MCP tools load on demand |
| Messages on fresh `Hello!` | ~5.5k | **4.9k** | Some fresh-session variation |
| Free space before autocompact buffer | Lower | **141.7k** | Based on 25.3k active context |
| Autocompact buffer | 33k | **33k** | Reserved before reaching the 200k ceiling |

### Optimisation changes

| Setting / Tool | Action | Reason / Notes |
|---|---|---|
| `disableClaudeAiConnectors` | `true` | Removes unused Claude.ai connector overhead |
| `enableWorkflows` | `false` | Disables dynamic workflows not currently used |
| `Artifact` | Denied via `permissions.deny` | Temporary workaround. The documented toggle is `enableArtifact: false`, but Claude Code currently has an open bug where that also removes the scratchpad directory |
| `ScheduleWakeup` | Denied | Not needed unless using self-paced `/loop` workflows |
| `AskUserQuestion` | Denied | Removes its schema from context; normal text questions still work |
| `SendFeedback` | Denied | Removes an unused always-loaded tool schema |
| `artifact-capabilities` | `off` | Artifact feature currently disabled |
| `artifact-diagramming` | `off` | Artifact feature currently disabled |
| `artifact-design` | `off` | Artifact feature currently disabled |
| `schedule` skill | `name-only` | Skill remains usable while only its name is kept in context |
| `loop` skill | `name-only` | Skill remains usable while only its name is kept in context |
| Bundled skills generally | Kept | Useful skills such as `code-review`, `simplify`, `run`, `claude-api` retained |
| ToolSearch / deferred tools | Kept | Important optimisation: full tool schemas load only when needed |
| Agent / subagents | Kept | Useful for forks, side agents and larger tasks |
| Read / Edit / Write / Bash | Kept | Core coding tools |
| IDE MCP tools | Kept | Deferred and currently 0-token overhead |
| `modelSettings` / Sonnet 5 effort | `medium` | Deliberate choice for general coding. Sonnet 5 default is `high`; use `/effort high` per-session for harder tasks |

### Important behaviour confirmed

| Behaviour | Confirmed |
|---|---|
| Bare tool names in `permissions.deny` remove the tool schema from Claude's context entirely | **Yes** |
| Scoped deny rules only block matching calls while leaving the tool itself available | **Yes** |
| `enableArtifact: false` is the documented Artifact toggle | **Yes** |
| `enableArtifact: false` currently has a scratchpad-removal bug | **Yes, keep the permission-deny workaround for now** |
| Sonnet 5 default effort is `high` | **Yes** |
| Current `medium` effort is intentional | **Yes** |

### Final `settings.json`

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",

  "permissions": {
    "defaultMode": "auto",
    "deny": [
      "Artifact",
      "ScheduleWakeup",
      "SendFeedback",
      "AskUserQuestion"
    ]
  },

  "modelSettings": {
    "claude-sonnet-5": {
      "effortLevel": "medium"
    }
  },

  "skillOverrides": {
    "artifact-capabilities": "off",
    "artifact-diagramming": "off",
    "artifact-design": "off",
    "schedule": "name-only",
    "loop": "name-only"
  },

  "disableClaudeAiConnectors": true,
  "enableWorkflows": false,

  "theme": "auto",
  "inputNeededNotifEnabled": true,
  "agentPushNotifEnabled": true
}