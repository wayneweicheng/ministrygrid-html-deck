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

- Use a warm, child-friendly palette with strong text contrast: deep ink for body text, a bright accent for questions, and one calm secondary color for answer reveals.
- Keep the stage visually calm: one dominant illustration, at most two supporting shapes, and generous margins.
- Use rounded cards and soft shadows sparingly. Avoid busy patterns behind text.
- Use local assets and `object-fit: cover`/`contain` intentionally. Give every meaningful image useful alt text; mark decorative shapes `aria-hidden="true"`.
- Prefer friendly cartoon scenes with clear silhouettes and diverse, non-caricatured children. Do not make a generated image look like a real identifiable person.

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

Navigation should use semantic buttons plus keyboard listeners. Recommended keys are `ArrowLeft`, `ArrowRight`, `Home`, `End`, and `Space`; do not intercept typing inside a focused form control.

## Content and question design

Use the Bible passage as the anchor, then paraphrase the leader guide. A question should make a child point to something visible, remember a story beat, or connect the story to the lesson's big idea. Good question cards have a short answer cue hidden behind the reveal; they do not become a quiz show with pressure to perform.

Aim for:

- one observation question;
- one meaning question;
- one personal application question;
- one big-picture or Christ-connection question when appropriate.

Keep the answer cue accurate but brief. If an answer requires nuance, put the nuance in the teacher's private notes or a small reveal rather than crowding the prompt.

## File contract

The lesson folder should contain:

- `index.html` as the only required entry point;
- `assets/` for local images, with stable relative paths;
- an optional `README.md` containing the lesson source, date reviewed, and launch instructions;
- no credentials, browser profile data, raw cookies, or unnecessary large media files.

Do not use absolute machine-specific paths in HTML. Keep generated art and extracted source visuals separate when that helps the teacher understand provenance.
