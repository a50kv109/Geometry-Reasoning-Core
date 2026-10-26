# Testing

Run from the package root with Node.js 20+ and npm:

```sh
npm install
npm test
npm run test:exp
npm run build
```

`npm test` executes `scripts/runTests.ts`, combining deterministic reflection tests and JSON Schema validation. `npm run test:exp` runs experimental 2D/3D branch-selection assertions. `npm run build` runs TypeScript in no-emit mode. A command that cannot start because dependencies are unavailable is blocked, not passed. Test results cover the fixtures in these suites only.
