# Contributing

The project is in planning; implementation will proceed in small, reviewable increments. Discuss substantial changes before investing in them. Public documentation, code identifiers and commit messages use English; user-facing translations target English and Spanish.

Use short branches from `main` and focused Conventional Commits in English. Review the staged diff; exclude private data, generated artifacts, local planning, backups and logs. Maintainers perform pushes and merges. Do not commit destructive-test data.

Once the Cargo workspace exists, run `cargo fmt --all -- --check`, `cargo clippy --workspace --all-targets -- -D warnings`, `cargo test --workspace`, and `cargo build --workspace` with the pinned toolchain. These commands are planned and cannot yet run. Report platform-specific manual checks and limitations. Describe behavior, tests, risks and user-visible changes in contributions. See [AGENTS.md](AGENTS.md).
