# Module 02: EvaluationEngine - Implementation Plan

## Purpose
Evaluates the player's 10-year performance and determines the outcome.

## Public Interface (Lean)
### Reactive Store
- (None - Pure Logic Module)

### Actions
- `evaluate(starvedAvg: number, acresPerPerson: number): GameRating` — Calculates the final rating based on performance metrics.
- `getRatingDescription(rating: GameRating): string` — Returns a human-readable description of the rating.

## Implementation Phases

### Phase 1: Domain Types
**Goal:** Define the rating and stats types.
**Affected Files:**
- `src/logic/EvaluationTypes.ts` (Create)
**TODOs:**
- [ ] TODO 1: Define `GameRating` enum (`FANTASTIC`, `GOOD`, `POOR`, `TERRIBLE`, `IMPEACHED`).
- [ ] TODO 2: Define `EvaluationStats` interface (starvedAvg, acresPerPerson, etc.).

### Phase 2: Evaluation Logic
**Goal:** Implement the scoring algorithm.
**Affected Files:**
- `src/logic/EvaluationEngine.ts` (Create)
**TODOs:**
- [ ] TODO 1: Create static `EvaluationEngine` class.
- [ ] TODO 2: Implement `evaluate()` method using the criteria:
    - `IMPEACHED`: if any single year starvation > 45% (this may need to be passed in or checked via state).
    - `FANTASTIC`: avg starvation ≤ 3%, acres/person ≥ 10.
    - `GOOD`: avg starvation ≤ 10%, acres/person ≥ 9.
    - `POOR`: avg starvation ≤ 33%, acres/person ≥ 7.
    - `TERRIBLE`: otherwise.
- [ ] TODO 3: Implement `getRatingDescription()` to return descriptive text for each `GameRating`.

### Phase 3: Unit Tests & Documentation
**Goal:** Verify scoring accuracy across all rating tiers.
**Affected Files:**
- `test/logic/EvaluationEngine.test.ts` (Create)
**TODOs:**
- [ ] TODO 1: Write test cases for each `GameRating` tier with specific input values.
- [ ] TODO 2: Verify that `IMPEACHED` takes precedence over other ratings.
- [ ] TODO 3: Update `mkdocs.yml` or relevant documentation.

## Verification Criteria
- [ ] Unit tests cover all Actions.
- [ ] No direct Action calls to other modules.
- [ ] Documentation updated in `mkdocs.yml`.
