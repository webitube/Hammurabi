# Module 04: FarmEngine - Implementation Plan

## Purpose
Calculates crop planting, harvest yield, and rat damage.

## Public Interface (Lean)
### Reactive Store
- (None - Uses GameState Store)

### Actions
- `validatePlanting(acresToPlant: number, ownedAcres: number, grain: number, population: number): { valid: boolean, reason?: string }` — Validates if planting is possible.
- `calculateHarvest(plantingAcres: number, yieldFactor: number): number` — Calculates total bushels harvested.
- `calculateRatDamage(grainInStore: number, ratFactor: number): number` — Calculates bushels lost to rats.
- `deductSeed(grain: number, plantingAcres: number): number` — Calculates remaining grain after planting.

## Implementation Phases

### Phase 1: Planting Validation
**Goal:** Implement logic to ensure planting is feasible.
**Affected Files:**
- `src/logic/FarmEngine.ts` (Create)
**TODOs:**
- [ ] TODO 1: Create static `FarmEngine` class.
- [ ] TODO 2: Implement `validatePlanting()`:
    - Check if `acresToPlant` <= `ownedAcres`.
    - Check if there is enough grain for seeds.
    - Check if there is enough population to work the land.

### Phase 2: Harvest & Rat Logic
**Goal:** Implement the core farming calculations.
**Affected Files:**
- `src/logic/FarmEngine.ts` (Modify)
**TODOs:**
- [ ] TODO 1: Implement `calculateHarvest()`: multiply `plantingAcres` by `yieldFactor`.
- [ ] TODO 2: Implement `calculateRatDamage()`: apply `ratFactor` to `grainInStore`.
- [ ] TODO 3: Implement `deductSeed()`: subtract seed cost per acre from `grain`.

### Phase 3: Unit Tests & Documentation
**Goal:** Verify farming calculations.
**Affected Files:**
- `test/logic/FarmEngine.test.ts` (Create)
**TODOs:**
- [ ] TODO 1: Write tests for `validatePlanting()` (all failure modes).
- [ ] TODO 2: Write tests for `calculateHarvest()` with various yield factors.
- [ ] TODO 3: Write tests for `calculateRatDamage()` with various rat factors.
- [ ] TODO 4: Update `mkdocs.yml` or relevant documentation.

## Verification Criteria
- [ ] Unit tests cover all Actions.
- [ ] No direct Action calls to other modules.
- [ ] Documentation updated in `mkdocs.yml`.
