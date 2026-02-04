# Claude Code Community Events Hub

Public repo for Claude Code community event leaders to share event materials, tools, and code.

**Org:** `claude-code-community-events`
**Repo:** `hub`
**License:** MIT
**Plan:** GitHub Free (public repo)

---

## Verification Flow

The system uses Luma as the source of truth. No manual approval, no org membership, no issue-first workflow.

### Trust Chain

1. **Anthropic** creates the event on `luma.com/claudecommunity` (Claude Community calendar) and adds the event leader as a host
2. **Event leader** adds GitHub usernames of speakers/contributors anywhere in the Luma event page — description, schedule, speaker bios. The automated validation scans the entire event page.
3. **Speaker** runs `/add-event-material` in Claude Code or Cowork. The skill asks for the Luma event URL, scaffolds the correct folder, and guides the contributor through adding content.
4. **Speaker** opens a PR. The PR path (e.g., `events/2026/02/2026-02-27-miami/`) tells the system which Luma event to validate against.

### Automated Validation (GitHub Action)

On every PR:
1. Extract event date + city from PR path
2. Find matching event on Luma calendar via API
3. Verify "Claude Community" is in Hosted By
4. Check PR author's GitHub ID exists anywhere in the Luma event page
5. Validate folder structure + file sizes
6. Claude Code Action reviews content quality (spam, promo, structure)

### Outcomes
- **All checks pass** → PR labeled `verified`, auto-merge or admin merge
- **Check fails** → PR labeled `needs-verification`, bot comments explaining which check failed and how to fix

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
│                   └── speaker-name/    # black box — contributor's sandbox
│                       └── (whatever they want)
├── tools/                    # Shared community tools
├── templates/                # Copy-paste starters
├── scripts/                  # CLI scaffolding tools
├── docs/                     # Diagrams, visual docs
├── .github/
│   ├── workflows/            # CI + Claude Code Action
│   ├── ISSUE_TEMPLATE/
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── CODEOWNERS
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── LICENSE
├── CLAUDE.md
└── README.md
```

### Folder Naming

- Events: `events/YYYY/MM/YYYY-MM-DD-city` (year/month nesting for scale — ~30 events/month)
- Speaker folders: lowercase, hyphenated name (e.g., `nick-frith`)
- Tools: `tools/tool-name/`

---

## Governance

- **Owners** (2-3): Nick + Anthropic rep. Org-level admin.
- **Members** (event leaders): Write access to repo. Review PRs for their events.
- **External contributors** (speakers): Fork + PR. No org membership needed. Validated via Luma.

### Branch Protection (main)
- Require pull request before merging
- Require 1 approval
- Require status checks to pass
- No direct pushes

### CODEOWNERS
- Root-level files, .github/, templates/, scripts/ → `@claude-code-community-events/admins`
- tools/ → `@claude-code-community-events/admins`
- events/ → `@claude-code-community-events/leaders`

---

## Large Files

Git LFS for media. `.gitattributes` tracks: pdf, pptx, key, png, jpg, jpeg, gif, mp4, mov, zip.

Guidelines:
- Photos: compress, max 2MB each, link to album if many
- Videos/recordings: link only (YouTube, etc). Never commit video files.
- Slides: PDF preferred (smaller than PPTX/Keynote)
