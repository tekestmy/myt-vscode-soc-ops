# Soc Ops - AI Agent Instructions

> **Social Bingo Game**: 5x5 grid matching social prompts for in-person mixers

## 🔒 Mandatory Development Checklist

Before committing or deploying, ensure ALL items are checked:

- [ ] **Lint**: `npm run lint` passes with no errors
- [ ] **Build**: `npm run build` completes successfully  
- [ ] **Test**: `npm run test` shows all tests passing

## Architecture Overview

**State Pattern**: `useBingoGame` hook controls all game state + localStorage persistence  
**Pure Logic**: `src/utils/bingoLogic.ts` - stateless functions for game mechanics  
**Types**: `src/types/index.ts` - `BingoSquareData`, `BingoLine`, `GameState`

**Component Flow**: `App.tsx` → `StartScreen` | `GameScreen` → `BingoBoard` → `BingoSquare` (×25)

## Critical Patterns

### Game Logic
- **Pure Functions**: All logic in `bingoLogic.ts` - no React state
- **Immutable Updates**: `toggleSquare()` returns new arrays, never mutates
- **Center Free Space**: Always index 12 in 25-grid, auto-marked on generation
- **Win Detection**: `checkBingo()` returns `BingoLine` with winning square IDs

### State Management
```typescript
// localStorage pattern with version validation
const STORAGE_KEY = 'bingo-game-state';
const STORAGE_VERSION = 1;
```

### Component Props
```typescript
// Always use specific callback signatures
interface GameScreenProps {
  board: BingoSquareData[];
  onSquareClick: (squareId: number) => void;
}
```

## Development Workflow

### Test-First Approach
- `src/utils/bingoLogic.test.ts` - 21 tests covering all game mechanics
- New game logic requires tests BEFORE implementation
- Use `npm run test -- --watch` for TDD workflow

### Component Development
1. Define TypeScript interface for props
2. Functional components only
3. Event handlers: `handle` prefix (`handleSquareClick`)
4. Direct Tailwind classes (no CSS modules)

## Key Implementation Details

**Mobile-First**: `user-scalable=no`, touch-friendly `py-4 px-8` buttons  
**Data Flow**: `questions.ts` → `generateBoard()` → user clicks → `toggleSquare()` → `checkBingo()`  
**Deployment**: Auto GitHub Pages on `main` push, Vite handles base path

## Key Files
- **Questions**: `src/data/questions.ts` (24 social prompts)
- **Game State**: `src/hooks/useBingoGame.ts` (add features here)
- **Logic**: `src/utils/bingoLogic.ts` (win conditions, board generation)
- **Types**: `src/types/index.ts` (TypeScript definitions)