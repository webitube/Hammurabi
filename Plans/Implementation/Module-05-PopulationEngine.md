# Module 05: PopulationEngine - Implementation Plan

## Purpose
Manages population dynamics — births, deaths, immigration, and plague.

## Public Interface (Lean)
### Reactive Store
- (None - Uses GameState Store)

### Actions
- `calculateFedPopulation(fedGrain: number, population: number): number` — Determines how many people are fed.
- `calculateBirths(harvestFactor: number, acresPerPerson: number, grainPerPerson: number, population: number): number` — Calculates new births.
- `checkPlague(grainFactor: number): boolean` — Determines if a plague occurs.
- `calculateStarvation(population: number, fed: number): number` — Calculates number of deaths.
- `validateStarvationThreshold(starved: number, population: number): boolean` — Returns true if impeachment is triggered (> 45%).

## Implementation Phases

### Phase 1: Feeding & Starvation
**Goal:** Implement the basic survival logic.
**Affected Files:**
- `src/logic/PopulationEngine.ts` (Create)
**TODOs:**
- [ ] TODO 1: Create static `PopulationEngine` class.
- [ ] TODO 2: Implement `calculateFedPopulation()`: divide `fedGrain` by consumption per person.
- [ ] TODO 3: Implement `calculateStarvation()`: `population - fed`.
- [ ] TODO 4: Implement `validateStarvationThreshold()`: check if `starved / population > 0.45`.

### Phase 2: Growth & Plague
**Goal:** Implement births and random plague events.
**Affected Files:**
- `src/logic/PopulationEngine.ts` (Modify)
**TODOs:**
- [ ] TODO 1: Implement `calculateBirths()`: use `harvestFactor`, `acresPerPerson`, and `grainPerPerson` to determine growth.
- [ ] TODO 2: Implement `checkPlague()`: use `grainFactor` to determine if a plague occurs.

### Phase 3: Unit Tests & Documentation
**Goal:** Verify population dynamics.
**Affected Files:**
- `test/logic/PopulationEngine.test.ts` (Create)
**TODOs:**
- [ ] TODO 1: Write tests for `calculateFedPopulation()` and `calculateStarvation()`.
- [ ] TODO 2: Write tests for `validateStarvationThreshold()` (boundary at 45%).
- [ ] TODO 3: Write tests for `calculateBirths()` and `checkPlague()`.
- [ ] TODO 4: Update `mkdocs.yml` or relevant documentation.

## Verification Criteria
- [ ] Unit tests cover all Actions.
- [ ] No direct Action calls to other modules.
- [ ] Documentation updated in `mkdocs.yml`.
