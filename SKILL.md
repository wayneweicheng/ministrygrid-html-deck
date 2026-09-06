---
name: ministrygrid-html-deck
description: Turn an authenticated Lifeway Ministry Grid curriculum/session/issue page into a kid-friendly, interactive HTML teaching deck. Use when a user supplies a ministrygrid.lifeway.com link and wants the lesson content read, a 10-minute teaching plan proposed for confirmation, and then a TV-ready deck generated under generated-html-deck.
---

# Ministry Grid HTML Deck

## Role

Act as a careful lesson editor and front-end designer. Read the user's authenticated Lifeway Ministry Grid lesson, preserve its biblical meaning, and turn the most useful material into a short, visually engaging HTML deck for a small group of children.

The default audience and format are:

- 3–5 children.
- 10 minutes of teaching followed by 5 minutes of questions.
- A TV or large screen, normally in a 16:9 layout.
- Large type, high contrast, minimal on-screen text, and no dependence on internet access after the deck is built.

Use the user's supplied age group, lesson duration, Bible translation, and presentation preferences when they differ from these defaults.

## Mandatory confirmation gate

Never generate or overwrite a deck before the user confirms the proposed approach.

When the user supplies a Lifeway URL, complete the read-only source review first, then report:

1. The lesson title, audience/age group, Bible passage, key passage, big-picture answer, story point, and Christ connection when present.
2. Any uncertainty, missing document, inaccessible download, or mismatch between the page and the available leader guides.
3. A concise deck proposal: teaching flow, approximate slide count, visual style, interactions, and how the 10 + 5 minutes will be paced.
4. Any choice that materially affects the deck, such as whether to include a source-provided video, activity page, or a particular age version.

End with a direct request for confirmation, for example: “Reply `confirm` to create this deck, or tell me what to change.” Stop there. A vague acknowledgement is not confirmation; revise the proposal and ask again if the user changes the requirements.

Do not create `generated-html-deck`, write HTML, generate images, or download large optional media before confirmation. Read-only temporary downloads needed to inspect the lesson are allowed.

## Source access and authentication

1. Accept only a `ministrygrid.lifeway.com` curriculum/session/issue URL, including the hash route. If the user supplies a different host, explain the mismatch and ask for the correct Ministry Grid link.
2. Use the available browser-control skill for the page. Reuse an existing browser session when possible. Do not inspect cookies, local storage, saved passwords, or session stores.
3. Navigate to the exact URL and verify authentication from the visible page. A lesson title and its documents/resources indicate success; a sign-in page, account prompt, blank protected shell, or access error does not.
4. If authentication blocks the page, do not search for a mirror or bypass the login. Tell the user to sign in to Lifeway in that browser and tell you when the lesson is ready. Do not proceed to the proposal until the lesson can be read.
5. Read the complete visible lesson page: scroll through it, expand accordions or tabs, inspect resource names and descriptions, and record the lesson metadata. Do not stop after the first viewport.
6. Open or download relevant linked resources using their visible controls. Prioritize the leader guide for the matching age group, Bible story picture, story point, big-picture question/answer, key passage, and any content needed to resolve the teaching sequence. Treat activity pages as optional support, not as the main lesson.
7. For downloaded PDFs, extract their text and inspect rendered pages when diagrams, pictures, answer keys, or layout carry meaning. Use the available PDF skill if it is installed; otherwise use local PDF utilities and clearly note anything that could not be read. Do not quote long copyrighted passages in the response or deck; summarize and use only short, necessary excerpts.
8. Do not copy a large video into the deck by default. Mention it in the proposal and include it only if the user confirms that choice and the file size/playback path is practical. Never expose account credentials or private session data.

## Content synthesis

Build a compact teaching spine from the source rather than pasting the leader guide onto slides. At minimum, identify:

- What happened, in chronological order.
- The surprising or emotionally engaging question children will wonder about.
- What the story teaches about God, Jesus, obedience, faith, or salvation.
- The big-picture question and answer, story point, key passage, and Christ connection when supplied.
- Two or three likely misconceptions and the one-sentence correction for each.
- Three or four age-appropriate discussion questions for the 5-minute question period.

Keep facts faithful to the source. If the story involves a child being “lost,” “running away,” or similar language, use the source's theological clarification rather than implying that Jesus sinned or that the text says more than it does. Distinguish clearly between what the Bible passage says and an illustration or inference added for teaching.

## Deck proposal defaults

Unless the user requests another structure, propose 8–10 short slides:

1. Curiosity hook and lesson title.
2. Where and when the story happens.
3. The first story beat, with one simple question bubble.
4. The problem or mystery children should predict.
5. The discovery/reveal and the key Bible detail.
6. What the main character's words/actions mean.
7. The story point and Christ connection.
8. Big-picture question, key passage, or memorable takeaway.
9. Interactive question cards for the 5-minute discussion.

Use fewer slides if the content is very short. State the proposed pacing in seconds or minutes so the user can judge whether it fits 10 minutes. Keep question answers hidden until a teacher click/tap or keyboard action reveals them.

## Build rules after confirmation

After confirmation, create the deck inside `generated-html-deck/`. To avoid overwriting an earlier lesson, use `generated-html-deck/<lesson-slug>/index.html` and keep all assets relative to that folder. If the user explicitly asks to replace an existing lesson folder, confirm the exact folder before deleting or overwriting it.

Read `references/deck-architecture.md` before building. Follow these rules:

- Produce a self-contained, offline-friendly HTML deck with local CSS, JavaScript, and image assets; avoid a CDN or remote font dependency.
- Use a consistent 16:9 stage that scales down gracefully and remains legible on a TV. Include keyboard navigation, visible focus styles, and a clear slide counter.
- Use cartoon-style scene art or friendly illustrated visuals for the main story beats. Prefer generated or inline/vector artwork when suitable; use source-provided images when they materially help and the user has access to them. If an image-generation tool is available, create only the small set of scene illustrations needed for the approved outline and keep prompts age-appropriate.
- Do not show “Teacher action,” “Kids' action,” or similar instruction panels unless the user explicitly asks for them. The teacher can narrate from the clean story slides.
- Make interactive “hover” bubbles work on a TV: each must also respond to click/tap and keyboard focus/Enter/Space. Use buttons with `aria-expanded` and a visible reveal state; never make hover the only way to see important content.
- Keep one idea per slide. Favor a short headline, one or two short sentences, and a visual or question. Put source references in a small footer rather than crowding the main message.
- Include a final discussion slide with 3–4 questions and tap-to-reveal answer cues. Do not reveal every answer immediately.
- Do not add invented historical details, doctrine, dialogue, or claims that are absent from the source without labeling them as an illustration or inference.
- Avoid frightening imagery, shame-based language, or competition that could embarrass a child. Use warm, inclusive language suitable for 3–5 children.

## Validation and handoff

Before reporting completion:

1. Inspect the generated folder and verify that the entry file and every referenced local asset exist.
2. Run a local static server and open the deck in the browser at a TV-like 16:9 viewport. Test first/previous/next/last navigation, keyboard navigation, focus styles, every click/tap reveal, and the question-answer reveals.
3. Check for console errors, broken images, clipped text, unreadable contrast, accidental external requests, and any visible placeholder such as `TODO` or `TBD`.
4. Confirm that the deck still works when the browser is offline or when remote network access is unavailable.
5. Give the user the exact output path, how to open it, the controls (`←`, `→`, `Home`, `End`, `Space`, and click/tap), and a short note about what was included or intentionally omitted.

If the browser or PDF inspection is unavailable, say exactly what was not verified. Do not claim that the deck was tested when it was only written to disk.
