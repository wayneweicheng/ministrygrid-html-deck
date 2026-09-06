# Ministry Grid HTML Deck

Codex skill for turning an authenticated Lifeway Ministry Grid curriculum, session, or issue page into a kid-friendly, interactive HTML teaching deck.

## Contents

- `SKILL.md` — workflow, source-review gate, content rules, and validation requirements
- `references/deck-architecture.md` — timing, slide structure, interaction, and file-contract guidance
- `agents/openai.yaml` — Codex skill metadata

## Use

Invoke the skill with a valid `ministrygrid.lifeway.com` curriculum/session/issue URL. The skill reviews the authenticated lesson, proposes a teaching plan for confirmation, and then creates an offline-friendly deck at `/Users/wayne/Repo/github/commercial/ministrygrid-html-deck/generated-html-dek/<lesson-slug>/index.html`, with its README and assets kept in the same lesson folder.

The source lesson must be accessible in the authenticated browser session. Optional source videos are not copied into a deck by default.
