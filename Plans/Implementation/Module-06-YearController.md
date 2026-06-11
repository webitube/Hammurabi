# Module 06: YearController - Implementation Plan

## Purpose
Orchestrates the yearly game cycle — the central loop that sequences market, decisions, harvest, population, and evaluation.

## Public Interface (Lean)
### Reactive Store
- `isGameOver: ReactiveValue<boolean>` — game over flag — Ephemeral

### Actions
- `startNewGame()`: void — Reset state and begin year 1.
- `processYear(decisions: GameDecisions)`: void — Execute one full year cycle.
- `evaluateTerm()`: void — Calculate final performance rating and trigger end screen.

## Implementation Phases

### Phase 1: Store & Initialization
**Goal:** Set up the controller state and game start logic.
**Affected Files:**
- `src/logic/YearControllerStore.ts` (Create)
- `src/logic/YearController.ts` (Create)
**TODOs:**
- [ ] TODO 1: Create `YearControllerStore` with `isGameOver` reactive value.
- [ ] TODO 2: Implement `startNewGame()`:
    - Call `GameStateActions.resetState()`.
    - Set `YearControllerStore.instance.isGameOver.Set(false)`.
    - Add "Welcome" event to `GameStateStore`.

### Phase 2: Year Cycle Orchestration
**Goal:** Implement the sequence of events for a single year.
**Affected Files:**
- `src/logic/YearController.ts` (Modify)
**TODOs:**
- [ ] TODO 1: Implement `processYear(decisions)`:
    - 1. Call `MarketEngine.generateLandPrice()` and update `GameStateStore`.
    - 2. Process land trades using `MarketEngine.buyAcres()` / `sellAcres()`.
    - 3. Validate and deduct seeds using `FarmEngine.validatePlanting()` / `deductSeed()`.
    - 4. Calculate harvest using `FarmEngine.calculateHarvest()`.
    - 5. Calculate rat damage using `FarmEngine.calculateRatDamage()`.
    - 6. Calculate feeding and starvation using `PopulationEngine.calculateFedPopulation()` / `calculateStarvation()`.
    - 7. Check for plague and calculate births using `PopulationEngine.checkPlague()` / `calculateBirths()`.
    - 8. Update `GameStateStore` (year++, population, grain, etc.).
    - 9. Check for impeachment via `PopulationEngine.validateStarvationThreshold()`. If true, set `isGameOver = true`.

### Phase 3: Term Evaluation
**Goal:** Implement the end-of-game logic.
**Affected Files:**
- `src/logic/YearController.ts` (Modify)
**TODOs:**
- [ ] TODO 1: Implement `evaluateTerm()`:
    - Call `EvaluationEngine.evaluate()` with final stats.
    - Set `YearControllerStore.instance.isGameOver.Set(true)`.

### Phase 4: Unit Tests & Documentation
**Goal:** Verify the full game loop.
**Affected Files:**
- `test/logic/YearController.test.ts` (Create)
**TODOs:**
- [ ] TODO 1: Write a "Happy Path" test: simulate 10 years of successful play.
- [ ] TODO 2: Write an "Impeachment" test: simulate a year with > 45% starvation.
- [ ] TODO 3: Verify that `evaluateTerm()` is called after year 10.
- [ ] TODO 4: Update `mkdocs.yml` or relevant documentation.

## Verification Criteria
- [ ] Unit tests cover all Actions.
- [ ] Store follows singleton pattern and inherits `ReactiveStoreBase`.
- [ ] No direct Action calls to other modules' internal state (only public interfaces).
- [ ] Documentation updated in `mkdocs.yml`.
