# Module 01: GameState Store - Implementation Plan

## Purpose
Central reactive state container holding all game variables (population, acres, grain, year, etc.) using `ReactiveStoreBase`.

## Public Interface (Lean)
### Reactive Store
- `population: ReactiveValue<number>` — current population — Serializable
- `acres: ReactiveValue<number>` — owned land — Serializable
- `grain: ReactiveValue<number>` — bushels in store — Serializable
- `year: ReactiveValue<number>` — current year (1-10) — Serializable
- `harvestYield: ReactiveValue<number>` — bushels per acre this year — Serializable
- `landPrice: ReactiveValue<number>` — bushels per acre for trading — Serializable
- `starvedTotal: ReactiveValue<number>` — cumulative deaths — Serializable
- `starvedAvg: ReactiveValue<number>` — average starvation % — Serializable
- `fedThisYear: ReactiveValue<number>` — people with full stomachs — Serializable
- `immigrants: ReactiveValue<number>` — new arrivals this year — Serializable
- `events: ReactiveList<GameEvent>` — event log entries — Serializable

### Actions
- `resetState()`: void — Resets all reactive values to starting conditions.
- `addEvent(event: GameEvent)`: void — Appends a new event to the event log.

## Implementation Phases

### Phase 1: Domain Types & Store
**Goal:** Define the data structures and the singleton store.
**Affected Files:**
- `src/state/GameState.ts` (Create)
- `src/state/GameStateStore.ts` (Create)
**TODOs:**
- [ ] TODO 1: Create `GameEvent` domain type in `GameState.ts` (including properties like `text`, `type`, `year`).
- [ ] TODO 2: Create `GameStateStore` inheriting `ReactiveStoreBase`.
- [ ] TODO 3: Implement singleton `instance` getter in `GameStateStore`.
- [ ] TODO 4: Define all public reactive properties as `ReactiveValue<number>` or `ReactiveList<GameEvent>`.
- [ ] TODO 5: Add `@jsonProperty` decorators to all serializable properties.

### Phase 2: Core Actions
**Goal:** Implement basic state mutation logic.
**Affected Files:**
- `src/state/GameStateActions.ts` (Create)
**TODOs:**
- [ ] TODO 1: Create static `GameStateActions` class.
- [ ] TODO 2: Implement `resetState()` to set initial values (e.g., year=1, population=10, acres=100, grain=100).
- [ ] TODO 3: Implement `addEvent(event: GameEvent)` to push to `GameStateStore.instance.events`.

### Phase 3: Unit Tests & Documentation
**Goal:** Verify state reactivity and serialization.
**Affected Files:**
- `test/state/GameStateStore.test.ts` (Create)
**TODOs:**
- [ ] TODO 1: Write tests to verify that `resetState()` correctly initializes all values.
- [ ] TODO 2: Write tests to verify that `addEvent()` updates the `events` list.
- [ ] TODO 3: Verify JSON serialization/deserialization of the store using `ReactiveSerializer`.
- [ ] TODO 4: Update `mkdocs.yml` or relevant documentation.

## Verification Criteria
- [ ] Unit tests cover all Actions.
- [ ] Store follows singleton pattern and inherits `ReactiveStoreBase`.
- [ ] Documentation updated in `mkdocs.yml`.
- [ ] No direct Action calls to other modules.
