# Module Integration Plan

## Overview
This document describes the high-level orchestration required to integrate the individual modules into a functional Hammurabi game.

## Integration Sequence

1. **State Initialization**:
   - The `UIManager` calls `YearController.startNewGame()`.
   - `YearController` resets `GameStateStore` and sets `isGameOver = false`.
   - `UIManager` renders the initial `DashboardPanel` and `DecisionPanel`.

2. **The Yearly Loop**:
   - **Input Phase**: Player enters decisions in `DecisionPanel`.
   - **Execution Phase**: `UIManager` calls `YearController.processYear(decisions)`.
   - **Logic Chain**:
     - `YearController` $\rightarrow$ `MarketEngine` (Price $\rightarrow$ Trade).
     - `YearController` $\rightarrow$ `FarmEngine` (Plant $\rightarrow$ Harvest $\rightarrow$ Rats).
     - `YearController` $\rightarrow$ `PopulationEngine` (Feed $\rightarrow$ Starve $\rightarrow$ Births $\rightarrow$ Plague).
     - `YearController` $\rightarrow$ `GameStateStore` (Update Year, Population, Grain).
   - **Reaction Phase**: `DashboardPanel` and `EventLogPanel` automatically update via subscriptions to `GameStateStore`.

3. **Game Termination**:
   - **Condition A (Year 10)**: After processing year 10, `YearController` calls `evaluateTerm()`.
   - **Condition B (Impeachment)**: If `PopulationEngine.validateStarvationThreshold()` returns true, `YearController` sets `isGameOver = true` immediately.
   - **End State**: `UIManager` detects `isGameOver == true` and renders the `EndScreen` using `EvaluationEngine`.

## Communication Matrix

| From | To | Method | Purpose |
|------|----|--------|---------|
| `UIManager` | `YearController` | Action Call | Trigger game start/year process |
| `YearController` | `MarketEngine` | Action Call | Calculate land price and trades |
| `YearController` | `FarmEngine` | Action Call | Calculate harvest and rat damage |
| `YearController` | `PopulationEngine` | Action Call | Calculate population changes |
| `YearController` | `GameStateStore` | Reactive Set | Update global game state |
| `UI Panels` | `GameStateStore` | Subscription | Update visual display |
| `YearController` | `EvaluationEngine` | Action Call | Determine final rating |

## Final Verification
- [ ] Full 10-year cycle completes without errors.
- [ ] Impeachment triggers correctly.
- [ ] Final rating matches expected criteria.
- [ ] UI remains synchronized with state at all times.
