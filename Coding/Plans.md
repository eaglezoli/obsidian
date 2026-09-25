

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

