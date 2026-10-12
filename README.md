# memorysmithapp-template

The starting point of every new repository of the [`memorysmithapp`](https://github.com/memorysmithapp) organisation. It carries no product code: it carries the documents humans and agents work by — how an agent works here, what the product delivers, how it is organised, how a change travels to a release — so that a new repository starts with its process already written. It is its own first instance: its documents describe this repository, and a new repository rewrites the parts that are its own and keeps the process.

## Create a repository from it

You need a GitHub account with permission to create repositories in the organisation, and, for the command line, the [GitHub CLI](https://cli.github.com/) authenticated (`gh auth login`).

Either press **Use this template → Create a new repository** on this repository's page on GitHub, or run:

```sh
gh repo create memorysmithapp/<name> --template memorysmithapp/memorysmithapp-template --public --clone
```

The new repository receives a copy of these files in one initial commit, and keeps no link to this one: an improvement made here later does not reach it.

## Adopt it in the first session

Open a [Claude Code](https://claude.com/claude-code) session at the root of the new repository. `CLAUDE.md` imports `AGENTS.md`, so the session starts with the instructions loaded. Ask it to adopt the repository: it follows [`AGENTS.md` §8](AGENTS.md#8-adopting-this-repository), on the branch `release/v0.1.0`, rewriting the identity, emptying `PRD.md` and `ARCHITECTURE.md` down to their skeletons, resetting the version and the changelog, and keeping `SDLC.md` and the rules.

## The documents

| Document | Answers |
|---|---|
| [`AGENTS.md`](AGENTS.md) (imported by [`CLAUDE.md`](CLAUDE.md)) | How an agent works here |
| [`PRD.md`](PRD.md) | What the product solves and delivers, under which rule |
| [`ARCHITECTURE.md`](ARCHITECTURE.md) | How the repository is organised, and why |
| [`SDLC.md`](SDLC.md) | How a change travels from an issue to a release |
| [`CHANGELOG.md`](CHANGELOG.md) | What changed in each version |

The version lives in the `version` field of [`package.json`](package.json).

## Licence

[MIT](LICENSE).
