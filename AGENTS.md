# Agent instructions

## Project and architecture

RuDir Explorer is a planned Windows/Linux file explorer and Rust learning project. No feature is implemented yet. Work in small, reviewable increments. Public documentation and commits use English; the application targets English and Spanish. These instructions do not depend on private planning or local skills.

Build a Cargo workspace with `rudir-core` shared by separate CLI and Iced GUI applications. Keep filesystem operations off the UI thread. Use bounded workers and queues, request IDs and cancellation to discard stale results. Preserve native paths (`PathBuf`/`OsString`); display strings are not filesystem identities. The CLI initially covers listing, metadata, sorting, traversal and then search.

## Safety and recovery

Initially guarantee ordinary files and directories on local and USB volumes only. Reject links or special attributes when correct preservation cannot be established. Never remove a source from a cross-volume move before the destination is verified and persisted to the extent supported by the platform. Stage copies in temporary files, verify before publication, record transitions before destructive actions, and reconcile after restart; SQLite transactions do not make filesystem changes atomic. Detect external changes before resuming or undoing; do not overwrite later work. Cancellation and recovery must be repeatable. Default backup retention is 7 days and 5 GiB; if insufficient, ask to increase the limit or cancel, preserving pending work. Test destructive behavior only in isolated temporary environments.

Use one active write operation initially and bounded independent reads. Investigate Windows, X11 and Wayland clipboard and bidirectional drag-and-drop early; 0.1 depends on demonstrated integration. Document filesystem and hardware durability limits rather than promising absolute crash safety.

## Dependencies and validation

Use stable Rust, edition 2024, Iced 0.14, Tokio, SQLite via rusqlite, BLAKE3 and Fluent as planned baselines, subject to compatibility and license review before adoption. Pin the toolchain and review dependency versions and licenses when creating the workspace; commit `Cargo.lock`. Avoid unnecessary dependencies. Keep native integration behind adapters.

Once a workspace exists run `cargo fmt --all -- --check`, `cargo clippy --workspace --all-targets -- -D warnings`, `cargo test --workspace`, and `cargo build --workspace`. Add meaningful isolated tests for behavior and failure paths; report manual Windows 11 and Ubuntu 24.04 GNOME X11/Wayland evidence when relevant. Compilation alone does not prove native integration. Measure performance in release builds under comparable cold and warm cache conditions; do not claim unmeasured improvements.

## Git and done

Use short branches and small Conventional Commits in English. Review staged files before each local commit. Do not push or merge; those actions belong to the maintainer. Never add local planning, `.agents/`, skill lockfiles, credentials, logs, test data, backups or build artifacts. Preserve unrelated user changes. A task is done when acceptance criteria, relevant checks, platform limitations and user-visible documentation are addressed and results are reported. State unavailable checks explicitly.
