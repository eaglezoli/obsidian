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
### Baseline

| Item | Before | After | Change / Notes |
|---|---:|---:|---|
| Claude Code version | v2.1.277 | v2.1.277 | Same version |
| Model | Sonnet 5 | Sonnet 5 | Same model |
| Context window | 200k | 200k | Hard context ceiling |
| Fresh-session context | ~43.0k | **25.3k** | ~41% reduction |
| System prompt | ~8.7k | **8.7k** | Essentially unchanged |
| System tools | ~12.7k+ | **9.7k** | Reduced by removing large always-loaded tools |
| Skills | 2.6k | **2.0k** | Reduced via skill trimming / name-only |
| MCP tools | Claude Docs + Top-Rated Online + IDE | **2 IDE tools, 0 tokens** | Claude.ai connectors disabled; remaining MCP tools load on demand |
| Messages on fresh `Hello!` | ~5.5k | **4.9k** | Some variation between fresh sessions |
| Free space before autocompact buffer | Lower | **141.7k** | Based on 25.3k active context |
| Autocompact buffer | 33k | **33k** | Claude Code reserves this before the 200k ceiling |

### Settings changes made

| Setting / Tool | Action | Reason |
|---|---|---|
| `disableClaudeAiConnectors` | `true` | Removed unused Claude.ai connector overhead |
| `enableWorkflows` | `false` | Disabled dynamic workflows not currently used |
| `Artifact` | Denied | Very large tool definition; not needed for normal coding |
| `ScheduleWakeup` | Denied | Only useful for self-paced `/loop` workflows |
| `AskUserQuestion` | Denied | Removed structured-question tool overhead; normal text questions still work |
| `SendFeedback` | Denied | Not needed for normal coding work |
| `artifact-capabilities` | Off | Artifact feature disabled |
| `artifact-diagramming` | Off | Artifact feature disabled |
| `artifact-design` | Off | Artifact feature disabled |
| `schedule` skill | `name-only` | Keeps skill usable without carrying full description every request |
| `loop` skill | `name-only` | Keeps skill usable without carrying full description every request |
| Bundled skills generally | Kept | Useful skills such as `code-review`, `simplify`, `run`, `claude-api` retained |
| ToolSearch / deferred tools | Kept | Important optimisation: loads full tool schemas only when needed |
| Agent / subagents | Kept | Useful for side agents, forks and larger tasks |
| Read / Edit / Write / Bash | Kept | Core coding tools |
| IDE MCP tools | Kept | Deferred, currently 0-token overhead |

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