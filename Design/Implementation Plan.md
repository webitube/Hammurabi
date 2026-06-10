# Hammurabi TypeScript Port — Implementation Plan

## Phase 1: Project Setup
**Goal:** Initialize the Vite + TypeScript project with ReactiveTypescript integration.

### TODO List
- [ ] Create project directory `hammurabi-ts/`
- [ ] Initialize with `npm create vite@latest hammurabi-ts -- --template ts`
- [ ] Install dependencies: `reactive-typescript` (from local ReactiveTypescript), `vitest`
- [ ] Configure `tsconfig.json` with strict mode
- [ ] Configure `vite.config.ts` for SPA build
- [ ] Set up ESLint + Prettier
- [ ] Create folder structure:
  ```
  hammurabi-ts/
  ├── src/
  │   ├── main.ts
  │   ├── types/
  │   │   ├── gameTypes.ts
  │   │   └── events.ts
  │   ├── store/
  │   │   └── GameState.ts
  │   ├── engines/
  │   │   ├── MarketEngine.ts
  │   │   ├── FarmEngine.ts
  │   │   ├── PopulationEngine.ts
  │   │   └── EvaluationEngine.ts
  │   ├── controller/
  │   │   └── YearController.ts
  │   └── ui/
  │       ├── GameUI.ts
  │       ├── DashboardPanel.ts
  │       ├── DecisionPanel.ts
  │       ├── EventLogPanel.ts
  │       └── EndScreen.ts
  ├── public/
  │   └── index.html
  ├── tests/
  │   ├── engines/
  │   │   ├── MarketEngine.test.ts
  │   │   ├── FarmEngine.test.ts
  │   │   ├── PopulationEngine.test.ts
  │   │   └── EvaluationEngine.test.ts
  │   └── controller/
  │       └── YearController.test.ts
  ├── index.html
  ├── vite.config.ts
  ├── tsconfig.json
  └── package.json
  ```
- [ ] Verify build: `npm run build` succeeds
- [ ] Verify dev server: `npm run dev` launches

---

## Phase 2: Core Types and State Store
**Goal:** Define shared types and implement the reactive GameState store.

### TODO List
- [ ] Create `src/types/gameTypes.ts` with `GameDecisions`, `GameRating`, `EvaluationStats`
- [ ] Create `src/types/events.ts` with `GameEvent`, `EventType`
- [ ] Create `src/store/GameState.ts` extending `ReactiveStoreBase`
- [ ] Implement all `ReactiveValue` properties for game state
- [ ] Implement `ReactiveList<GameEvent>` for event log
- [ ] Implement `reset()` method to initialize default values
- [ ] Implement `advanceYear()` method
- [ ] Implement `addEvent()` method
- [ ] Write unit tests for GameState store initialization and reset
- [ ] Verify reactive subscriptions work correctly

---

## Phase 3: Game Engines (Pure Logic)
**Goal:** Implement all pure logic engines with comprehensive unit tests.

### TODO List — MarketEngine
- [ ] Create `src/engines/MarketEngine.ts`
- [ ] Implement `generateLandPrice()` — random 17-26
- [ ] Implement `buyAcres()` — validate grain, deduct cost, add acres
- [ ] Implement `sellAcres()` — validate ownership, add grain, remove acres
- [ ] Write tests: normal buy, normal sell, insufficient grain, insufficient acres, zero acres

### TODO List — FarmEngine
- [ ] Create `src/engines/FarmEngine.ts`
- [ ] Implement `validatePlanting()` — check acres owned, grain for seed, workers available
- [ ] Implement `calculateHarvest()` — random yield 1-5 × planting acres
- [ ] Implement `calculateRatDamage()` — random factor × grain stores
- [ ] Implement `deductSeed()` — half of planting acres
- [ ] Write tests: valid planting, insufficient grain, insufficient workers, max planting, harvest yields, rat damage

### TODO List — PopulationEngine
- [ ] Create `src/engines/PopulationEngine.ts`
- [ ] Implement `calculateFedPopulation()` — grain / 20 per person
- [ ] Implement `calculateBirths()` — formula: `INT(C * (20*A+S) / P / 100 + 1)`
- [ ] Implement `checkPlague()` — 15% chance modified by grain factor
- [ ] Implement `calculateStarvation()` — population minus fed
- [ ] Implement `validateStarvationThreshold()` — >45% triggers impeachment
- [ ] Write tests: fed calculation, birth formula, plague probability, starvation threshold

