# Claude Code Community Events Hub

Shared resources, event materials, and tools for Claude Code community event leaders worldwide.

## How It Works

```
Anthropic creates event       Event leader adds GitHub       Speaker runs /add-event-material
on Luma Community calendar    IDs anywhere in event page     in Claude Code or Cowork
        |                              |                              |
        v                              v                              v
  [luma.com/claudecommunity]    [Luma event description]       [Opens PR to this repo]
                                                                      |
                                                                      v
                                                          +-----------------------+
                                                          | Automated Validation  |
                                                          +-----------------------+
                                                          | 1. Extract event from |
                                                          |    PR path            |
                                                          | 2. Match on Luma      |
                                                          |    calendar           |
                                                          | 3. Verify "Claude     |
                                                          |    Community" host    |
                                                          | 4. Check PR author's  |
                                                          |    GitHub ID in event |
                                                          | 5. Validate structure |
                                                          | 6. Claude Code Action |
                                                          |    reviews content    |
                                                          +-----------------------+
                                                                |             |
                                                                v             v
                                                         [verified]    [needs-verification]
                                                          auto-merge    bot explains fix
```

## Verification System

No manual approval. No org membership required. No issue-first workflow.

The trust chain is:

1. **Anthropic** creates the event on the [Claude Community calendar](https://luma.com/claudecommunity) and adds the event leader as a host
2. **Event leader** adds speaker/contributor GitHub usernames anywhere in the Luma event page (description, schedule, speaker bios — the validation scans the entire event)
3. **Speaker** opens Claude Code or Cowork, runs `/add-event-material`, provides their Luma event URL, and submits a PR
4. **GitHub Action** validates the PR automatically against the Luma event — no human review needed for verification

See [docs/verification-flow.html](docs/verification-flow.html) for a visual diagram of the system.

## Repo Structure

```
events/YYYY/MM/YYYY-MM-DD-city/     # one folder per event
├── README.md                        # event metadata, hosts, links
└── speakers/
    └── your-name/                   # your sandbox — put whatever you want
```

Events organized by year/month for scale. Speaker folders are black boxes — your space, your structure.

## Quick Start

**With Claude Code or Cowork:**
```
/add-event-material
```

**Manual:** See [CONTRIBUTING.md](CONTRIBUTING.md).

**CLI scaffolding:**
```bash
./scripts/new-event.sh --date 2026-02-07 --city chiang-mai --speakers "Nick Frith" "Ian Borders"
```

## License

MIT
