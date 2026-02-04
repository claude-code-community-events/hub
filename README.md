# Claude Code Community Events Hub

Shared resources and event materials for Claude Code community event leaders worldwide.

## How It Works

1. **Anthropic** creates the event on the [Claude Community calendar](https://luma.com/claudecommunity)
2. **Event leader** adds speaker GitHub usernames (e.g., `@nfrith`) in the Luma event description
3. **Speaker** runs `/add-event-material` in Claude Code or Cowork, provides the Luma URL, and opens a PR
4. **GitHub Action** validates the PR automatically — checks the contributor's `@username` is in the Luma event description

No manual approval. No org membership required.

## Repo Structure

```
events/YYYY/MM/YYYY-MM-DD-city/     # one folder per event
├── README.md                        # event metadata, hosts, links
└── speakers/
    └── github-username/             # your sandbox — put whatever you want
```

Events organized by year/month for scale. Speaker folders are your space, your structure.

## Quick Start

**With Claude Code or Cowork:**
```
/add-event-material
```

**Manual:** See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT
