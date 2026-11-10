# Contributing to the benchmarks

The benchmark is useful only while it is fair and reproducible. A change here should keep both true.

- Read `SPEC.md` first. A change to the contract (the database, the endpoints, the rules) comes with the reason, and with new results from a run on the machine described in `results/env.json`.
- Results are produced by `run.mjs`, never edited by hand.
- `node tools/conformance.mjs <url>` must pass for the app before it is measured.
- Commit messages read `type(scope): what the code now does`. The framework's [CONTRIBUTING.md](https://github.com/NavreeHQ/navree/blob/main/CONTRIBUTING.md) has the other conventions.

Your contribution comes in under the project's terms: MIT or Apache-2.0, at the user's option (section 5 of the Apache License). There is no contributor agreement to sign.
