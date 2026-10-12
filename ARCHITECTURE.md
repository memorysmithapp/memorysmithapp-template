# Architecture

How `memorysmithapp-template` is organised, and why. It describes this repository itself: what it is made of, what enforces each invariant of [`AGENTS.md` §5](AGENTS.md#5-invariants), what it integrates with, and the decisions behind it.

*Rewritten on adoption*, except [§6](#6-architecture-decision-records), whose format is kept and whose records start empty. A repository created from this one keeps every heading below with the one-line instruction in italics under it, and replaces the content with its own.

Claims carry their status when it is not obvious: *observed*, *declared*, *inferred*, and **To confirm** for what was not verified ([`PRD.md`](PRD.md), RN-DOC-006).

## 1. Overview

*Instruction: what the system is made of, and how the parts relate.*

The repository carries no product code. It is made of:

- **Documents**, the core of what it delivers: `CLAUDE.md` imports `AGENTS.md`; `AGENTS.md` maps the reading and the writing onto `PRD.md`, `ARCHITECTURE.md`, `SDLC.md` and `README.md`, and states the limits and invariants in one line each; `CHANGELOG.md` records what each version changed.
- **Repository files:** `package.json`, the one home of the version; `.gitignore`, `.editorconfig` and `LICENSE`.
- **GitHub configuration** that a copy does not carry: the ruleset `main` of this repository.

Each fact has one home ([`PRD.md` RN-DOC-004](PRD.md#7-features-and-rules)): an invariant is stated in `AGENTS.md` and its mechanism here; a rule is stated in `PRD.md` and enforced where §3 says.

## 2. Layout

*Instruction: every file and directory, and what it is for.*

| Path | What it is for |
|---|---|
| `CLAUDE.md` | The single line `@AGENTS.md`, which Claude Code imports at the start of every session and sub-agent |
| `AGENTS.md` | How an agent works here: identity, reading and writing maps, limits, invariants, verified commands, the checklist before done, adoption |
| `PRD.md` | What the product solves and delivers, under which rule |
| `ARCHITECTURE.md` | This document |
| `SDLC.md` | How a change travels from an issue to a release |
| `README.md` | What this is and how to start |
| `CHANGELOG.md` | What changed in each version, in Keep a Changelog 1.1.0 |
| `package.json` | The one home of the version (`version`), and the package manager pinned (`packageManager`); private, named `@memorysmithapp/template` |
| `.gitignore` | Dependencies, build output, coverage, environment files, logs, operating-system and editor files |
| `.editorconfig` | UTF-8, LF, two spaces, final newline |
| `LICENSE` | The MIT licence |

## 3. Invariants and their mechanisms

*Instruction: one subsection per invariant of `AGENTS.md` §5, saying what enforces it, or that nothing does.*

### INV-01 The version has one home

The version lives in the `version` field of the root `package.json` and nowhere else; `CHANGELOG.md` records the versions that were cut (RN-VER-001, RN-VER-002).

**Mechanism:** none mechanical yet. The writing map of `AGENTS.md` and the owner's review hold it.

### INV-02 CLAUDE.md is only the import

`CLAUDE.md` is the line `@AGENTS.md` and nothing else (RN-DOC-002). Claude Code expands an `@path` line into the contents of the file it names, so the instructions load in every session and sub-agent; a `CLAUDE.md` that only mentioned `AGENTS.md` in prose would leave reading it to the agent's judgement (*observed* in a fresh session, #2).

**Mechanism:** none mechanical yet. The owner's review holds it.

### INV-03 main changes only through a pull request

**Mechanism:** the repository ruleset `main` (*observed*, id `24923714`), active on the default branch, with no bypass actors:

- `deletion`: the branch cannot be deleted;
- `non_fast_forward`: no force push;
- `pull_request`: every change through a pull request, with 0 required approvals, merge, squash and rebase allowed.

Nobody can bypass it, administrators included (`current_user_can_bypass: never`, *observed*). A ruleset is a setting of the repository, not a file, so a created repository does not receive it.

### INV-04 Only the release workflow writes a tag

A version names one commit: the tag `vX.Y.Z` is written once, on the merged commit, and never moved or deleted ([`SDLC.md` §10](SDLC.md#10-release), [§11](SDLC.md#11-rollback)).

**Mechanism:** none mechanical yet. The limit of `AGENTS.md` §4 holds it.

## 4. Integrations

*Instruction: every external system the project depends on, and what it uses from each.*

**GitHub.**

- *Template repositories:* a repository is created from this one with *Use this template* or `gh repo create --template`, receiving a copy of the files of the default branch in one initial commit, with no link back and no settings ([ADR-004](#adr-004-a-github-template-repository-copied-once)). This repository is not marked as a template yet (*observed*); #10 tracks it.
- *Rulesets:* the ruleset `main` of [INV-03](#inv-03-main-changes-only-through-a-pull-request).
- *Issues and milestones:* GitHub's blank issue and default labels; a milestone per version ([ADR-005](#adr-005-githubs-defaults-for-issues-pull-requests-and-labels)).

**npm.** Any package a repository of the organisation publishes uses the scope `@memorysmithapp` ([ADR-006](#adr-006-the-npm-scope-memorysmithapp)). This repository publishes none.

## 5. Operation

*Instruction: what runs, where, with which permissions and secrets.*

Nothing runs: the repository has no workflow, no deployable and no secret.

## 6. Architecture decision records

*Kept on adoption: the format below stays, and a created repository starts with no record.*

Each record has an identifier, never reused; its context, decision, rationale and consequences; its date, status and **origin**. A decision that changes keeps its old record, marked *Superseded by ADR-NNN*, and a new record states the new decision.

The records ADR-001 to ADR-007 are **reconstructed**: the decisions were taken by the owner of the organisation before this repository existed, declared in #1 on 2026-10-12, and written here as records by the session that built v0.1.0.

### ADR-001 A small set of documents instead of a large CLAUDE.md

- **Context:** the main repository keeps its agent instructions in a `CLAUDE.md` of about 7,500 words and its knowledge in five documents under `docs/` (*observed*). The instructions are loaded whole in every session, and the knowledge overlaps them.
- **Decision:** each repository holds `CLAUDE.md` → `AGENTS.md`, `PRD.md`, `ARCHITECTURE.md`, `SDLC.md` and `README.md`, each answering one question (RN-DOC-001).
- **Rationale:** a document per question gives each fact one home; `AGENTS.md`, loaded always, stays a short map pointing at sections instead of a copy of them.
- **Consequences:** the writing map of `AGENTS.md` §3 becomes the arbiter of where a paragraph goes. The structure is tried here first; the main repository migrates only if it proves itself (*declared*).
- **Date:** 2026-10-12. **Status:** Accepted. **Origin:** reconstructed; declared by the owner in #1.

### ADR-002 CLAUDE.md is the AGENTS.md import

- **Context:** Claude Code reads `CLAUDE.md`; other agents read `AGENTS.md`.
- **Decision:** `CLAUDE.md` is the single line `@AGENTS.md` (RN-DOC-002).
- **Rationale:** the import makes Claude Code load the instructions automatically in every session and sub-agent; a `CLAUDE.md` that mentioned `AGENTS.md` in prose would not. One file holds the instructions for every agent.
- **Consequences:** nothing is written in `CLAUDE.md`; [INV-02](#inv-02-claudemd-is-only-the-import).
- **Date:** 2026-10-12. **Status:** Accepted. **Origin:** reconstructed; declared by the owner in #1.

### ADR-003 The version lives in the root package.json

- **Context:** the main repository reads its version out of `CLAUDE.md` with a regex, which is what keeps that file from shrinking (*observed*).
- **Decision:** the version lives in the `version` field of the root `package.json`, and nowhere else; `CHANGELOG.md` follows Keep a Changelog 1.1.0 (RN-VER-001, RN-VER-002).
- **Rationale:** `package.json` is where the tooling of the organisation already looks for a version, and a field is read without a regex.
- **Consequences:** every repository has a root `package.json`, even one with no package; [INV-01](#inv-01-the-version-has-one-home).
- **Date:** 2026-10-12. **Status:** Accepted. **Origin:** reconstructed; declared by the owner in #1.

### ADR-004 A GitHub template repository, copied once

- **Context:** the organisation needs every new repository to start with its process written, with two or three repositories in sight (*declared*).
- **Decision:** a GitHub template repository, copied once into each created repository and never synced, instead of a generator package or an organisation `.github` repository.
- **Rationale:** a template needs no tooling to create a repository and no machinery to maintain; at this number of repositories, syncing costs more than it saves. An organisation `.github` repository is not created until the need for it is felt.
- **Consequences:** an improvement made here does not reach the repositories already created; what a template does not copy, the settings of a repository, needs another mechanism.
- **Date:** 2026-10-12. **Status:** Accepted. **Origin:** reconstructed; declared by the owner in #1.

### ADR-005 GitHub's defaults for issues, pull requests and labels

- **Context:** the main repository has issue forms and custom labels (*observed*).
- **Decision:** GitHub's blank issue, no issue or pull request templates, GitHub's default labels. The format of a PR description lives as text in [`SDLC.md` §6](SDLC.md#6-pull-request).
- **Rationale:** nothing to maintain or to copy, and the format of a PR is read where the process is.
- **Consequences:** the PR format is followed by reading, not by a form.
- **Date:** 2026-10-12. **Status:** Accepted. **Origin:** reconstructed; declared by the owner in #1.

### ADR-006 The npm scope @memorysmithapp

- **Context:** repositories of the organisation will publish npm packages, the next one being `memorysmithapp/memorysmithapp-markdown` (*declared*).
- **Decision:** every package published by a repository of the organisation uses the scope `@memorysmithapp`.
- **Rationale:** the scope matches the GitHub organisation, so a package names where it lives.
- **Consequences:** the root `package.json` of each repository is named under the scope, even when private.
- **Date:** 2026-10-12. **Status:** Accepted. **Origin:** reconstructed; declared by the owner in #1.

### ADR-007 The repository is its own first instance

- **Context:** a starting point made of placeholders shows a structure but never proves it.
- **Decision:** `AGENTS.md`, `PRD.md`, `ARCHITECTURE.md` and `SDLC.md` are real documents describing this repository; each marks which of its sections a created repository keeps and which it rewrites (RN-DOC-003).
- **Rationale:** a structure that cannot describe a small repository will not describe a large one, and this repository is small and new enough that nothing breaks if a part is wrong.
- **Consequences:** a created repository has an adoption step ([`AGENTS.md` §8](AGENTS.md#8-adopting-this-repository), RN-ADO-001) that empties the content and keeps the process.
- **Date:** 2026-10-12. **Status:** Accepted. **Origin:** reconstructed; declared by the owner in #1.
