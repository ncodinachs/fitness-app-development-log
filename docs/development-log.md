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
