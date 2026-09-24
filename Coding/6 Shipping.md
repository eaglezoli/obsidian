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
![[tracer-bullets.png|Building out sideways from the tracer bullet (vertical slice – or horizontal in this diagram)]]
To get beautifully vertically sliced tickets, you use the `/to-tickets` [skill](https://www.aihero.dev/ai-coding-dictionary/skill).

**When to Call /to-tickets**



![[spec-tickets.png|The spec is the destination; each ticket is one leg of the journey]]