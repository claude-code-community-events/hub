# Claude Code Community Events Hub

Public repo for Claude Code community event organizers to share event materials.

**Org:** `claude-code-community-events`
**Repo:** `hub`
**License:** MIT

---

## Verification Flow

The system uses Luma as the source of truth. No manual approval, no org membership required.

### Trust Chain

1. The event is listed on the `luma.com/claudecommunity` (Claude Community calendar) with the event leader as a host
2. **Event leader** adds GitHub usernames of speakers/contributors in the Luma event description (prefixed with `@`, e.g. `@nfrith`). Only the event description counts.
3. **Speaker** runs `/add-event-material` in Claude Code, or manually creates their folder following CONTRIBUTING.md
4. **Speaker** opens a PR. The Claude Code Action runs `/validate-pr` to verify the contributor against the Luma event page.

### Automated Validation (GitHub Action)

On every PR, the `/validate-pr` skill:
1. Extracts the Luma URL from the event README (must be `lu.ma` or `luma.com` — no other domains)
2. Curls the Luma page and extracts the event description, date, and city
3. Verifies the PR author's `@username` exists in the event description
4. Cross-references the Luma event date and city against the folder path
5. Enforces file permission rules (loose or strict mode depending on whether the description maps usernames to roles)
6. Validates folder structure and file sizes (2MB limit)

See `.claude/skills/validate-pr/SKILL.md` for the full rule set.

### Outcomes
- **All checks pass** → PR labeled `verified`, ready for merge
- **Check fails** → bot comments explaining which check failed and how to fix

---

## Repo Structure

```
hub/
├── events/
│   └── YYYY/
│       └── MM/
│           └── YYYY-MM-DD-city/
│               ├── README.md
│               └── speakers/
│                   └── speaker-name/    # contributor's sandbox
│                       └── (whatever they want)
├── plugin/                  # Marketplace plugin for non-cloners
├── docs/                    # Diagrams, visual docs
├── .claude/
│   └── skills/              # Skills (validate-pr, add-event-material)
├── .github/
│   ├── workflows/           # CI + Claude Code Action
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── CODEOWNERS
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── LICENSE
├── CLAUDE.md
└── README.md
```

### Folder Naming

- Events: `events/YYYY/MM/YYYY-MM-DD-city` (year/month nesting for scale)
- Speaker folders: lowercase, hyphenated name (e.g., `nick-frith`)

---

## Governance

- **Admins** (2-3): Org-level admin.
- **Leaders** (event leaders): Write access to repo. Review PRs for their events.
- **External contributors** (speakers): Fork + PR. No org membership needed. Validated via Luma.

### Branch Protection (main)
- Require pull request before merging
- Require 1 approval
- Require status checks to pass
- No direct pushes

### CODEOWNERS
- Root-level files, `.github/`, `.claude/`, `plugin/`, `docs/` → `@claude-code-community-events/admins`
- `events/` → `@claude-code-community-events/leaders`

---

## Large Files

Git LFS for media. `.gitattributes` tracks: pdf, pptx, key, png, jpg, jpeg, gif, mp4, mov, zip.

Guidelines:
- All files: max 2MB
- Videos/recordings: link only (YouTube, etc). Never commit video files.
- Slides: PDF preferred (smaller than PPTX/Keynote)
