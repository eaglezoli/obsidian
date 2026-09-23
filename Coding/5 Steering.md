## The Steering Map

### Understanding Context Load

**Anything that you load into the agent up front, you pay for on every single [model provider request](https://www.aihero.dev/ai-coding-dictionary/model-provider-request).**
![[session-turns.png|Diagram showing a session with three turns, each turn containing multiple model provider requests represented as light blue dots]]

Each model provider request carries all of the history and everything new along with it. **Any little instruction that you add early in the [context window](https://www.aihero.dev/ai-coding-dictionary/context-window) is going to be passed in on every single request.**
![[instructions-context.png|Context load diagram showing five numbered requests, each row containing blocks representing the growing payload with a violet block at the front being re-sent every time]]

**You're paying [tokens](https://www.aihero.dev/ai-coding-dictionary/token) to include these steering instructions on every request.** But there's a second cost: **you're also paying in [attention](https://www.aihero.dev/ai-coding-dictionary/attention-budget).**

Every extra instruction that you load makes every other instruction a little bit quieter and pushes the agent a little bit closer to the [dumb zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone).
![[attention.png|Attention diagram showing five empty boxes with arrows scattered across them, clustered densely at the left and thinning out toward the right]]
That combined cost, paying more tokens and spreading your agent's attention thinner, is what we'll call **context load**. And every time you have a steering instruction, you need to think about the context load that steering instruction is providing.

**So when we talk about steering, we're not just thinking about writing good rules for our agent. It's about figuring out which rules, which patterns we encode in the context window, because we pay a cost in context load for everything we add.**

### Push vs Point: Two Strategies for Steering

| Strategy | Cost                  | Availability     |
| -------- | --------------------- | ---------------- |
| Push     | High on every request | Always present   |
| Point    | Minimal most turns    | Only when needed |
![[steering-push-point.png|Side-by-side comparison of Push and Point strategies, showing the context window with a large block inside for Push versus a tiny pointer square for Point]]
#### Push: Always-On Steering

Imagine the agent's context window looks like a box, and our instruction is a yellow blob sitting inside it. When we push the instruction to the agent, it means that steering instruction is always on. It sits in the context window for every single session. The agent cannot miss it because it's already in its context window.

That means it's costing us context load whether this turn needs it or not.

#### Point: On-Demand Steering

When you point, you put the steering instructions somewhere in the [environment](https://www.aihero.dev/ai-coding-dictionary/environment). You put one little line in the context window just to point to it. This line could read: "when you're doing a certain kind of work, then use these instructions." That line is a [**context pointer**](https://www.aihero.dev/ai-coding-dictionary/context-pointer).

It's a pointer that sits in the context window so that when the agent needs it, it goes and follows the pointer, pulls in the full instruction.

Most turns a context pointer will cost you almost nothing.

### Where Pushed Steering Lives: AGENTS.md

So how do you push to an agent context window? One technique is the [AGENTS.md](https://www.aihero.dev/ai-coding-dictionary/agents-md) file. This is a file often at the root of your project that the [harness](https://www.aihero.dev/ai-coding-dictionary/harness) loads into the context window at the session start.

`AGENTS.md` is a cross-harness convention, so whatever tool that you're using probably will understand it. The big exception here is Claude Code, which calls it `CLAUDE.md` for reasons beyond understanding. Throughout this course we'll call it `AGENTS.md`.

#### The Epidemic of Over-Pushing

This advice will run counter to what a lot of people are doing right now. They are pushing tons of instructions into `CLAUDE.md` or `AGENTS.md`, and I think they're seeing worse results because of it.

There is an epidemic of pushing right now and so much so many tokens are being wasted. So much context load is being placed on these agents when I think instead you need to be considering techniques for pointing.

**In this course, in practice: you point by default.** And you let the agent decide whether to pull in those instructions or not.

## Steering With A Pointer

### The Doc-Plus-Pointer Pattern

You don't need the steps on every request. You need them **reachable** from every request. Those are different things.

Take the steps out of `AGENTS.md` and give them their own document. Leave one short line in `AGENTS.md`: _when you're changing the database schema, read this doc first_. The context load becomes a single sentence. The steps load only when the agent follows the pointer and needs them.

That's the **doc-plus-pointer** pattern. A [context pointer](https://www.aihero.dev/ai-coding-dictionary/context-pointer) is a reference in the agent's context that names some material and encodes the condition for reaching it. It needs two things to work:

- **A stable path** - the agent needs to know where to find it.
- **Clear description** - the agent needs to know when following it is worth it. A bare path is a pointer the agent has no reason to use. Word it the way the task actually presents.

### The /writing-for-agents Skill

Writing a good document for an agent is its own skill. You're going to use the `/writing-for-agents` skill to do it. This [skill](https://www.aihero.dev/ai-coding-dictionary/skill) takes the steps in your head and turns them into a document an agent can follow: clear, ordered, no waffle. It's built exactly for writing `AGENTS.md` and for writing the kind of focused docs that sit behind pointers.

The pointer should describe when and why the agent should reach for the document. Something like: "When making a database schema change, consult `docs/database-migrations.md` for the exact steps."

### Understanding Pointers

A [pointer](https://www.aihero.dev/ai-coding-dictionary/context-pointer) is basically made up of two parts:

1. The link - the actual thing that's pointing to it
2. The text around the pointer - what tells the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) when to use it

Example:

```
Database migrations – docs/database-migrations.md. Read before editing app/db/schema.ts, when a schema change needs scripts/seed.ts updated, or when npm run db:seed fails to start.
```

I'm not exactly happy with this pointer description. It's certainly quite concrete, like, "read before editing this specific file, read whenever a schema change needs this thing updated, or when this particular command fails to start." That's very concrete and very specific, but I think I want to make it a bit broader.

So I'm going to say:

```
Update the description of the pointer in AGENTS.md to be a bit broader to say: whenever we make a database change, follow these steps.
```

That way the agent has a really clear rationale and understands exactly when it needs to. Of course it will use its own judgment too - it might look at the name of the file, for instance, and just say "okay, database migrations, I'll do it whenever database migration is needed." But this reads a little bit better to me, and it's also a little bit shorter, which always helps.

### The Key Takeaway

So whenever you're thinking about adding or doing some steering in the global scope, I recommend pointing over pushing.

And this pattern of having local docs inside the repo, hidden behind a pointer, is very, very effective.

However, it does have some weaknesses.

## Agent Skills
![[skills-structure.png|Diagram showing layered structure from context window to SKILL.md to reference files]]


|Invocation Type|How It Works|Context Load|Cognitive Load|
|---|---|---|---|
|**Model-invoked**|Description is in the context window. The agent can see it, notice it's relevant, and pull it in on its own.|Higher|Lower|
|**User-invoked**|Description is hidden from the agent. Only you can invoke it by typing its name.|Zero|Higher (you must remember it)|

**The portable pointer** – skills are just the same as our doc and pointer approach, except they're just more portable.

**Where Skills Live**

| Level   | Location            | Scope                 | Sharing                         |
| ------- | ------------------- | --------------------- | ------------------------------- |
| User    | `~/.agents/skills/` | Personal to you       | Global across all your projects |
| Project | `.agents/skills/`   | Scoped to one project | Shared with everyone who clones |

**Two Flavours**

![[two-skill-flavours.png|Whiteboard diagram showing user-level vs project-level skill characteristics]]

| User-Level | Project-Level  |
| ---------- | -------------- |
| Personal   | Checked-in     |
| Global     | Single-project |
|            | Communal       |

**Personal:** It's yours alone, nobody else sees it, and nobody else has to use it.

**Global:** It follows you everywhere. Install it once in your user directory, and it's available in every project you open on your machine with no setup and no copying.

**Checked-in:** The skill is part of your repository. It's tracked in git history and travels with the project.

**Single-project:** It won't follow you to your next project, but it's scoped to this one for good reason.

**Communal:** Everyone who edits the project can also contribute to the skill. The skill automatically grows with the project, and everyone on the team gets to build it up over time.

## Navigation Pointers

A **navigation pointer** is a short line in `AGENTS.md` that sends the agent straight to an important part of the codebase with no scanning in between. It's a [context pointer](https://www.aihero.dev/ai-coding-dictionary/context-pointer) with a specific job: instead of telling the agent what to do, it tells the agent where to look.

You don't build highways to everywhere. That would push your entire file tree into [context](https://www.aihero.dev/ai-coding-dictionary/context), imposing serious context load. You build highways to the places the agent needs often, and let it take local roads for the final stretch once it's arrived.

The rule is simple: **whenever you change your project structure, check your navigation pointers**. A stale highway is worse than no highway, because the agent believes it.


| Scope         | Mechanism          | Location     |
| ------------- | ------------------ | ------------ |
| Every session | Navigation pointer | `AGENTS.md`  |
| One turn      | @-mention          | Chat message |

Use navigation pointers for files that are:
- Hard to discover by scanning
- Critical to change when solving a problem
- Part of non-obvious workflows

## Pruning

