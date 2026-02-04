---
name: add-event-material
description: >-
  This skill should be used when the user asks to "add event material",
  "submit my slides", "add my talk", "contribute to an event",
  "upload my presentation", "add speaker material", "submit event assets",
  "link my talk repo", "add materials to the event",
  or invokes /add-event-material. Guides speakers and event
  hosts through contributing materials to the Claude Code Community Events hub.
disable-model-invocation: true
user-invocable: true
version: 0.1.0
---

# Add Event Material

Interactive workflow for contributing materials to the Claude Code Community Events hub repo. Handles both speakers submitting talk materials and event hosts submitting event-level assets.

## Workflow

### Step 1: Determine Role

Ask the contributor:

> Are you a **speaker** adding your talk materials, or an **event host** adding event-level assets (photos, recordings, event summary)?

This affects which files get created, but the folder structure is the same.

### Step 2: Get Event Information

Ask for the Luma event URL (e.g., `https://lu.ma/abc123`).

Fetch the Luma event page using WebFetch to extract:
- **Event date** (YYYY-MM-DD format)
- **City name** (lowercase, hyphenated)
- **Event title**

If WebFetch fails or the page doesn't load, check if the contributor has a browser MCP tool available (e.g., Chrome extension) and use that to navigate to the Luma page and extract the information. If no browser tool is available either, ask the contributor to take a screenshot of the Luma event page and submit it so the event details can be read from the image.

Construct the event folder path: `events/YYYY/MM/YYYY-MM-DD-city/`

### Step 3: Get Contributor Name

Ask for the contributor's name. Convert to lowercase hyphenated format for the folder name (e.g., "Nick Frith" becomes `nick-frith`).

### Step 4: Determine Material Type

Ask how the contributor wants to share their materials:

1. **Upload materials directly** — slides, code, notes go into their folder in this repo
2. **Link to external repo** — create a CLAUDE.md pointing to their own repository
3. **Both** — some materials here plus a pointer to an external repo

### Step 5: Scaffold the Folder Structure

Check if the event folder already exists. If not, create it with the event README.

Create the contributor's speaker folder: `events/YYYY/MM/YYYY-MM-DD-city/speakers/contributor-name/`

**If uploading materials (option 1 or 3):**
- Create `README.md` in the speaker folder using the speaker template from `assets/speaker-readme-template.md`
- Pre-fill with the contributor's name, talk title, and event info

**If linking to external repo (option 2 or 3):**
- Create `CLAUDE.md` in the speaker folder with the repo URL, a description of what's in the repo, and instructions for how to use it
- Format the CLAUDE.md so that Claude Code will understand the pointer when someone opens this folder

**If event host creating the event folder:**
- Create or update the event `README.md` using the template from `assets/event-readme-template.md`
- Pre-fill with event details extracted from the Luma page

### Step 6: Guide Content Addition

For speakers uploading materials, guide them through adding:
- **Talk title and description** in their README.md
- **Slides** (PDF preferred, compress to < 2MB)
- **Demo code** (any structure they want)
- **Links** to recordings, blog posts, related repos

Remind contributors:
- Their speaker folder is their sandbox — organize however they like
- Photos: compress, max 2MB each
- Videos/recordings: link only (YouTube, etc). Never commit video files.
- Slides: PDF preferred (smaller than PPTX/Keynote)
- No file over 50MB
- Binary files are tracked by Git LFS

### Step 7: Verify and Summarize

Confirm what was created. Remind the contributor to:
- Review the generated files
- Open a PR when ready
- Ensure their GitHub username appears somewhere in the Luma event page (the automated validation checks this)

## Event Folder Naming Convention

Pattern: `events/YYYY/MM/YYYY-MM-DD-city/`

Examples:
- `events/2026/02/2026-02-07-chiang-mai/`
- `events/2026/01/2026-01-15-new-york/`
- `events/2025/12/2025-12-10-san-francisco/`

Cities are lowercase, hyphenated. Date matches the Luma event date.

## Templates

Event README template: `assets/event-readme-template.md`
Speaker README template: `assets/speaker-readme-template.md`

Read and use these templates when scaffolding folders. Pre-fill fields with information gathered from the contributor and the Luma event page.

## External Repo Pointer (CLAUDE.md)

When a speaker links to an external repo instead of uploading materials, create a `CLAUDE.md` in their speaker folder using the template from `assets/external-repo-template.md`. Pre-fill with the speaker's name, talk title, repo URL, and description.

This file serves as a pointer so that anyone browsing the hub repo (or using Claude Code) can discover and navigate to the speaker's external materials.
