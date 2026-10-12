# PRD

What `memorysmithapp-template` solves and delivers, and under which rule. Here the product is this repository itself: it is its own first instance.

*Rewritten on adoption.* A repository created from this one keeps every heading below with the one-line instruction in italics under it, and replaces the content with its own project's.

Claims carry their status when it is not obvious: *observed* (seen in this repository or in GitHub), *declared* (said by the owner of the organisation), *inferred* (an interpretation to confirm). What was not verified is marked **To confirm**.

## 1. Problem

*Instruction: the pain the product removes, for whom, and how it shows today.*

Every new repository of the `memorysmithapp` organisation starts empty and rediscovers its process and its agent instructions: how a change reaches `main`, how a version is cut, where a fact is written. The main repository, [`memorysmithapp/memorysmithapp`](https://github.com/memorysmithapp/memorysmithapp), shows where that leads: its agent instructions grew into a `CLAUDE.md` of about 7,500 words, loaded whole in every session, which also holds the product's version and so cannot be shrunk (*observed*).

## 2. Audience

*Instruction: who uses the product, and what each of them needs from it.*

- **The owner of the organisation**, who creates repositories and reviews and merges every pull request. Needs a new repository to start with its process already written and its protections applied (*declared*).
- **The agents working in the organisation's repositories**, Claude Code first. Need to know, in every session and from the repository alone, how to work, where to read and where to write (*declared*).

## 3. Goals and scope

*Instruction: what the current version delivers, and what it deliberately does not.*

**Delivers:**

- The set of documents a repository works by, each answering one question ([§7](#7-features-and-rules), RN-DOC-001), written as real documents describing this repository.
- An adoption step that turns a copy of this repository into the starting point of another project ([`AGENTS.md` §8](AGENTS.md#8-adopting-this-repository)).

**Deliberately does not** (*declared*):

- Sync anything to the repositories already created: each receives a copy once, and an improvement made here later does not reach them ([ADR-004](ARCHITECTURE.md#adr-004-a-github-template-repository-copied-once)).
- Use an organisation `.github` repository to share `SECURITY.md`, `CONTRIBUTING.md` or the like.
- Ship issue templates, a pull request template or custom labels.
- Contain product code.

## 4. Principles

*Instruction: the product principles behind the decisions, each in one sentence.*

- **One home per fact.** A fact is written in exactly one document; the others reference it by section (*declared*).
- **Documents describe the present.** If it is in a document, it is true now; the future lives in issues (*declared*).
- **The agent reads the same documents a person does.** There is no separate, larger body of instructions for agents: `AGENTS.md` is a map and a short list of rules pointing at the documents a person reads (*declared*).
- **Small and loaded always beats complete and loaded never.** What an agent reads in every session is kept short, and the rest is opened at the section that answers the question (*inferred* from the size of the main repository's `CLAUDE.md`; **To confirm** when the main repository migrates).

## 5. Ubiquitous language

*Instruction: the terms of the product, each with the meaning it has here and nowhere else.*

| Term | Meaning |
|---|---|
| **`memorysmithapp-template`** | This repository, always by its full name. *Template* alone is a term of the MemorySmith product (the shape of the notes of a folder), so the repository is never called "the template" |
| **Created repository** | A repository made from this one with *Use this template* or `gh repo create --template`, holding a copy of its files in one initial commit and no link back |
| **Instance** | A repository whose documents describe itself under the structure of this one. This repository is the first instance; every adopted repository is another |
| **Adoption** | The first session of a created repository, which rewrites what is the project's own and keeps the process ([`AGENTS.md` §8](AGENTS.md#8-adopting-this-repository)) |
| **Kept section** | A section a created repository keeps as it is on adoption |
| **Rewritten section** | A section a created repository rewrites with its own project's content on adoption, keeping the heading |
| **Owner** | The owner of the `memorysmithapp` organisation, who decides, reviews and merges |
| **Cycle** | The work of one version, on the branch `release/vX.Y.Z`, closed by one pull request |

## 6. Journeys

*Instruction: the paths a member of the audience follows through the product, step by step.*

**Creating a repository from it.** The owner creates the repository with *Use this template* or `gh repo create memorysmithapp/<name> --template memorysmithapp/memorysmithapp-template --public --clone`, and receives these files in one initial commit.

**Adopting it in the first session.** A Claude Code session opened at the root of the created repository loads `AGENTS.md` through `CLAUDE.md`, finds §8 *Adopting this repository*, and on the branch `release/v0.1.0` rewrites the identity, empties `PRD.md` and `ARCHITECTURE.md` to their skeletons, resets the version and the changelog, keeps `SDLC.md` and the rules, and deletes §8.

**A later session working under it.** A session in any instance starts with `AGENTS.md` loaded, follows the reading map to the section it needs, works an issue on the branch of the cycle under `SDLC.md`, writes each paragraph where the writing map says, and runs the checklist of `AGENTS.md` §7 before calling the work done.

## 7. Features and rules

*Instruction: what the product provides, as business rules with codes `RN-{AREA}-{NNN}`.*

Codes are append-only: never renumbered, never reused. A rule that stops holding stays on its own line, marked **Removed** with the version and the reason. Areas: `DOC` (documents), `VER` (version and changelog), `REP` (repository settings), `ADO` (adoption).

| Code | Rule | Status |
|---|---|---|
| RN-DOC-001 | A repository holds `CLAUDE.md`, `AGENTS.md`, `PRD.md`, `ARCHITECTURE.md`, `SDLC.md`, `README.md` and `CHANGELOG.md`, each answering one question: how Claude Code reaches the instructions; how an agent works here; what the product solves and delivers; how it is organised and why; how a change travels to production; what this is and how to start; what changed and when | declared |
| RN-DOC-002 | `CLAUDE.md` is exactly the line `@AGENTS.md`, so Claude Code imports the instructions in every session and sub-agent | declared; the import observed in a fresh session (#2) |
| RN-DOC-003 | Every section of `AGENTS.md`, `PRD.md`, `ARCHITECTURE.md` and `SDLC.md` says whether it is kept or rewritten on adoption | declared |
| RN-DOC-004 | Each fact has one home; `AGENTS.md` keeps the writing map that says where a new paragraph goes | declared |
| RN-DOC-005 | A document describes only what is true now, and carries no version notes, revision dates or "internal document" footers | declared |
| RN-DOC-006 | `PRD.md` and `ARCHITECTURE.md` mark the status of every claim that is not obvious, and **To confirm** what was not verified | declared |
| RN-DOC-007 | Everything in the repository is written in American English (en-US) | declared |
| RN-VER-001 | The version lives in the `version` field of the root `package.json`, and nowhere else | declared |
| RN-VER-002 | `CHANGELOG.md` follows Keep a Changelog 1.1.0: `[Unreleased]` on top, its categories only, compare links at the foot | declared |
| RN-REP-001 | `scripts/setup-repo.sh` applies to a created repository what a copy does not carry: the description and topics, merge, squash and rebase allowed, wiki and discussions off, and the ruleset `main` on the default branch (no deletion, no force push, changes only through a pull request with 0 required approvals, no bypass actors); labels stay GitHub's defaults | declared; the ruleset it creates *observed* identical to this repository's (#7) |
| RN-REP-002 | `scripts/setup-repo.sh` is idempotent, reports what it changed and what was in place, and fails loudly on a missing argument, tool or permission | declared; *observed* on a throwaway repository (#7) |
| RN-ADO-001 | `AGENTS.md` §8 says what the first session of a created repository rewrites, empties, resets, keeps and deletes, `scripts/setup-repo.sh` included | declared |

## 8. Quality requirements

*Instruction: the measurable qualities the product holds, each with its threshold.*

| Code | Requirement | Threshold | Status |
|---|---|---|---|
| QR-001 | `AGENTS.md` is loaded whole in every session, so it stays short | Under about 2,000 words | declared; 1,111 words *observed* at #2 |
| QR-002 | A person who never saw the repository can create one from it with the `README.md` alone | No step outside the README | declared |

## 9. Acceptance criteria

*Instruction: how each rule is checked, by its code.*

| Rule | The rule holds when |
|---|---|
| RN-DOC-001 | Each of the seven files exists at the root, and its opening paragraph states the question it answers |
| RN-DOC-002 | `CLAUDE.md` is byte for byte `@AGENTS.md` and a newline, and a fresh Claude Code session at the root shows `AGENTS.md` in its context without reading a file |
| RN-DOC-003 | Every top-level section of the four documents carries an italic *Kept* or *Rewritten* line, or the document states it once for all of its sections |
| RN-DOC-004 | `AGENTS.md` §3 has a row for each document and the boundary cases |
| RN-DOC-005 | No document has a line starting with a revision note or an "internal document" footer; plans live in issues |
| RN-DOC-006 | Non-obvious claims in `PRD.md` and `ARCHITECTURE.md` carry *observed*, *declared* or *inferred* |
| RN-DOC-007 | The repository's text, commits, branches, issues and PRs are in en-US |
| RN-VER-001 | `version` appears in the root `package.json` and in no document |
| RN-VER-002 | `CHANGELOG.md` opens with `[Unreleased]`, uses only Keep a Changelog categories, and has a link definition for every section |
| RN-REP-001 | After a run, `gh api repos/<r>/rulesets/<id>` returns the same ruleset as this repository's, except identifiers and timestamps |
| RN-REP-002 | A second run reports nothing changed; a run without its three arguments, without `gh` or `jq`, or without administrator rights exits non-zero with the reason |
| RN-ADO-001 | Following `AGENTS.md` §8 in a created repository yields a coherent repository empty of this one's content, with the process intact |
