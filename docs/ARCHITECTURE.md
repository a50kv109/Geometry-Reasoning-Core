# Architecture

The package has three distinct responsibilities:

1. `src/core/` represents geometry and computes operations, metrics, signatures, and derived state.
2. `src/experimental/` explores candidate solutions and branch selection. Its status is experimental.
3. `src/verifier/` independently checks supported 2D reflection claims against geometric invariants.

The separation is intentional: a producer claim is not receiver truth. Candidate generation, selection, and verification must remain distinct. The verifier currently imports the 2D reflection types and checks; it is not a general proof engine for all modules in `src/core/`.

The deterministic test runner is `scripts/runTests.ts`; it invokes `src/tests/testRunner.ts` and the schema checks. Experimental tests have their own entry point under `src/experimental/tests/`.
