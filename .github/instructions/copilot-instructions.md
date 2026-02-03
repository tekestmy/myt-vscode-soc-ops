- [ ] Lint (`npm run lint`)
- [ ] Build (`npm run build`)
- [ ] Test (`npm run test`)

**Overview (shortened)**
Single-page React + Vite TypeScript app (Tailwind v4). Key intent: simple Bingo game where UI components are thin and logic lives in reusable utils/hooks.

**Key areas**
- `src/components/` — UI screens and small presentational components (StartScreen, GameScreen, BingoBoard, BingoSquare).
- `src/hooks/useBingoGame.ts` — game state and orchestration.
- `src/utils/bingoLogic.ts` — pure game algorithms (well-tested in `src/utils/bingoLogic.test.ts`).
- `src/data/questions.ts` — static data.

**Useful commands**
```
npm install
npm run dev   # http://localhost:5173/
npm run build
npm run test
npm run lint
```

**Conventions & tips**
- Keep domain logic in `src/utils`/`src/hooks`; add unit tests for logic changes.
- ESLint uses TypeScript project references — if you see parser errors, check `tsconfig.app.json` and `eslint.config.js`.

**Agent rules**
- Make small, focused edits; run `npm run test` and `npm run lint` before PR.
- Document any intentional lint failures in PR description.

---
Updated and shortened. For deeper ESLint fix automation, say the word and I’ll implement it.
