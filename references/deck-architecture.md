# HTML deck architecture

Use this reference after the user confirms the proposal and before writing the deck.

## Timing

For a 10-minute teaching block, target 8–10 slides and roughly 45–75 seconds per story slide. Allow the teacher to pause on a visual, ask one prediction question, and then reveal the answer without changing slides. Reserve the last slide or two for the separate 5-minute question period.

## Recommended structure

| Slide | Purpose | On-screen pattern |
|---|---|---|
| 1 | Curiosity hook | Big title, one surprising question, friendly illustration |
| 2 | Setting | Place/time in one sentence, simple map/object/scene |
| 3–5 | Story beats | One event per slide, expressive cartoon, one reveal bubble |
| 6 | Meaning | Short “This shows…” statement tied to the passage |
| 7 | Gospel connection | Story point, Christ connection, or salvation link |
| 8 | Memory anchor | Big-picture answer and/or short key-passage excerpt |
| 9 | Questions | Three or four discussion prompts with answer reveals |

Combine or omit rows when the source content does not support them. The teacher's spoken explanation supplies detail; the screen should supply focus and memory.

## Visual system

- Use a warm, child-friendly palette with strong text contrast: deep teal ink for body text, a gold accent for questions and progress, green for answer cards, rose for emphasis, and cream as the main surface.
- Follow the established poster-led layout: a centered 16:9 `.stage-shell`/`.stage`, a hero slide with large copy and angled artwork, alternating split copy/art slides, rounded cards, a truth/memory slide, and a four-card discussion slide. Keep generous margins and one dominant visual per slide. Treat `generated-html-dek/jesus-saves-us-to-follow-him/index.html` as the visual reference, copying its structure and styling pattern rather than its lesson content.
- Keep one coherent style system and a single primary stylesheet; do not append competing CSS override layers. Use rounded cards and soft shadows sparingly. Avoid busy patterns behind text.
- Use local assets and `object-fit: cover`/`contain` intentionally. Give every meaningful image useful alt text and explicit dimensions; mark decorative shapes `aria-hidden="true"`.
- When a source story poster or illustration exists, store it in the lesson's `assets/` directory and use it as the main visual in the hero and rounded `.art-panel` elements. Reuse the asset with deliberate `object-position` crops for different story beats, as in the established deck. If no suitable source visual exists, create 3–4 distinct local illustrations instead.
- Prefer friendly, expressive illustrated scenes with clear silhouettes and diverse, non-caricatured children. Avoid CSS-only character stickers, generic geometric scenes, or busy decorative overlays that compete with the source artwork. Do not make a generated image look like a real identifiable person.
- Use short, colorful reveal buttons and speech/thought-style bubbles sparingly. Bubbles may show a source-supported short line or an explicitly labeled wondering prompt, but must not invent biblical dialogue.

## Interaction contract

Use a semantic button for each reveal:

```html
<button class="bubble-toggle" aria-expanded="false" aria-controls="reveal-1">
  What do you notice?
</button>
<div id="reveal-1" class="bubble-pop" hidden>
  The short answer or clue appears here.
</div>
```

The script should:

- toggle `hidden`, an open class, and `aria-expanded` on click;
- support Enter and Space through the native button behavior;
- support hover as a convenience only, never as the sole reveal path;
- close or reset stale reveals when changing slides unless the approved design says otherwise;
- keep the reveal within the viewport at TV scale;
- avoid rapid animation and respect `prefers-reduced-motion`.

Controls should be at least 44px by 44px, with 48px preferred, and should set `touch-action: manipulation`. Check actual text and background colors for WCAG AA contrast; white small text on rose is not acceptable below 4.5:1. Replace decorative Unicode interface symbols with small inline SVG icons, and label icon-only buttons for assistive technology.

Navigation should use semantic buttons plus keyboard listeners. Recommended keys are `ArrowLeft`, `ArrowRight`, `Home`, `End`, and `Space`; do not intercept typing inside a focused form control.

Navigation should also:

- read and write a hash in the form `#slide=N`;
- handle initial load, `hashchange`, browser back/forward, and invalid values by clamping to the available slide range;
- move focus to the active slide heading after navigation; and
- update a polite `aria-live` region with the current position, for example "Slide 6 of 9."

An optional presenter mode may be enabled with a documented local control or URL flag. It must be off by default, keep pacing notes, Bible references, and activity suggestions out of the TV-facing slide, and never make the children's view depend on presenter-only content.

## Content and question design

Use the Bible passage as the anchor, then paraphrase the leader guide. A question should make a child point to something visible, remember a story beat, or connect the story to the lesson's big idea. Good question cards have a short answer cue hidden behind the reveal; they do not become a quiz show with pressure to perform.

Aim for:

- one observation question;
- one meaning question;
- one personal application question;
- one big-picture or Christ-connection question when appropriate.

Keep the answer cue accurate but brief. If an answer requires nuance, put the nuance in the teacher's private notes or a small reveal rather than crowding the prompt.

## File contract

The generated output should contain:

- `<lesson-slug>/index.html` as the entry point;
- `<lesson-slug>/README.md` with source and launch notes;
- `<lesson-slug>/assets/` for lesson-specific supporting assets, with stable relative paths;
- an optional `README.md` containing the lesson source, date reviewed, and launch instructions;
- no credentials, browser profile data, raw cookies, or unnecessary large media files.

Do not use absolute machine-specific paths in HTML. Keep generated art and extracted source visuals separate when that helps the teacher understand provenance.