### TODO List — EvaluationEngine
- [ ] Create `src/engines/EvaluationEngine.ts`
- [ ] Implement `evaluate()` — rating based on avg starvation and acres/person
- [ ] Implement `getRatingDescription()` — descriptive text for each rating
- [ ] Implement `getHistoricalComparison()` — historical figure references
- [ ] Write tests: all rating thresholds, edge cases

---

## Phase 4: YearController
**Goal:** Orchestrate the yearly game cycle.

### TODO List
- [ ] Create `src/controller/YearController.ts`
- [ ] Implement `startNewGame()` — reset state, initialize year 1
- [ ] Implement `processYear()` — sequence: market → decisions → harvest → population → advance
- [ ] Implement `evaluateTerm()` — call EvaluationEngine after year 10
- [ ] Implement `isGameOver()` — check year counter or impeachment
- [ ] Wire up reactive subscriptions for year-change and game-over events
- [ ] Write integration tests: full year cycle, impeachment scenario, 10-year completion

---

## Phase 5: UI Layer
**Goal:** Build the browser UI with HTML, CSS, and TypeScript.

### TODO List — HTML Structure
- [ ] Create `index.html` with semantic structure
- [ ] Add header bar with title, year counter, rating
- [ ] Add dashboard panel container (grid of resource cards)
- [ ] Add decision panel container (form inputs)
- [ ] Add event log container (scrollable div)
- [ ] Add end-screen overlay container (hidden by default)

### TODO List — CSS Styling
- [ ] Create `src/ui/styles.css` with CSS custom properties
- [ ] Implement clay tablet theme (colors, textures, borders)
- [ ] Style dashboard cards with grid layout
- [ ] Style decision form with input validation states
- [ ] Style event log with color-coded severity
- [ ] Style end-screen overlay with dramatic entrance
- [ ] Implement responsive breakpoints (1024px, 768px)
- [ ] Add animations (fade, slide, pulse, flip)

### TODO List — UI Components
- [ ] Create `src/ui/GameUI.ts` — main UI controller
- [ ] Create `src/ui/DashboardPanel.ts` — render resource cards
- [ ] Create `src/ui/DecisionPanel.ts` — render form with validation
- [ ] Create `src/ui/EventLogPanel.ts` — render event log entries
- [ ] Create `src/ui/EndScreen.ts` — render evaluation screen
- [ ] Wire up input handlers and submit flow
- [ ] Subscribe to reactive state changes
- [ ] Implement inline validation feedback
- [ ] Add ARIA live regions for accessibility

---

## Phase 6: Integration and Polish
**Goal:** Connect all pieces, test end-to-end, and polish the experience.

### TODO List
- [ ] Wire `main.ts` to initialize GameState, YearController, and GameUI
- [ ] Test full game flow: start → decisions → year cycle → end screen
- [ ] Verify all reactive subscriptions update correctly
- [ ] Test edge cases: zero population, zero grain, max acres
- [ ] Cross-browser testing (Chrome, Firefox, Safari, Edge)
- [ ] Performance testing: ensure smooth animations
- [ ] Accessibility audit (keyboard nav, screen reader, contrast)
- [ ] Fix any remaining bugs
- [ ] Add final polish: transitions, micro-interactions, error states

---

## Phase 7: Post-MVP Expansion (Deferred)
**Goal:** Add creative expansions identified in the UI/UX design.

### TODO List
- [ ] Implement trade routes system
- [ ] Implement building construction (granaries, temples, walls)
- [ ] Implement diplomacy with neighboring city-states
- [ ] Implement technology tree
- [ ] Implement population class system
- [ ] Implement tax system
- [ ] Add random events (floods, droughts, refugee waves)
- [ ] Add city visualization SVG
- [ ] Add dark mode
- [ ] Add sound effects
- [ ] Add achievement system

---

## Testing Strategy

### Unit Tests (Vitest)
- All engines tested in isolation with mock inputs
- Coverage target: 90%+ for engine code
- Test boundary conditions and edge cases

### Integration Tests
- YearController tested with mocked engines
- Full year cycle tested end-to-end
- Reactive state updates verified

### UI Tests
- Manual testing for visual correctness
- Responsive layout testing at all breakpoints
- Accessibility testing with screen readers

---

## Build and Deployment

### Development
```bash
npm run dev        # Start Vite dev server with HMR
npm run build      # Production build
npm run preview    # Preview production build locally
npm run test       # Run Vitest unit tests
npm run test:watch # Run Vitest in watch mode
```

### Deployment
- Build output goes to `dist/` directory
- Deploy to any static hosting (GitHub Pages, Netlify, Vercel)
- No server-side requirements
