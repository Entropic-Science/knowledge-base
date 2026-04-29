# Knowledge base

Central hub for Entropic Science community knowledge: shared research, project documentation, division rosters, and proposals.

**GitHub**: [github.com/Entropic-Science](https://github.com/Entropic-Science)
**Discord**: [discord.gg/2EbveaB2wS](https://discord.gg/2EbveaB2wS)
**Community docs**: [community repo](https://github.com/Entropic-Science/community)

## How this repo is organized

```
knowledge-base/
├── library/                          # Shared content — research, projects, writeups
│   ├── research/                     # Research notes, summaries, paper drafts
│   ├── projects/                     # Project documentation and reports
│   └── writeups/                     # Essays, blog drafts, explainers
│
└── divisions/                        # Division boards (one per workstream)
    ├── infrastructure/               # Quantum-random systems infrastructure
    ├── research/                     # Research and evaluation
    └── outreach-fundraising/         # Community outreach and fundraising
```

Each **division** folder contains three documents:

| File | What it's for | Who can edit |
|------|---------------|--------------|
| `ROSTER.md` | Members sign up with their name and current work | Anyone (via PR) |
| `PROPOSALS.md` | New project ideas and proposals | Anyone (via PR) |
| `ACTIVE_PROJECTS.md` | Accepted projects currently being worked on | Division leads and admins only |

## Quick start

### I want to share research, a project writeup, or an essay

1. Pick the right folder under `library/`:
   - `library/research/` — research notes, experiment reports, literature reviews, paper drafts
   - `library/projects/` — documentation for a project you're building or contributing to
   - `library/writeups/` — essays, blog drafts, explainers, opinion pieces
2. Copy the `_TEMPLATE.md` file in that folder
3. Rename it descriptively (e.g., `qrng-latency-benchmarks-2026-04.md`)
4. Fill it in and submit a pull request

### I want to join a division

1. Open the `ROSTER.md` file in the division you want to join (under `divisions/`)
2. Add your entry to the table following the format shown
3. Submit a pull request — a quick review and merge is all that's needed

### I want to propose a new project or idea

1. Open the `PROPOSALS.md` file in the relevant division
2. Add your proposal following the template at the top of the file
3. Submit a pull request
4. Discussion happens in the PR comments and/or on Discord

### I want to update my roster entry

Same as joining — edit your row in `ROSTER.md` and submit a PR. Keep it current: update when you start or finish projects, shift focus, or change availability.

## Access model

This repo uses three access tiers:

### Trusted contributors (direct push)

Members of the `@Entropic-Science/trusted` team can push directly to `main` — no PR or review needed. These are people the admins trust to add and edit content freely. They should still use PRs for admin-controlled files (see below), but this is a social norm, not a technical barrier.

To get trusted access, ask an admin on Discord or during a weekly call.

### Community-editable (open PRs welcome)

Everyone else contributes via pull requests. These files are designed for community members to add to directly:

- All `ROSTER.md` files — sign yourself up, update your projects
- All `PROPOSALS.md` files — propose ideas, anyone can contribute
- Everything under `library/` — share your work

PRs to these files need one approving review from any contributor with write access. The bar is low: if your entry follows the format and is good-faith, it gets merged.

### Admin-controlled (requires admin/lead review)

These files represent decisions and commitments, so changes need sign-off even from trusted contributors:

- All `ACTIVE_PROJECTS.md` files — only updated when proposals are accepted
- `README.md` — this guide
- `CODEOWNERS` — access control definitions

PRs to these files require review from a division lead or admin (defined in `CODEOWNERS`).

## Conventions

- **File names**: lowercase, hyphens, include a date if time-sensitive (e.g., `consciousness-survey-2026-04.md`)
- **One file per piece of work** in the library — don't append to someone else's document
- **Use the templates** — they exist so the library stays navigable
- **Keep roster entries current** — stale entries get cleaned up quarterly
- **Proposals stay open** until explicitly accepted (moved to `ACTIVE_PROJECTS.md`) or withdrawn

## Licensing

All content in this repository is licensed under [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) unless otherwise stated. Code snippets within documents fall under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0).

## See also

- [Charter](https://github.com/Entropic-Science/community/blob/main/CHARTER.md) — mission and scope
- [Contributing guide](https://github.com/Entropic-Science/community/blob/main/CONTRIBUTING.md) — how to participate
- [How we work](https://github.com/Entropic-Science/community/blob/main/HOW_WE_WORK.md) — tools and communication norms
- [Code of conduct](https://github.com/Entropic-Science/community/blob/main/CODE_OF_CONDUCT.md) — behavioral standards
