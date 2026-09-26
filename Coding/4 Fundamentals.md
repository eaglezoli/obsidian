## Starting Context

### Resetting Your Config
1. Go to your `settings.json` file and rename it as `settings-backup.json` - this is a backup of your settings before you start the course.
2. Rename your `skills` directory to `skills-backup` as well.
### What's In Your Baseline: `context`

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

| Item                                 |                               Before |                     After | Change / Notes                                                    |
| ------------------------------------ | -----------------------------------: | ------------------------: | ----------------------------------------------------------------- |
| Claude Code version                  |                             v2.1.277 |                  v2.1.277 | Same version                                                      |
| Model                                |                             Sonnet 5 |                  Sonnet 5 | Same model                                                        |
| Context window                       |                                 200k |                      200k | Hard context ceiling                                              |
| Fresh-session context                |                               ~43.0k |                 **25.3k** | ~41% reduction                                                    |
| System prompt                        |                                ~8.7k |                  **8.7k** | Essentially unchanged                                             |
| System tools                         |                                12.7k |                  **9.7k** | Reduced by removing large always-loaded tool schemas              |
| Skills                               |                                 2.6k |                  **2.0k** | Reduced via skill trimming / `name-only`                          |
| MCP tools                            | Claude Docs + Top-Rated Online + IDE | **2 IDE tools, 0 tokens** | Claude.ai connectors disabled; remaining MCP tools load on demand |
| Messages on fresh `Hello!`           |                                ~5.5k |                  **4.9k** | Some fresh-session variation                                      |
| Free space before autocompact buffer |                                Lower |                **141.7k** | Based on 25.3k active context                                     |
| Autocompact buffer                   |                                  33k |                   **33k** | Reserved before reaching the 200k ceiling                         |

### Optimisation changes


| Setting / Tool                                                       | Action                              | Reason / Notes                                                                                                                                                                                     |
| -------------------------------------------------------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `disableClaudeAiConnectors`                                          | `true`                              | Removes unused Claude.ai connector overhead                                                                                                                                                        |
| `disableWorkflows`                                                   | `true`                              | **Corrected from `enableWorkflows: false`** — this is the documented setting for turning off dynamic workflows for yourself                                                                        |
| `Artifact`                                                           | Denied via `permissions.deny`       | Temporary workaround. Documented toggle (`enableArtifact: false`) currently has an open bug that also removes the scratchpad directory                                                             |
| `ScheduleWakeup`                                                     | **Removed from deny**               | Required for self-paced `/loop` (no fixed interval) to reschedule or stop itself — denying it breaks that feature, which you're keeping (`loop: name-only`)                                        |
| `AskUserQuestion`                                                    | **Removed from deny**               | This is the actual interactive multiple-choice mechanism, not just schema overhead — denying it would have forced plain-text fallback, contradicting the stated goal of keeping that functionality |
| `SendFeedback`                                                       | Denied                              | Removes an unused always-loaded tool schema                                                                                                                                                        |
| `artifact-capabilities` / `artifact-diagramming` / `artifact-design` | `off`                               | Kept off; not made redundant by the Artifact deny rule, but harmless either way since they'd never fire without it                                                                                 |
| `schedule` skill                                                     | `name-only`                         | Skill remains usable while only its name is kept in context                                                                                                                                        |
| `loop` skill                                                         | `name-only`                         | Skill remains usable while only its name is kept in context                                                                                                                                        |
| Bundled skills generally                                             | Kept                                | Useful skills such as `code-review`, `simplify`, `run`, `claude-api` retained                                                                                                                      |
| ToolSearch / deferred tools                                          | Kept                                | Full tool schemas load only when needed                                                                                                                                                            |
| Agent / subagents                                                    | Kept                                | Useful for forks, side agents and larger tasks                                                                                                                                                     |
| Read / Edit / Write / Bash                                           | Kept                                | Core coding tools                                                                                                                                                                                  |
| IDE MCP tools                                                        | Kept                                | Deferred and currently 0-token overhead                                                                                                                                                            |
| `modelSettings` / Sonnet 5 effort                                    | `medium`                            | Deliberate choice for general coding. Sonnet 5 default is `high`; use `/effort high` per-session for harder tasks                                                                                  |
| `statusLine` (ccstatusline)                                          | Kept, via `npx ccstatusline@latest` | Real, current package. Consider pinning a version or installing locally instead of `@latest` — runs on every prompt, no review step on updates                                                     |

### Important behaviour confirmed

