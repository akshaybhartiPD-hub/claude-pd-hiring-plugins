# ParallelDots Hiring — Claude plugin marketplace

This repository is a Claude plugin marketplace that distributes the **pm-interview-evaluator**
skill to the team, so `/pm-interview-evaluator` resolves for everyone who installs it — instead
of the `Unknown skill` error you get when a skill is only shared through a project.

## What's inside

```
paralleldots-hiring-marketplace/
├── .claude-plugin/
│   └── marketplace.json                     # the catalog (marketplace name: paralleldots-hiring)
└── plugins/
    └── pm-interview-evaluator/
        ├── .claude-plugin/
        │   └── plugin.json                  # plugin manifest (v1.0.0)
        └── skills/
            └── pm-interview-evaluator/
                ├── SKILL.md
                └── assets/                  # case studies + HTML report/question templates
```

## Publish it (one-time, done by the owner)

Host the marketplace in a git repo so teammates get versioning and automatic updates.

1. Create a repo, e.g. `paralleldots/paralleldots-hiring-marketplace`.
2. Copy the **contents** of this folder into the repo root, so that `.claude-plugin/marketplace.json`
   sits at the repository root.
3. Commit and push:

   ```bash
   git init
   git add .
   git commit -m "Add ParallelDots hiring marketplace + pm-interview-evaluator plugin"
   git branch -M main
   git remote add origin https://github.com/paralleldots/paralleldots-hiring-marketplace.git
   git push -u origin main
   ```

A private repo works fine — teammates just need read access (see Anthropic's docs on
private-repo auth for background auto-updates).

## Install it (each teammate, once)

```
/plugin marketplace add paralleldots/paralleldots-hiring-marketplace
/plugin install pm-interview-evaluator@paralleldots-hiring
```

Then invoke it as `/pm-interview-evaluator` (or `/pm-interview-evaluator:pm-interview-evaluator`
if a name collision ever occurs). To enable it automatically for everyone who trusts the project,
add the marketplace to `.claude/settings.json` via `extraKnownMarketplaces` + `enabledPlugins`.

## Update it later

Bump `version` in **both** `marketplace.json` and `plugin.json` (keep them equal), push, and
teammates run `/plugin marketplace update paralleldots-hiring`. If you omit `version`, every new
commit is treated as a new version automatically.

## Validate before sharing

```bash
claude plugin validate .
```

## Note on PDF output

The skill builds its PDFs with `wkhtmltopdf`. Make sure each user's environment has it available,
or the final export step will fail even though the skill loads correctly.
