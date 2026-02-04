# Contributing

## Add Your Event Materials

### Option A: Use the skill (recommended)

In Claude Code or Cowork, run:

```
/add-event-material
```

The skill asks for your Luma event URL and your name, scaffolds the folder, and guides you through adding your content.

### Option B: Manual

1. Fork this repo
2. Create your event folder (if it doesn't exist): `events/YYYY/MM/YYYY-MM-DD-city/`
3. Add your speaker folder: `events/YYYY/MM/YYYY-MM-DD-city/speakers/your-name/`
4. Add a `README.md` to your folder (talk title, description, links to materials)
5. Add your materials — slides, code, notes, whatever you want
6. Open a PR

The automated validation verifies your GitHub ID appears in the Luma event page. No manual approval needed.

## Add Yourself to an Existing Event

If the event folder already exists:

1. Fork the repo
2. Create your subfolder: `events/YYYY/MM/YYYY-MM-DD-city/speakers/your-github-username/`
3. Add a `README.md` to your folder (talk title, description, links to materials)
4. Add your materials
5. Open a PR

## Naming Conventions

- Event folders: `YYYY-MM-DD-city` (lowercase, hyphenated)
- Speaker folders: your name (lowercase, hyphenated, e.g., `nick-frith`)
- Cities: lowercase, hyphenated (e.g., `chiang-mai`, `new-york`, `san-francisco`)

## File Guidelines

- **Photos:** Compress to < 2MB each. Link to an album if you have many.
- **Videos/recordings:** Link only (YouTube, etc). Never commit video files.
- **Slides:** PDF preferred (smaller than PPTX/Keynote).
- **No file over 50MB.** Files over 5MB will trigger a warning.

Binary files (pdf, pptx, key, png, jpg, jpeg, gif, mp4, mov, zip) are tracked by Git LFS.

## Folder Structure

```
events/
  YYYY/
    MM/
      YYYY-MM-DD-city/
        README.md              # event metadata
        speakers/
          contributor-name/    # your sandbox - put whatever you want here
            README.md          # about you and your talk
            ...
```

Within your speaker folder, you can organize however you like. It's your sandbox.

## PR Checklist

See the [PR template](.github/PULL_REQUEST_TEMPLATE.md) for the full checklist.
