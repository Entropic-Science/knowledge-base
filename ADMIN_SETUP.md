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

### 3. Create the `admins` team on GitHub

Go to **github.com/orgs/Entropic-Science/teams** and create a team called `admins` with the three founders:
- @jordanmmck
- @kluck77 (or @alchemystack)
- @orphiceye

This team is referenced in `CODEOWNERS`. Without it, CODEOWNERS rules won't activate.

### 4. Enable branch protection on `main`

Go to **Settings > Branches > Add branch ruleset** (or classic branch protection) for `main`:

- [x] **Require a pull request before merging**
  - [x] Require approvals: **1**
  - [x] Require review from Code Owners
- [x] **Require status checks to pass** (optional, no CI yet)
- [ ] Do NOT enable "Restrict who can push" — we want anyone with write access to create PRs

This is the key step. Without branch protection + "Require review from Code Owners", the CODEOWNERS file has no effect — it's just a comment.

### 5. Set repository permissions

Go to **Settings > Collaborators and teams**:

- `admins` team → **Admin** role
- For community members: either add individually with **Write** access, or create a `contributors` team with **Write** access and add people to that

**Write access** lets people:
- Create branches and PRs
- Approve PRs (for community-editable files)
- Cannot merge PRs that touch admin-controlled files without admin approval

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

**"Admin can't merge without review"** — Admins can bypass branch protection by default. If you want even admins to need reviews, enable "Do not allow bypassing the above settings" in branch protection. Recommended to leave bypass enabled for admins during initial setup.
