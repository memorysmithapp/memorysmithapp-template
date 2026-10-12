# Changelog

All notable changes to this repository are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this repository adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- A sixth check in `Quality`: the links at the foot of `CHANGELOG.md` name the repository the check runs in, so an adoption that forgets to rewrite them fails on its pull request (#14).

### Fixed

- A repository created from `memorysmithapp-template` no longer receives a `v0.1.0` tag and Release of the template on its initial commit: `Release` publishes only when the links at the foot of `CHANGELOG.md` name the repository it runs in (#14).

## [0.1.0] - 2026-10-12

### Added

- `AGENTS.md`, how an agent works in this repository: identity, reading and writing maps, limits, invariants, verified commands, the checklist before calling something done, and the adoption step of a repository created from this one (#2).
- `CLAUDE.md`, the single line `@AGENTS.md`, so Claude Code loads the instructions in every session and sub-agent (#2).
- `SDLC.md`, how a change travels from a need to a release: life cycle, issues and milestones, branches, commits, when an issue closes, the three sections of a pull request, a blocked merge, tests and review, versioning, release, rollback and done criteria (#3).
- `PRD.md`, the product requirements of `memorysmithapp-template` itself: problem, audience, goals and scope, principles, ubiquitous language, journeys, the business rules `RN-DOC-001`–`007`, `RN-VER-001`–`002` and `RN-ADO-001`, quality requirements and acceptance criteria (#4).
- `ARCHITECTURE.md`, the organisation of the repository: overview, layout, the mechanism of each invariant of `AGENTS.md`, integrations, operation, and the reconstructed records ADR-001 to ADR-007 of the decisions declared before the repository existed (#5).
- `README.md`, what this repository is, how to create a repository from it and how the first session adopts it (#6).
- `package.json` at the root, private, named `@memorysmithapp/template`, the one home of the version, with pnpm pinned (#6).
- `.gitignore` and `.editorconfig` (#6).
- `scripts/setup-repo.sh`, which applies to a created repository what a copy does not carry: description, topics, merge options, wiki and discussions off, and the ruleset `main`; idempotent, using only `gh` and `jq` (#7).
- The workflow `Quality` and `pnpm run quality`: the version agrees with `CHANGELOG.md`, `CHANGELOG.md` keeps its format, `CLAUDE.md` is exactly the import, relative links and anchors resolve, and no document carries a version footer; with `pnpm test` making each check fail on a deliberate violation (#8).
- `scripts/setup-repo.sh` requires the status check `Quality` in the ruleset `main` (#8).
- The workflow `Release`: on every push to `main`, it writes the annotated tag of the version in `package.json` on the merged commit and the GitHub Release with the notes of its `CHANGELOG.md` section, and refuses a tag that already names another commit (#9).

### Changed

- `LICENSE` names `memorysmithapp` as the copyright holder (#6).
- `ARCHITECTURE.md` records that the npm organisation `memorysmithapp` exists on the free plan, so a package published under `@memorysmithapp` declares `"publishConfig": { "access": "public" }`, a package never meant to be published declares `"private": true`, and publishing from CI goes through trusted publishing; ADR-006 and `SDLC.md` §10 point at it (#11).

[unreleased]: https://github.com/memorysmithapp/memorysmithapp-template/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/memorysmithapp/memorysmithapp-template/releases/tag/v0.1.0
