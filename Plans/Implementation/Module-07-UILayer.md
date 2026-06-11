# Module 07: UI Layer - Implementation Plan

## Purpose
Renders the game state and collects player input. Built with vanilla TypeScript + HTML + CSS.

## Public Interface (Lean)
### Reactive Store
- (None - Subscribes to GameStateStore and YearControllerStore)

### Actions
- `renderDashboard(state: GameState)`: void — Update stats panel.
- `renderDecisionsPanel()`: void — Show buy/sell/feed/plant inputs.
- `renderEventLog(events: GameEvent[])`: void — Append event entries.
- `renderEndScreen(rating: GameRating, stats: EvaluationStats)`: void — Show final evaluation.
- `bindInputHandlers(callbacks: GameCallbacks)`: void — Wire up button clicks.

## Implementation Phases

### Phase 1: HTML/CSS Structure
**Goal:** Create the visual shell of the application.
**Affected Files:**
- `index.html` (Create)
- `src/styles/main.css` (Create)
**TODOs:**
- [ ] TODO 1: Create `index.html` with containers for Dashboard, Decision Panel, Event Log, and End Screen.
- [ ] TODO 2: Implement CSS for the "Ancient Sumerian" theme (clay-tablet colors, cuneiform-inspired fonts).
- [ ] TODO 3: Ensure responsive layout for desktop and tablet.

### Phase 2: Dashboard & Event Log Rendering
**Goal:** Implement reactive updates for stats and logs.
**Affected Files:**
- `src/ui/DashboardPanel.ts` (Create)
- `src/ui/EventLogPanel.ts` (Create)
- `src/ui/UIManager.ts` (Create)
**TODOs:**
- [ ] TODO 1: Implement `DashboardPanel` to subscribe to `GameStateStore` and update DOM elements.
- [ ] TODO 2: Implement `EventLogPanel` to subscribe to `GameStateStore.events` and append new entries.
- [ ] TODO 3: Implement `UIManager` to coordinate these panels.

### Phase 3: Decision Panel & Input Handling
**Goal:** Implement the player interaction loop.
**Affected Files:**
- `src/ui/DecisionPanel.ts` (Create)
- `src/ui/UIManager.ts` (Modify)
**TODOs:**
- [ ] TODO 1: Implement `DecisionPanel` with inputs for Buy/Sell Acres, Feed Population, and Plant Acres.
- [ ] TODO 2: Implement input validation feedback (inline messages instead of alerts).
- [ ] TODO 3: Bind "Process Year" button to `YearController.processYear()`.

### Phase 4: End Screen & Game Flow
**Goal:** Implement the game start and end transitions.
**Affected Files:**
- `src/ui/EndScreen.ts` (Create)
- `src/ui/UIManager.ts` (Modify)
**TODOs:**
- [ ] TODO 1: Implement `EndScreen` to display the final `GameRating` and stats.
- [ ] TODO 2: Subscribe `UIManager` to `YearControllerStore.isGameOver` to toggle between Decision Panel and End Screen.
- [ ] TODO 3: Implement "Start New Game" button calling `YearController.startNewGame()`.

### Phase 5: Integration Tests & Polish
**Goal:** Final UX verification.
**Affected Files:**
- `test/ui/UIIntegration.test.ts` (Create)
**TODOs:**
- [ ] TODO 1: Verify that UI updates immediately when `GameStateStore` values change.
- [ ] TODO 2: Verify that invalid inputs are blocked and show errors.
- [ ] TODO 3: Perform a full play-through to ensure all screens transition correctly.

## Verification Criteria
- [ ] UI reacts to all `GameStateStore` changes.
- [ ] No direct mutation of state in UI (all via `YearController` or `GameStateActions`).
- [ ] Theme matches the "Ancient Sumerian" aesthetic.
- [ ] Responsive layout works on tablet/desktop.
