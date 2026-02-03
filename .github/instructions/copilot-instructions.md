**Overview**
- Purpose: Assist AI coding agents to quickly understand and contribute to this React + Vite TypeScript app.
- App type: Single-page React app using Vite, TypeScript, Tailwind.

**Architecture (big picture)**
- **UI layers:** Core UI components live in [src/components](src/components/) — key screens: [src/components/StartScreen.tsx](src/components/StartScreen.tsx) and [src/components/GameScreen.tsx](src/components/GameScreen.tsx).
- **Game logic:** State and game flow are in [src/hooks/useBingoGame.ts](src/hooks/useBingoGame.ts). Pure game algorithms are in [src/utils/bingoLogic.ts](src/utils/bingoLogic.ts) (well-covered by tests in [src/utils/bingoLogic.test.ts](src/utils/bingoLogic.test.ts)).
- **Data:** Static question data is in [src/data/questions.ts](src/data/questions.ts).
- **Assets/config:** Vite config at [vite.config.ts](vite.config.ts), TypeScript settings at [tsconfig.json](tsconfig.json), ESLint config at [eslint.config.js](eslint.config.js).

**Developer workflows (commands)**
- Install: `npm install`
- Dev server: `npm run dev` (opens at http://localhost:5173/)
- Build: `npm run build` (runs `tsc -b` then `vite build`)
- Tests: `npm run test` (Vitest — unit tests located under `src/utils`)
- Lint: `npm run lint` (ESLint; note: currently errors due to `parserOptions.project` / tsconfig inclusion)

**Project-specific conventions & patterns**
- Keep domain logic in `src/utils` and `src/hooks` — UI components should be thin and read-only where possible.
  - Example: `generateBoard`, `toggleSquare`, `checkBingo` live in [src/utils/bingoLogic.ts](src/utils/bingoLogic.ts) and are accessed by the hook in [src/hooks/useBingoGame.ts](src/hooks/useBingoGame.ts).
- Tests target pure logic functions (see [src/utils/bingoLogic.test.ts](src/utils/bingoLogic.test.ts)). Prefer adding unit tests for new algorithmic code rather than UI snapshots.
- Tailwind v4 is used; follow the project's Tailwind setup in `index.css` and `package.json` dependencies.

**Integration points & external deps**
- Runtime: `react` / `react-dom` + Vite with `@vitejs/plugin-react`.
- Styling: `tailwindcss` + `@tailwindcss/vite` plugin.
- Testing: `vitest` + `@testing-library/react`.
- Linting: ESLint configuration expects TypeScript project references; see [eslint.config.js](eslint.config.js) and [tsconfig.app.json](tsconfig.app.json) for how TypeScript projects are laid out.

**Common issues & quick fixes**
- ESLint parsing errors about `parserOptions.project`: this occurs when ESLint cannot locate tsconfig paths for the files. Quick options:
  - Adjust `eslint.config.js` to remove or scope `parserOptions.project`, or
  - Ensure `tsconfig.json` and `tsconfig.app.json` include the `src` files (project references).
- If adding new TypeScript files, ensure they're included by the TypeScript project referenced by ESLint.

**Where to look for examples**
- Game hook usage in [src/components/GameScreen.tsx](src/components/GameScreen.tsx).
- Board rendering in [src/components/BingoBoard.tsx](src/components/BingoBoard.tsx) and square interaction in [src/components/BingoSquare.tsx](src/components/BingoSquare.tsx).
- Test patterns in [src/utils/bingoLogic.test.ts](src/utils/bingoLogic.test.ts).

**Agent behavior rules (do this first)**
- Prefer small, focused changes: update the hook or utils for logic changes, and the corresponding component only for view changes.
- Run tests locally before opening PRs: `npm run test`.
- When modifying TypeScript configuration or ESLint, run `npm run lint` to verify no new parser/project errors are introduced.
- Leave UI/UX tweaks minimal unless requested — this repo focuses on the bingo logic.

**PR checklist for agents**
- Tests updated/added for logic changes.
- Lint passes or known ESLint issues documented in PR description.
- Dev server runs and primary flows (start → generate board → mark squares) work.

---
Please review this guidance and tell me if you want more detail on any section (examples, deeper architecture notes, or automated fixes for the ESLint `parserOptions.project` issue).
