# Geometry Reasoning Core

Geometry Reasoning Core is a TypeScript research package for representing and checking geometric claims. It contains a 3D geometry core, a 2D reflection subsystem, experimental solution selection, and a separate verifier.

The package separates computation from trust: a producer's result is a claim, not a verified fact. Use `src/verifier/independentVerifier.ts` to check supported 2D reflection invariants independently. The verifier does not establish that every algorithm is mathematically complete or suitable for every input.

## Status and scope

This is a research package. `src/core/` contains the main geometry model and operations; `src/verifier/` contains independent checks for the reflection subsystem; `src/experimental/` contains prototypes for branch selection and 2D/3D problems. Experimental outputs should not be treated as universally correct or as proofs. The package does not model physical paper thickness, continuous folding kinematics, or general collision behavior.

## Layout

- `src/core/`: geometry types, topology, metrics, transformations, semantics, and agent gateway.
- `src/verifier/`: independent reflection checks.
- `src/experimental/`: experimental branch selection and problem domains.
- `src/tests/`: deterministic core and schema validation suites.
- `schemas/`: pattern passport JSON Schema.
- `scripts/runTests.ts`: entry point for the core and schema suites.
- `docs/`: package architecture, status, testing, and known limitations.

## Requirements and commands

Use Node.js 20 or newer and npm. From this directory:

```sh
npm install
npm test
npm run test:exp
npm run build
```

`npm test` runs the deterministic reflection and schema checks. `npm run test:exp` runs experimental cross-domain checks. `npm run build` performs TypeScript checking (`tsc --noEmit`); it does not emit distributable JavaScript.

## Reading verification results

The main test runner exits nonzero if a suite reports failure. A passing producer computation alone does not imply verification: inspect the independent verifier result for the claim being evaluated. The included tests cover specific fixtures and tolerances only; they do not prove correctness for all geometries.

## Extending a domain

Experimental domains implement the `GeometricProblem` interface in `src/experimental/types.ts` and return a `SolutionSet`. Add a domain-specific verifier or invariant checks before relying on its output. Keep candidate generation, solution selection, and independent checking as separate steps, and add tests for both accepted and rejected cases.

## Limits

See [Architecture](docs/ARCHITECTURE.md), [Status](docs/STATUS.md), [Testing](docs/TESTING.md), and [Known limitations](docs/KNOWN_LIMITATIONS.md). The current test suites are small executable checks, not formal proofs. `LICENSE` uses the copyright attribution explicitly confirmed by the project owner.
