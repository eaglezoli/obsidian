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


![[application-layers.png|Application layers: database, API, front-end, services, and components]]

![[horizontal-phases.png|How an agent thinks to break up tasks: horizontal slices with separate phases for each layer]]

![[image-2.png]]

![[spec-tickets.png|The spec is the destination; each ticket is one leg of the journey]]