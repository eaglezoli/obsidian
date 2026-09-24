## How to Tackle Massive Tasks
![[smart-dumb-zone-tasks.png|Small tasks like small features or bug fixes can fit in the smart zone, but not larger tasks like a refactor that touches every layer of the application]]
![[spec-tickets.png|The spec is the destination; each ticket is one leg of the journey]]
## Set Up Your Issue Tracker
```Terminal
npx skills@latest add mattpocock/skills --skill=setup-matt-pocock-skills
```
- Search for "setup skills skill"
	- This will add the `/setup-matt-pocock-skills` [skill](https://www.aihero.dev/ai-coding-dictionary/skill) to the repo.
- Run`/setup-matt-pocock-skills`in Claude Code
	- The skill will do a brief exploration of the repo's current state and provide a recommendation on the issue tracker to use.

## Write Great Specs With `/to-spec`

**The Process**
1. Initial grilling session
2. Turn that grilling session into a spec
3. Turn that spec into [tickets](https://www.aihero.dev/ai-coding-dictionary/ticket)
4. Implement each individual ticket
5. Review against the spec that we initially created
![[5-step-system.png|Five-step system: grilling session → spec → tickets → implement → review]]
**The Spec Template**

The spec that's created uses a template that's nice and meaty. It includes:

- A problem statement
- A solution description
- A bunch of user stories (a classic software development technique)
- Implementation decisions
- Testing decisions
- Out of scope items
- Further notes

An analytics page is so big, so potentially scope creepy and could expand larger and larger that I think it makes a very good candidate for a grilling session followed by a spec. We need to shape this into something reasonable and it's definitely going to be larger than one [Smart Zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone).

I rarely actually go and read these specs myself. If I were to read the spec, what would I actually be testing for? I'd just be testing the agent's ability to summarize what we just talked about. And that's something that I kind of take on trust.

# Split Features Across Context Windows With `/to-tickets`

**Horizontal Slices Are a Trap**

![[application-layers.png|Application layers: database, API, front-end, services, and components]]
Every application has layers. But you shouldn't develop in layers, which is what the AI likes to do.

![[horizontal-phases.png|How an agent thinks to break up tasks: horizontal slices with separate phases for each layer]]
This looks well-organized and reasonable, but it's a trap. Software developers have known about this for decades.

If you do it this way, all of the code in phase 1, you don't really know if it works or if it's well designed until you're implementing phase 3. You need to cross the layers to work out if the code for that layer is well designed.

With horizontal slices, you get feedback on the whole system far too late.

**Vertical Slices Give Early Feedback**

The way to fix this is vertical slices. The agent works across layers from the very first phase.

From the word go, they're touching the database, the API, and the front-end. They're building out a minimal implementation first, then building from there.
![[vertical-slices.png|Vertical slices cutting across all layers from the first phase]]
This means they're getting feedback on their design, its feasibility, and seeing how all the layers integrate from the first phase.

Every phase that builds on that is pretty trivial because it's just building on work that it already knows is well integrated.

Using the phrase "vertical slices" is actually really good because the agent already understands vaguely what it means. The concept of vertical slices and tracer bullets has been around for a long time - it goes back to [_The Pragmatic Programmer_](https://www.amazon.co.uk/Pragmatic-Programmer-Andrew-Hunt/dp/020161622X).
![[tracer-bullets.png|Building out sideways from the tracer bullet (vertical slice – or horizontal in this diagram, also not sure why it's starting with UI)]]
To get beautifully vertically sliced tickets, you use the `/to-tickets` [skill](https://www.aihero.dev/ai-coding-dictionary/skill).

**When to Call /to-tickets**
![[phase-end_decision-tree.png|Decision tree diagram for when to continue, compact, or start fresh at the end of a phase]]
When you reach the end of a phase, you need to decide what to do next. After `/to-spec`, that's definitely the end of a piece of work.

Walk through this decision tree:

**Can you continue?** Do you have enough smart zone left?

If yes, and your [context](https://www.aihero.dev/ai-coding-dictionary/context) is relevant to the next piece of work, you can keep going in the same session.

**Is your context irrelevant?** If the information in your context isn't relevant to the next task, [start fresh](https://www.aihero.dev/ai-coding-dictionary/clearing).

In this case, the context is extremely relevant. All the decisions that went into the spec are in the context. It makes sense to keep this around.

**Do we need to [hand off](https://www.aihero.dev/ai-coding-dictionary/handoff)?** Not if we're staying within the same agent and directory.

**Can this be done [AFK](https://www.aihero.dev/ai-coding-dictionary/afk)?** Not if you need [human review](https://www.aihero.dev/ai-coding-dictionary/human-review).

This situation is a great candidate for [compacting](https://www.aihero.dev/ai-coding-dictionary/compaction) if you're outside the smart zone. However, if you don't need to, you can just continue.

**Review the Ticket Breakdown**

Each ticket should cut across all layers - database, API, front-end - not focus on just one layer.

Look for tickets that say things like "implement the database schema" or "build the API endpoints" as separate phases. That's horizontal slicing.

Good vertical slices deliver end-to-end behavior in each ticket - a narrow but complete path through every layer.

Remember, you've only got one smart zone per session to play with. Each ticket should be sized to fit in a single fresh [context window](https://www.aihero.dev/ai-coding-dictionary/context-window).

If a ticket looks like it's trying to do too much, ask the agent to split it further.

The agent will iterate with you until you approve the breakdown. Don't move forward until the tickets are properly vertically sliced and appropriately sized.

### Example

**The first proposal: 10 tickets**

It comes back pretty fast and gives us 10 tickets.

10 tickets feels way too much for this. If you think of the [smart zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone) as 150,000 [tokens](https://www.aihero.dev/ai-coding-dictionary/token), then this would mean we are budgeting 1.5 million tokens for this feature.

That feels like way too much to me. I'm picturing that maximum we would need 450k. So let's say three tickets.

The way I'm able to make that judgment call is just a gut feeling really, just having done a lot of this, a lot of looking at these proposed ticket breakdowns and seeing what comes out.

450k even feels generous. I think this could probably even be done in two [sessions](https://www.aihero.dev/ai-coding-dictionary/session), but I don't want to push it.

**Horizontal slicing is still a problem**
![[claudes-initial-horizontal-tickets.png|Claude's initial 10-ticket breakdown showing horizontal slicing]]
What we can see here too is doing classic horizontal slicing as well, which is frustrating because I'm really trying inside the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) to not get it to do this, but it still just persistently does it.

**This is why I feel a human looking at this is so important, by the way.**

I think 10 is not a good candidate, I'm just going to say:

```
I would like to break this down into maximum three tickets. 
I think ten feels way too much.
```

Let's give this a go.

**Three tickets, but Claude pushes back**


Okay, it's now given me three pretty large pieces of work here and it's actually saying:

> One trade I want to be explicit about: tickets two and three are larger than a single fresh [context window](https://www.aihero.dev/ai-coding-dictionary/context-window).

![[claudes-ticket-warning.png|Claude's warning about tickets exceeding context window size]]
So it's saying that it's pretty scared about this overview tab. Okay. Maybe we'll pull it to like five or something.

What I can see though is that these three are pretty good vertical slices. There is some groundwork that's being done here. There's some stuff that's kind of being included in this PR that probably could be elsewhere. So there's indexes, the seed rewrite, and the dead parameter prefactor.

Prefactor by the way if you've never heard of this - this is just a refactor before you do some work.

This will burn a lot of tokens because we're just like plowing in a bunch of seed data, and so just like lots of [output tokens](https://www.aihero.dev/ai-coding-dictionary/output-tokens) will be produced during this. And so I guess it makes sense to have it before we do any of the other vertical slices.

But the other ones, because they're now grouping a ton of work together, they are by definition vertical because they're like building out throughout an entire feature.

So let's see if it retains the vertical slices when we go to five:

```
Could we have five tickets instead of three?
```

## Five tickets: the sweet spot

Okay, so the groundwork is looking the same here and then it starts then with a page shell. That's a good classic vertical slice. I really like that.

It then goes on and adds some extra overview panels, then the course detail selector, progress and drop-off funnel and course detail extras. Okay.

It's even explicitly saying here:

> Every ticket lands as something you can look at

Think of the tracer bullets landing at the final destination (the UI).
![[tickets-landing.png|Claude's message stating every ticket lands as something you can look at]]
**Blocking relationships and parallel work**

It also, by the way, does this clever thing where it has blocking relationships here.

So technically we can do these in parallel if we wanted to. For instance, in the overview panels, like two, we've got the page shell, and then three is blocked by two and four is blocked by two.

So this means we could work on one and two and then split up to do three and four in separate context windows if we wanted to.

That's entirely optional, you don't have to do that, but it is a little bit quicker if you can make that work. And this means that we can scale this [skill](https://www.aihero.dev/ai-coding-dictionary/skill) up to actually fanning out, producing multiple pieces of work and merging them back together.

**The published tickets**
![[published-issue-ticket.png|GitHub issues page showing the parent issue #4 with five sub-issues]]
So we've got our spec and we have the first one that's unblocked, which is the groundwork.

We get an explicit link to the parent, and then we get what to build and the acceptance criteria.

Notice this ticket is pretty light here because we have the parent spec to rely on. All we're doing is really specifying which bit of the spec we're building now.

![[ticket-parent-link_acceptance-criteria.png|Ticket #5 showing parent link and acceptance criteria]]
And having this explicit acceptance criteria is really nice for giving it a point where it can stop.

**Review the tickets lightly**

What I recommend you do is read through some of these. Again, I don't recommend actually reviewing each of these because they're just summaries of the things that we've decided already.

These tickets are relatively light, they're just splitting up the spec so that we can go and work on it.

## Executing Your Tickets

There are three [skills](https://www.aihero.dev/ai-coding-dictionary/skill) that handle this: `/implement`, `/tdd`, and `/code-review`. They work together to build features, write tests first, and review the work before committing.

### **The `/implement` Skill**

The `/implement` skill is the orchestrator. It delegates most of its work to the other two skills.

Here's what it does:

- Implement the work described in the spec or tickets
- Use `/tdd` where possible, at pre-agreed seams
- Run [typechecking](https://www.aihero.dev/ai-coding-dictionary/automated-check) regularly, single test files regularly, full test suite once at the end
- Once done, use `/code-review` to review the work
- Commit your work to the current branch

It's very simple. The real work happens in `/tdd` and `/code-review`.


### **The `/tdd` Skill**

The `/tdd` skill is where the quality comes from. [Agents](https://www.aihero.dev/ai-coding-dictionary/agent) do their best work when they have the most feedback, and TDD is a great technique for that.

You write the unit test for the feature first, then implement it. The test gives the agent immediate feedback on whether the implementation is correct.

The skill includes:

- What a good test is - tests verify behaviour through public interfaces, not implementation details
- Advice on mocking and tests
- What seams are - the public boundary you test at
- What bad tests are - implementation-coupled, tautological, or horizontal slicing
- Rules of the loop - red before green, one slice at a time, refactoring belongs in review

**Test Only at Pre-Agreed Seams**

A **seam** is the public boundary you test at. Tests live at seams, never against internals.

Before writing any test, you write down the seams under test and confirm them with the user. No test is written at an unconfirmed seam.

This keeps testing effort on the critical paths and complex logic instead of every edge case.

**Tautological Tests**

One anti-pattern (“don't do it this way” pattern) worth calling out: **tautological tests**. These are tests where the assertion recomputes the expected value the way the code does.

For example: `expect(add(a, b)).toBe(a + b)`. The test passes by construction and can never disagree with the code.

Expected values must come from an independent source of truth - a known-good literal, a worked example, the spec.

### The `/code-review` Skill

The `/code-review` skill does a two-axis review of the diff between `HEAD` and a fixed point you supply.

It runs two [reviews](https://www.aihero.dev/ai-coding-dictionary/automated-review) in parallel [sub-agents](https://www.aihero.dev/ai-coding-dictionary/subagent):

- **Standards** - does the code conform to this repo's documented coding standards?
- **Spec** - does the code faithfully implement the originating issue / PRD / spec?

**Why Two Axes**

A change can pass one axis and fail the other:

- Code that follows every standard but implements the wrong thing - **Standards pass, Spec fail**
- Code that does exactly what the issue asked but breaks the project's conventions - **Spec pass, Standards fail**

Reporting them separately stops one axis from masking the other.

**The Standards Sub-Agent**

The Standards sub-agent gets:

- The full diff command and commit list
- The list of standards-source files found in the repo
- A smell baseline from _Refactoring_ - Mysterious Name, Duplicated Code, Feature Envy, Data Clumps, and others

It reports every place the diff violates a documented standard, and any baseline smell it spots. Documented-standard breaches can be hard violations, but baseline smells are always judgement calls.

### The Spec Sub-Agent

The Spec sub-agent gets:

- The diff command and commit list
- The path or fetched contents of the spec

It reports:

- Requirements the spec asked for that are missing or partial
- Behavior in the diff that wasn't asked for (scope creep)
- Requirements that look implemented but where the implementation looks wrong

This second pass massively increases the quality of the output. It often goes and fixes the really bad stuff itself.

![[spec-tickets.png|The spec is the destination; each ticket is one leg of the journey]]