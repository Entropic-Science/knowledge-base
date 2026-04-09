# Admin setup guide

Step-by-step instructions for setting up and maintaining this knowledge base repo. This file is only visible to people who look for it — it's not linked from the main README on purpose.

## Initial setup checklist

### 1. Create the GitHub repo

```bash
gh repo create Entropic-Science/knowledge-base \
  --public \
  --description "Central knowledge base for Entropic Science — research, projects, division boards" \
  --clone
```

Or create it through the GitHub UI under the Entropic-Science org.

### 2. Push this content

```bash
cd knowledge-base
git init
git add .
git commit -m "Set up knowledge base structure"
git remote add origin https://github.com/Entropic-Science/knowledge-base.git
git branch -M main
git push -u origin main
```

### 3. Create teams on GitHub

Go to **github.com/orgs/Entropic-Science/teams** and create two teams:

**`admins`** — the three founders:
- @jordanmmck
- @kluck77 (or @alchemystack)
- @orphiceye

**`trusted`** — people you trust to edit the knowledge base freely (add members as you go):
- Start empty, add people as trust is established

Both teams are referenced in `CODEOWNERS` and branch protection. Without them, access control won't activate.

### 4. Enable branch protection on `main`

Go to **Settings > Rules > Rulesets > New ruleset > New branch ruleset**:

**Basics:**
- Name: `main protection`
- Enforcement: **Active**
- Target: default branch (`main`)

**Bypass actors** (these people can push directly to main without PRs):
- `admins` team — **Always**
- `trusted` team — **Always**

**Rules:**
- [x] **Require a pull request before merging**
  - [x] Required approvals: **1**
  - [x] Require review from Code Owners
- [x] **Require status checks to pass** (optional, no CI yet)
- [ ] Do NOT enable "Block force pushes" unless you want to prevent force-push from admins too

This is the key step. The bypass actors list is what gives trusted contributors direct push access. Without branch protection + "Require review from Code Owners", the CODEOWNERS file has no effect.

> **Classic branch protection alternative**: If using classic branch protection instead of rulesets, go to **Settings > Branches > Add rule** for `main`, enable the same rules, and check **"Allow specified actors to bypass required pull requests"** — then add the `admins` and `trusted` teams.

### 5. Set repository permissions

Go to **Settings > Collaborators and teams**:

- `admins` team → **Admin** role
- `trusted` team → **Write** role (push access; bypass is handled by the ruleset, not the role)
- For regular community members: either add individually with **Write** access, or create a `contributors` team with **Write** access

**The three tiers in practice:**

| Tier | Team | What they can do |
|------|------|------------------|
| Admin | `admins` | Everything — bypass all protection, approve any PR |
| Trusted | `trusted` | Push directly to main (bypass branch protection). Should still use PRs for admin-controlled files (social norm). |
| Contributor | `contributors` or individual Write access | Submit PRs. Community-editable files need 1 review from anyone. Admin-controlled files need admin review. |

### 6. Enable Discussions (optional)

Go to **Settings > Features > Discussions** and enable it. This gives proposals a place for longer-form discussion beyond PR comments.

## Ongoing maintenance

### Quarterly roster cleanup

Once a quarter, review roster files for stale entries (people who haven't been active). Reach out on Discord first, then remove entries with no response after 2 weeks.

### Moving proposals to active projects

When a proposal is accepted (via lazy consensus or council decision per governance tiers):

1. Copy the proposal content from `PROPOSALS.md` to `ACTIVE_PROJECTS.md`
2. Update the status in `PROPOSALS.md` to **Accepted** with a link to the active project entry
3. Assign a lead in the active project entry
4. Do this in a single PR for clean history

### Adding division leads to CODEOWNERS

When workstream leads are assigned, you can give them approval power over their division's `ACTIVE_PROJECTS.md`:

```
# Example: giving a lead control over infra active projects
/divisions/infrastructure/ACTIVE_PROJECTS.md    @Entropic-Science/admins @username
```

### Library housekeeping

The library is self-service, but periodically check for:
- Files without the template frontmatter (title, author, date)
- Duplicate or superseded content (link the newer version, archive the old)
- Content that should move to a project repo instead of living here

## Backup plan

If GitHub goes down or you need to migrate:
- This is a standard git repo — clone it anywhere
- All content is plain markdown — no vendor lock-in
- CODEOWNERS is GitHub-specific but the access model can be replicated on GitLab (also has CODEOWNERS) or via manual review policies elsewhere

## Troubleshooting

**"CODEOWNERS file not working"** — Branch protection must be enabled with "Require review from Code Owners" checked. CODEOWNERS alone does nothing without branch protection.

**"Contributors can't create PRs"** — They need at least **Write** access to the repo (or fork-based workflow, but Write is simpler for a small community).

**"Admin can't merge without review"** — Admins can bypass branch protection by default. If you want even admins to need reviews, remove them from the bypass actors list in the ruleset.

**"Trusted contributor can't push directly"** — Verify: (1) they're in the `trusted` team, (2) the team is listed as a bypass actor in the branch ruleset, (3) the team has at least **Write** role on the repo. All three are required.

**"Trusted contributor pushed to ACTIVE_PROJECTS.md"** — Bypass actors can technically push to any file. CODEOWNERS only enforces reviews on PRs, not direct pushes. If someone pushes to an admin-controlled file directly, git blame shows who did it. Have a conversation — it's a social norm, not a technical gate.