|Behaviour|Confirmed|
|---|---|
|Bare tool names in `permissions.deny` remove the tool schema from Claude's context entirely|**Yes**|
|Scoped deny rules only block matching calls while leaving the tool itself available|**Yes**|
|`AskUserQuestion`, `ScheduleWakeup`, `SendFeedback` are all current, valid, non-deprecated tool names|**Yes** — checked against the live tools reference|
|`enableArtifact: false` is the documented Artifact toggle; `disableArtifact` is its deprecated predecessor (same underlying flag)|**Yes**|
|Both Artifact toggles currently trigger the scratchpad-removal bug (#93746, open)|**Yes — keep the `permissions.deny` workaround for now**|
|`disableWorkflows: true` is the documented way to turn workflows off for yourself|**Yes**|
|Sonnet 5 default effort is `high`; current `medium` setting is intentional|**Yes**|

### Final `settings.json`

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",

  "permissions": {
    "defaultMode": "auto",
    "deny": [
      "Artifact",
      "SendFeedback"
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
  "disableWorkflows": true,

  "theme": "auto",

  "inputNeededNotifEnabled": true,
  "agentPushNotifEnabled": true,

  "statusLine": {
    "type": "command",
    "command": "npx ccstatusline@latest"
  }
}
```

## Showing Context in the Status Line

Claude Code doesn't show your [context window](https://www.aihero.dev/ai-coding-dictionary/context-window) usage by default. You need to set this up yourself if you want to monitor it constantly while you're coding.

Having that number right in your status line, visible at a glance, gives you the feedback you need to make good decisions about your [session](https://www.aihero.dev/ai-coding-dictionary/session). We'll use [`ccstatusline`](https://www.npmjs.com/package/ccstatusline), a community tool that formats Claude Code's session data into a clean status line.

## Codebase Exploration

```
Give me a much more in-depth understanding about the different parts of the app, the different modules inside it, and go ahead and read a ton of source code to give me more information. Use subagents.
```

This explicit mention of sub-agents should prompt the agent to spawn sub-agents to do the exploration.

## `/teach` skill

### Setting up the teaching workspace

The `/teach` [skill](https://www.aihero.dev/ai-coding-dictionary/skill) puts together several key files to ground your learning. Here's what gets created:

- `MISSION.md` — Your learning goal and success criteria
- `NOTES.md` — A learner profile describing what you know and what you don't
- `RESOURCES.md` — [Primary sources](https://www.aihero.dev/ai-coding-dictionary/primary-source) like official docs and community links
- `assets/lesson.css` and `assets/quiz.js` — Shared stylesheets and quiz components that every future lesson reuses
- `lessons/` — HTML lessons designed for your exact level
- `reference/glossary.html` — A reference doc you'll return to
- `learning-records/` — [Stateful](https://www.aihero.dev/ai-coding-dictionary/stateful) records of where you are in your learning journey
### Getting the most from /teach

This is the technique recommended for learning any new repository:

1. Create a new teaching workspace just for that repo
2. Tell the agent where you're at
3. Tell it what you understand
4. Tell it what you don't understand
5. Let it teach you

## Build a Feature

### Summary: What Went Right and Wrong

|Aspect|Result|
|---|---|
|Exploration|Thorough, no [subagent](https://www.aihero.dev/ai-coding-dictionary/subagent) needed|
|Implementation|Complete end-to-end feature|
|Testing|Comprehensive: unit, type, integration, smoke tests|
|Token usage|~75k for build, ~90k total (smart zone)|
|Production bug|Shipped a critical bundling issue|
|Bug fix|Identified and resolved quickly once feedback was provided|
The agent demonstrated solid engineering practices: exploration, test-driven development, verification, and the ability to learn from feedback. However, it did ship a bug that broke interactive features, suggesting gaps in how it reasons about client vs. server boundaries in modern frameworks.

## Why Plan Mode Sucks
### The critical issue: plan mode is still rushing

Here's the problem: instead of rushing to create an implementation, the agent rushed to create a plan which reads exactly like the implementation would. It's still rushing to create an asset. The plan is the asset now, not the code.

### The root cause: sycophantic trait of agents

This feeling of premature completion, of rushing to get to the end, is a [sycophantic](https://www.aihero.dev/ai-coding-dictionary/sycophancy) trait of agents. When you tell it you want to produce something, it will go produce that thing.

It won't necessarily stop to make sure it's done the legwork to ensure you're aligned on how it should look.

This is really bad because it leads to a failure mode that happens constantly: the agent builds the wrong thing.

## The Grill-Execute-Clear Loop

### The Grilling Skill: `/grill-me`

The grilling skill works by building a design tree. Every decision branches into the decisions that hang off it.

It asks questions in rounds. The frontier is every decision whose prerequisites are already settled. The skill asks the whole frontier at once, then waits for your answers.

As you answer, the frontier expands. New questions unlock. Previously blocked decisions become answerable.

The [session](https://www.aihero.dev/ai-coding-dictionary/session) ends when the frontier is empty: every branch visited, nothing left silently assumed. Only then should you implement.

### Round 1: The Strategic Questions

Do not answer each question separately. You dictate one long paragraph, covering all the answers.

### Round 2: The Implementation Layer

### The Spec
You do not need to read it. Your answers throughout the [session](https://www.aihero.dev/ai-coding-dictionary/session) have already encoded all the decisions. The spec is just a confirmation - proof that you and the agent share the same understanding.

However, if the [grilling](https://www.aihero.dev/ai-coding-dictionary/grilling) session took a weird twisty turn, you might want to skim it. In this case, everything feels aligned.

### The Loop

This is one cycle of the grill-execute-clear loop:

1. **Grill**: Ask clarifying questions until you and the agent share a mental model
2. **Execute**: Build the feature with confidence, context still warm
3. **Clear**: Once the feature is done and committed, clear the context before the next task

The next time you work on something, you start fresh. The session history is gone. But the grilling session before it left you with exactly what you needed.

## Compaction: `/compact`

| Approach                 | Tokens | Quality                     | Downsides                                                                                           |
| ------------------------ | ------ | --------------------------- | --------------------------------------------------------------------------------------------------- |
| Continue current session | 156k+  | Full context, lots of noise | High latency, dumb zone results                                                                     |
| Clear and start fresh    | ~5k    | Clean slate                 | Must re-explore everything, lossy understanding                                                     |
| Compaction               | ~28k   | Summarized context          | Lossy compression, [secondary source](https://www.aihero.dev/ai-coding-dictionary/secondary-source) |

```
/compact Yeah, we're going to do some QA in this area.
```

This instruction matters. The thing doing the summarisation is a language model, so it needs context to highlight relevant information. Your instruction doesn't need to be detailed - one sentence is often enough.

Here's a useful tip: you can queue messages inside the compaction UI. Once compaction finishes, your queued message runs automatically - no need to sit around waiting.

### The Trade-off: Information Loss

Compaction is the first hand-off mechanism you've seen that preserves context between sessions. But all hand-off mechanisms suffer from the same issue: whenever you create a secondary source, you lose information.
![[compaction.png|The compaction summary as a 'historian' looking over the session]]

| Approach                      | Information | Noise | Maneuverability |
| ----------------------------- | ----------- | ----- | --------------- |
| Primary source (continue)     | Full        | Lots  | Limited         |
| Secondary source (compaction) | Lossy       | Less  | More room       |
### When Compaction Shines – QA

However, in the exact situation where you want to do **QA on a finished piece of work**, compaction is a cast-iron great place to use it. You're not re-implementing. You're not making architectural decisions. You're validating something that's already complete.

## Handing Off: `/handoff`

Compaction, though, has some constraints. It can only compact within the same directory, and it can only compact within the same [agent](https://www.aihero.dev/ai-coding-dictionary/agent).

Like most of my skills, it's pretty short:
```
Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save to the temporary directory of the user's OS - not the current workspace.
```

One useful feature here is that it saves to the temporary directory of the user's OS. This means these handoff documents are designed to be ephemeral. They're not going to be saved locally in your project, and they won't be stored in any memory. They will be deleted when your computer resets, or whenever the OS decides to clear the temporary directory.=

```
/handoff pass to Codex to review
```

Just like with compact, we give the `/handoff` skill a reason for the handoff. This tells it the purpose of the next session.

The way I would seed this into a new session is to open it in a separate window. I've just run `/clear`, so I've got a totally empty session. Now I can use the `@` symbol to reference the file:

```
@/tmp/handoff-course-star-ratings-review.md
```

### /handoff vs. Compact

That's how the `/handoff` skill works. It's really nice for:

- Passing work to separate agents
- Saving a document you can send to a colleague
- Handing off to another agent in a different repo to fix a bug you encountered

It's just like compaction, except a little bit more flexible and a little bit more involved.

I wouldn't say that handoff is a total replacement for compaction. Here's when to use each:

|When|Use|
|---|---|
|Staying in the same directory|Compaction|
|Retaining context of the previous conversation|Compaction|
|Don't care about retaining previous conversation|Compaction (especially because you can queue up messages after it)|
|Passing to a different agent|`/handoff`|
|Handing off to another repo|`/handoff`|
|Sending to a colleague|`/handoff`|

Compaction is still really good. `/handoff` is nice too, but the linking to the next conversation is a little bit more involved, and it's only really useful if you're getting something out of it.

## Clear, Compact, Handoff, Or Subagent

### Phase Boundaries
![[phase-boundaries.png|Decision tree for phase boundaries showing the five options the choices we assigned to each phase boundary]]
### Your Five Options

| Option                                                               | What It Does                                                                                                    |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Continue**                                                         | Stay in the current session, no context switch needed                                                           |
| [**Clear**](https://www.aihero.dev/ai-coding-dictionary/clearing)    | Totally clear your [context window](https://www.aihero.dev/ai-coding-dictionary/context-window) and start fresh |
| **Compact**                                                          | Compress your context and seed a new session with it                                                            |
| [**Handoff**](https://www.aihero.dev/ai-coding-dictionary/handoff)   | Create a markdown file summarizing the session to pass anywhere                                                 |
| [**Subagent**](https://www.aihero.dev/ai-coding-dictionary/subagent) | Spawn a subagent to handle the task and report back                                                             |
![[phase-boundary-decision-tree.png|The decision tree diagram showing all five options]]
#### Question 1: Can You Continue?

**Does it make sense to continue in the current session?**

This is a fairly rich decision in itself. Between grilling and implementation, it obviously makes sense to continue because we've got that rich primary source that we need. We don't want to discard it for when we get to the implementation.

You may also want to continue if you just have enough smart zone budget left. If you're at 80k tokens maybe and you know the task is pretty small and is going to fit inside the smart zone, then yes, you can just continue.

![[phase-boundary-decision-tree-q1.png]]


#### Question 2: Is Your Context Irrelevant To The Next Task?

If you need to do something, ask yourself: **is all the information in this session totally disposable?**

In other words, all the explorations, the decisions that were made in that session - is it totally irrelevant to what comes next?

**If yes, clear your context window.** Clearing is the most efficient path if you can take it because it takes zero time. You're just deleting information. Then you have the most smart zone available to you. You're going back to a blank slate.

However, if you clear the context with relevant information inside, you're losing information that might have been useful later. Imagine if I cleared rather than compacted when I went to QA. This means that the QA would know absolutely nothing about the implementation, which maybe is okay - it could figure it out from the git commits. But it would also lose all the information from the grilling as well.

It would lose the reasoning behind the decisions that I had made. Both phases were important for the QA that then followed. So clearing just wasn't an option.

**If no, your context is relevant.** Move to the next question.
![[phase-boundary-decision-tree-q2.png|Decision tree showing the second question: Is your context irrelevant?]]
#### Question 3: Do You Need To Hand Off?

This is specifically about the handoff [skill](https://www.aihero.dev/ai-coding-dictionary/skill). The handoff skill is relatively narrow compared to the other options.

You'll only need to do the handoff when you need to:

- Pass work to another agent
- Pass work to another directory or another colleague
- Fork off a side task you discovered mid-phase without derailing the current session

For instance, you might find something during grilling that also needs to be tackled. You can just hand off to another session while you're doing that.

**If yes, use handoff** (`/handoff`). **If no, move to the next question.**
![[phase-boundary-decision-tree-q3.png|Decision tree showing the third question: Do you need to hand off?]]
#### Question 4: Can The Task Be Done AFK?

**[AFK](https://www.aihero.dev/ai-coding-dictionary/afk) means away from keyboard.** You're not touching the keyboard. You're just watching the agent go and you cannot intervene.

This means the task is well-scoped. The agent can do it without needing your intervention at all.

Let's imagine we wanted to do an [automated review](https://www.aihero.dev/ai-coding-dictionary/automated-review) on the implementation before [human review](https://www.aihero.dev/ai-coding-dictionary/human-review) got there. Automated review is where you send the agent into the codebase and you get it to look at the changes and check if it's broken anything or done anything weird.
![[afk-example.png|Diagram showing automated review as an example of AFK task]]We could have compacted at this point (we're at 150k tokens from the implementation), then run the review in the main session. But since the human isn't needed for automated review, we might as well run it in a subagent. That means we just get it to run in its own context window. We don't affect the main session.

**If yes, spawn a subagent.** **If no, move to the final option.**

![[phase-boundary-decision-tree-q4.png|Decision tree showing the fourth question: Can the task be done AFK?]]
#### The Default: Compact

This is the bottom of the decision tree. When your context is relevant, when you want to do something with the context, and you can't continue, when you don't need to use a handoff, and when the task needs to be done with you there - then compact is the solution.

Compact compresses your context window and seeds a new session with the good stuff. You keep what matters and discard what doesn't.

### Auto-Compaction

![[auto-compaction.png|Compacting in the middle of a phase Is dangerous]]
