> You cannot reliably know everything that is missing before you actually interact with the product. More ceremony can predict more problems, but after a point you'**re asking AI to reason about an imaginary product rather than learning from a real one**.

Too little ceremony creates avoidable mistakes. Useful ceremony catches expensive mistakes early. **Too much ceremony creates increasingly detailed speculation about something nobody has used yet.**

Owning the process does not mean personally possessing all the engineering expertise. It means owning how that expertise gets applied and verified.

You own the pipeline, not necessarily the technical labour.

Small implementation units reduce the amount of code you need to understand at once and make it much easier to identify where a bad decision entered the system.

The question is not whether the framework has more ceremony. The question is whether each stage contributes information, catches risk or improves a decision.





```
IDEA
↓
???
↓
PROTOTYPE
↓
???
↓
FIRST PRODUCTION SLICE
↓
???
↓
AFK EXECUTION
↓
???
↓
REVIEW
```


Your workflow

```
                 GREENFIELD

Idea
 ↓
Discovery / challenge assumptions
 ↓
Prototype uncertain UX
 ↓
Product definition
 ↓
Architecture + standards
 ↓
Choose first vertical slice


              EACH REAL SLICE

Grill / clarify
 ↓
Spec
 ↓
Technical plan
 ↓
Tasks
 ↓
Implement in bounded contexts
 ↓
Tests
 ↓
Standards review
 ↓
Spec review
 ↓
Correctness review
 ↓
QA
 ↓
Feature-wide completeness check
```

> **Who currently does each box best?**


The process I’d actually use

```
RAW APP IDEA
    ↓
1. DISCOVERY / IDEA ASSESSMENT
   What problem? Who for? What assumptions?
    ↓
2. PRODUCT ROADMAP
   Break the whole app into meaningful vertical slices
   Decide what should be proved first
    ↓
3. QUICK THROWAWAY PROTOTYPE
   Matt-style /prototype
   Fake data, fast UX exploration
    ↓
4. AGREE THE FIRST PRODUCTION SLICE
    ↓
────────────────────────────────
       SPEC KIT FULL CYCLE
────────────────────────────────
5. Constitution
   Project-wide principles / quality expectations
    ↓
6. Specify
   What should this slice do?
    ↓
7. Clarify
   Remove ambiguity
    ↓
8. Plan
   Technical architecture and approach
    ↓
9. Tasks
   Break implementation down
    ↓
10. Analyse
    Check spec ↔ plan ↔ tasks consistency
    ↓
11. Implement
    Build it
    ↓
12. Converge
    Find missing / partial / contradictory work
    ↓
────────────────────────────────
          QUALITY GATES
────────────────────────────────
13. Independent code review
    • engineering standards
    • spec compliance
    • correctness / bugs
    ↓
14. YOUR QA
    Does it actually behave and feel right?
    ↓
15. Commit / ship
    ↓
Next vertical slice
```


Mobile App Process

```
1. PRODUCT DISCOVERY
   BMAD
   ├─ brainstorm
   ├─ research
   ├─ challenge assumptions
   ├─ product definition
   └─ UX journeys

          ↓

2. PRODUCT PROTOTYPE
   quick/disposable
   ├─ fake data
   ├─ actual screens
   └─ you physically use it

          ↓

3. PRODUCTION DEFINITION
   BMAD
   ├─ PRD
   ├─ architecture
   ├─ first vertical slice
   └─ acceptance criteria

          ↓

4. ENGINEERING
   Superpowers OR BMAD build initially
   ├─ small bounded tasks
   ├─ TDD where appropriate
   ├─ tests/typecheck/lint
   ├─ spec review
   ├─ code-quality review
   └─ correctness review

          ↓

5. MOBILE-SPECIFIC REVIEW
   React Native / Expo rules
   ├─ architecture
   ├─ accessibility
   ├─ performance
   ├─ permissions/privacy
   └─ platform behaviour

          ↓

6. VISUAL FEEDBACK LOOP
   YOU + screenshots/device
   ├─ iPhone
   ├─ Android
   └─ web if supporting it

          ↓

7. FEATURE QA / REGRESSION
```


The balance I'd use

```
1. BROAD DISCOVERY
   BMAD-style
   ↓
   users, problem, competitors,
   possible product directions,
   core journeys, assumptions

2. QUICK PROTOTYPE
   ↓
   fake data, rough UI,
   enough screens to FEEL the product

3. USE IT
   ↓
   "Oh, actually map-first is annoying"
   "I need collections here"
   "Events and places should behave differently"
   "This screen needs context I hadn't considered"

4. SECOND DISCOVERY / UX PASS
   ↓
   now BMAD/AI has REAL evidence
   rather than hypothetical assumptions

5. DEFINE MVP + ARCHITECTURE
   ↓
   PRD, UX rules, technical decisions,
   first production slice

6. BUILD FIRST REAL SLICE
   ↓
   use it again

7. ITERATE
```


Prototyping

```
BMAD
Brainstorm / Forge / Research
        ↓
Product Brief / PRD
        ↓
BMAD UX
        ↓
━━━━━━━━━━━━━━━━━━━━━━━━
 EARLY PROTOTYPE CHECKPOINT
━━━━━━━━━━━━━━━━━━━━━━━━
        ↓
Stitch / Figma prototype
and/or
Matt /prototype for interactions
that need actual code
        ↓
YOU USE IT
        ↓
"Actually, this should work differently..."
        ↓
BMAD Update PRD / UX
        ↓
Architecture
        ↓
First real vertical slice
```


BMAD + Superpowers + Mobile App specialists workflow

```
BMAD
Discovery → PRD → UX → Architecture → Stories
                ↓
        authoritative repo docs
                ↓
        Superpowers feature cycle
                ↓
     Expo / RN specialist skills
                ↓
      fresh implementation agents
                ↓
           reviews + tests
                ↓
             your QA

claude-mem runs alongside this,
remembering useful session history
```


```
              PRODUCT
────────────────────────────────
BMAD
research / product / UX / architecture

              ↓

       DURABLE PROJECT TRUTH
────────────────────────────────
AGENTS.md / CLAUDE.md      ← short
docs/
  ARCHITECTURE.md
  ENGINEERING_STANDARDS.md
  TESTING.md
  SECURITY.md
  UX / decisions / ADRs

              ↓

            ENGINEERING
────────────────────────────────
Superpowers
plan → small task → TDD → review → verify

              +

Official Expo skills
React Native specialist skills

              ↓

          QUALITY LAYERS
────────────────────────────────
Spec review
Code-quality review
Correctness review
Conditional:
  mobile / security / accessibility /
  architecture / performance

              ↓

              YOU
────────────────────────────────
actual-device visual + behavioural QA


RUNNING ALONGSIDE ALL OF IT:
claude-mem
session history / debugging recall
```

Then **later**, if the repo starts accumulating AI cruft:

```
Desloppify / codebase health pass
```

And even later, if you want many tasks worked through AFK:

```
GSD / stronger orchestration
```

