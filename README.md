# fabcrowd/skills

Shared **Cursor** skills, agents, rules, and references for Fabcrowd projects. Clone this repo and sync into a project’s `.cursor/` folder (works with repos that include `scripts/sync_fabcrowd_skills.ps1` / `.sh`).

## Layout

| This repo | After sync → project `.cursor/` |
|-----------|----------------------------------|
| `skills/<skill-id>/SKILL.md` | `skills/<skill-id>/SKILL.md` |
| `agents/*.md` | `agents/` |
| `rules/*.mdc` | `rules/` |
| `references/*` | `references/` |

## Sync into tradingbot (or another repo)

From the **project** root (where `scripts/sync_fabcrowd_skills.*` exists):

```powershell
$env:FABSKILLS_REPO = "C:\path\to\skills"   # this clone
.\scripts\sync_fabcrowd_skills.ps1
```

```bash
export FABSKILLS_REPO=/path/to/skills
./scripts/sync_fabcrowd_skills.sh
```

Then open the project in **Cursor**.

## Contents (initial import)

**Skills**

- `proposed-changes-pnl-test` — structural P&L / deploy A/B vs baseline
- `tradingview-extract` — TradingView / pine-facade parameter extract

**Agents**

- `awesome-deep-research-agent` — deep-research landscape specialist

**Rules**

- `scope-guard` — plan-mode / feature creep guard

**References**

- `claude-skill-design-methodology` — skill authoring notes

## Contributing

Add a folder under `skills/<name>/SKILL.md` following [Cursor Agent Skills](https://cursor.com/docs) conventions. Open a PR or push to `main` if you maintain the org.
