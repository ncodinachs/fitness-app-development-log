# Development Log

This document tracks the evolution of the fitness app from concept to product.
It focuses on architectural decisions, product thinking and lessons learned,
without exposing source code.

---

## Week 1 – Project foundation & MVP scope

### Goal
Define a solid foundation for a commercial fitness app while keeping the scope
small enough to reach a functional MVP.

---

### Key decisions

#### 1. Private source from day one
From the beginning, the project was conceived as a commercial product.
For that reason, the source code is private and development is documented
at a conceptual and architectural level only.

This allows sharing real-world experience without compromising
intellectual property.

---

#### 2. MVP-first mindset
Instead of building everything at once, the app was split into clear functional areas:
- Profile
- Workout
- Diet
- Review (progress tracking)

Each area is treated as an independent module.

---

#### 3. Separating static data from progress data
One of the earliest architectural decisions was to separate:
- **Profile** → static user data
- **Review** → time-based data (weight, photos, charts)

This separation simplifies state management and improves long-term scalability.

---

#### 4. Tab-based modular architecture
The app uses a tab-based structure where each tab owns:
- Its own UI
- Its own data flow
- Its own responsibilities

This reduces coupling and makes future refactors easier.

---

### Challenges encountered
- Early state inconsistencies when navigating between tabs
- Deciding what belongs to UI state vs domain state
- Avoiding premature backend integration

---

### Lessons learned
- A clean structure early saves a lot of refactoring later
- MVP does not mean “quick and dirty”
- Protecting product ownership does not prevent knowledge sharing

---

### Current status
- MVP structure defined
- Core tabs implemented
- Architecture ready for future persistence and backend integration

---

### Next steps
- Refine UX inside each tab
- Implement progress visualization
- Prepare a public DEMO with mock data

---

## Week 2 – Workout & session flow (product + architecture)

### Goal
Design a workout experience that works in real gym conditions:
fast to use, minimal taps, and reliable tracking during a session.

---

### What was built / defined (conceptually)
- A clear separation between:
  - **Workout Plan creation** (building templates)
  - **Workout Session** (executing a workout in real time)
- A workflow where the user can:
  1) Choose a plan  
  2) Start a session  
  3) Log sets (weight / reps)  
  4) Finish session  
  5) Save results into history

---

### Key decisions

#### 1. "Plan" ≠ "Session"
A plan is a reusable template.  
A session is a time-based execution instance.

This prevents common issues like:
- Overwriting the plan with session data
- Mixing historical records with templates
- Complexity when editing a plan after past sessions exist

---

#### 2. Minimal friction UX for the gym
During a workout, users do not want forms.
The session flow was designed to prioritize:
- One-screen visibility (current exercise + sets)
- Quick edits
- Clear “finish session” moment

---

#### 3. Data model boundaries
To keep the system scalable, the structure was conceptualized as:
- **WorkoutPlan** → exercises + default structure
- **WorkoutSession** → date/time + performed sets
- **SetEntry** → weight/reps (and optional notes)

This makes workout history consistent and analytics-friendly.

---

#### 4. History as a first-class feature
Workout history is not just a “log”.
It becomes the basis for:
- Progress tracking (strength over time)
- Better UX (prefill last used weights)
- Future insights (volume, PRs, trends)

So history was treated as a core module, not an afterthought.

---

### Challenges encountered
- Avoiding state loss when navigating between tabs
- Deciding where session state should live during execution
- Keeping plan editing safe without breaking historical sessions

---

### Lessons learned
- Templates vs instances is a critical distinction for fitness products
- History data becomes extremely valuable once it is consistent
- Gym UX must optimize for speed and clarity, not “feature density”

---

### Current status
- Workout plan vs session concept finalized
- Session flow clarified for real-world usage
- History considered as the foundation for future progress features

---

### Next steps
- Improve diet flow (search → select → quantity → save)
- Review tab: connect progress metrics to workout/diet outcomes
- Prepare the DEMO experience (mock data + polished navigation)

---

## Week 3 – State persistence & cross-tab consistency

### Goal
Ensure that user data remains consistent and available when navigating
between tabs, avoiding data loss and unexpected resets during normal usage.

This week focused less on new features and more on **stability and correctness**.

---

### Context
The app uses a tab-based navigation system.
Early on, switching tabs caused temporary state to reset in certain scenarios,
especially for:
- Diet entries
- Workout session progress
- Form-based inputs

These issues often remain hidden in early prototypes but become critical
once the app is used continuously.

---

### Key decisions

#### 1. Identify what *must* persist
Not all state is equal. A clear distinction was made between:
- **Ephemeral UI state** (scroll position, temporary selections)
- **User-critical state** (entered food, session progress, profile changes)

Only user-critical state was prioritized for persistence.

---

#### 2. Persistence before polish
Instead of refining UX immediately, effort was shifted to:
- Making sure data survives tab navigation
- Avoiding silent data loss
- Ensuring predictable behavior

Polish can be added later; lost data destroys trust.

---

#### 3. Explicit ownership of state
Each functional area became responsible for:
- Creating its own state
- Updating it intentionally
- Persisting it when needed

Implicit or shared state between tabs was avoided.

---

#### 4. Delayed backend integration
Although backend integration was considered, it was intentionally postponed.
The goal was to:
- Validate flows locally
- Keep iteration fast
- Avoid coupling UX decisions to API constraints too early

---

### Challenges encountered
- Understanding when Flutter rebuilds widgets
- Avoiding accidental state recreation
- Deciding persistence boundaries without overengineering

---

### Lessons learned
- State bugs are product bugs, not just technical ones
- Users forgive missing features, not missing data
- Solving persistence early simplifies everything that follows

---

### Current status
- Cross-tab data consistency stabilized
- Diet and workout inputs no longer reset unexpectedly
- App behavior is predictable during long sessions

---

### Next steps
- Refine Diet UX (speed and clarity)
- Connect Review metrics with persisted data
- Start defining DEMO scenarios and user journeys
