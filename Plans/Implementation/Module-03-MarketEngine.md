# Module 03: MarketEngine - Implementation Plan

## Purpose
Generates annual land prices and processes buy/sell transactions.

## Public Interface (Lean)
### Reactive Store
- (None - Uses GameState Store)

### Actions
- `generateLandPrice(): number` — Random price between 17-26 bushels/acre.
- `buyAcres(acres: number, grain: number): { success: boolean, acres: number, grainSpent: number }` — Processes land purchase.
- `sellAcres(acres: number, land: number): { success: boolean, acres: number, grainGained: number }` — Processes land sale.

## Implementation Phases

### Phase 1: Pricing Logic
**Goal:** Implement the random price generation.
**Affected Files:**
- `src/logic/MarketEngine.ts` (Create)
**TODOs:**
- [ ] TODO 1: Create static `MarketEngine` class.
- [ ] TODO 2: Implement `generateLandPrice()` using `Math.random()` to return a value between 17 and 26.

### Phase 2: Trading Logic
**Goal:** Implement buy/sell transactions with validation.
**Affected Files:**
- `src/logic/MarketEngine.ts` (Modify)
**TODOs:**
- [ ] TODO 1: Implement `buyAcres()`:
    - Validate if player has enough grain.
    - Calculate total cost.
    - Return success/failure and transaction details.
- [ ] TODO 2: Implement `sellAcres()`:
    - Validate if player has enough land.
    - Calculate total grain gained.
    - Return success/failure and transaction details.

### Phase 3: Unit Tests & Documentation
**Goal:** Verify trading logic and price ranges.
**Affected Files:**
- `test/logic/MarketEngine.test.ts` (Create)
**TODOs:**
- [ ] TODO 1: Write tests to verify `generateLandPrice()` is always within [17, 26].
- [ ] TODO 2: Write tests for `buyAcres()` (success case, insufficient grain case).
- [ ] TODO 3: Write tests for `sellAcres()` (success case, insufficient land case).
- [ ] TODO 4: Update `mkdocs.yml` or relevant documentation.

## Verification Criteria
- [ ] Unit tests cover all Actions.
- [ ] No direct Action calls to other modules (only reads/writes to `GameStateStore`).
- [ ] Documentation updated in `mkdocs.yml`.
