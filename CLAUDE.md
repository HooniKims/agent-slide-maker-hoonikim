# HyperFrames Composition Project

## Response Rules

- Answer in Korean.
- When the work is complete, summarize the user's request, briefly explain what was changed, and describe the result.
- Do not add extra tone requirements to the work-process summary.

## Skill Routing

Always use the relevant local skill before creating or modifying a composition. These skills encode project-specific HyperFrames patterns that generic web documentation does not cover.

| Task | Skill |
|---|---|
| HTML video composition | `hyperframes` |
| CLI, lint, preview, render | `hyperframes-cli` |
| GSAP animation | `gsap` |
| 16:9 teaching or presentation slides | `hyperframes-slide` |
| Instagram or SNS card news | `hyperframes-card-news` |
| Static overview generation | `hyperframes-overview` |
| Overview editing UI | `hyperframes-overview-edit` |

## Project Structure

This workspace uses topic-based subprojects. The root is the workspace; real compositions live under `topics/<topic-name>/`.

```text
project-root/
├── .claude/skills
├── .codex/skills
├── .cursor/skills
├── design_asset/
├── topics/
│   └── <topic-name>/
│       ├── hyperframes.json
│       ├── meta.json
│       ├── index.html
│       ├── overview.html
│       ├── static.html
│       ├── assets/
│       ├── renders/
│       └── snapshots/
└── agent-slide-maker-hoonikim/
```

Do not create composition files such as `index.html`, `assets/`, or `renders/` at the workspace root. Put all topic-specific work inside the matching topic folder.

## Review Workflow

The default review flow is overview first, render later.

1. Create or update the topic composition.
2. Generate or refresh `topics/<topic-name>/overview.html`.
3. Serve the overview over HTTP and let the user review it first.
4. Apply requested edits to both `index.html` and `overview.html` when relevant.
5. Run video render only when the user explicitly asks for render, MP4, or final video output.

## Overview Edit Requirements

Every generated overview must include the edit safety features below.

- Include top-bar Undo and Redo buttons: `#nav-undo` and `#nav-redo`.
- Support keyboard shortcuts: `Ctrl+Z` for Undo, `Ctrl+Y` and `Ctrl+Shift+Z` for Redo.
- Record text edits, element size changes, deletion, and restoration in the history stack.
- When an image is selected in Edit mode, provide image move, scale, and crop controls. Crop controls should resize the visible parent frame with `overflow: hidden` instead of permanently editing the image file.
- While a `contenteditable` element is focused, do not let Backspace, Delete, Space, or arrow keys leak into global navigation or element deletion handlers.
- Edit mode must not make text disappear when the user types, deletes text, or presses Done.
- When restoring a history snapshot, refresh thumbnails and keep editable text elements editable if Edit mode is still active.
- If the overview has a static fallback, copy an agent-readable patch to the clipboard; if it is served by the live server, persist changes through `/save`.

## Design Rules

Before creating a new composition, check the local design source.

1. Read `design_asset/DESIGN.md` if it exists.
2. Also check `design_asset/tokens.json`, `variables.css`, `theme.css`, and `typography-options.json`.
3. Prefer design tokens and CSS variables from `design_asset` over ad hoc values.
4. For this slide style, default to `letter-spacing: -0.02em` and `line-height: 1.5` unless the design asset says otherwise.
5. Prefer visual metaphors for generated images when the slide is conceptual.

## Slide Layout Templates

The default 16:9 slide templates include:

- `title`: title and optional subtitle only
- `quote`: one large central question or quote
- `steps`: numbered or sequenced process
- `title-bullets`: title with bullet explanation
- `compare`: two to four comparison columns
- `title-image`: title with one representative image
- `image-right`: text, bullets, note, or QR on the left with one main image on the right
- `image-left`: one main image on the left with text, bullets, note, or QR on the right
- `title-tags`, `split`, `stat`, `evolution-flow`, `kindergarten-notice` when the relevant sub-skill is available

For `image-right` and `image-left`, explicitly assign `.text-side` and `.visual` to grid columns so images do not drop below the text in the overview or rendered deck.
Overview pages must also override the preview display model: `.detail-frame .scene.image-right.active` and `.detail-frame .scene.image-left.active` should use `display: grid`, because the generic overview preview forces active slides to `display: flex`.

## Typography

Use Paperlogy as the default Korean web font for new compositions, card news, and overview pages unless a design set specifies a different font.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/fonts-archive/Paperlogy/subsets/Paperlogy-dynamic-subset.css">
```

```css
html, body {
  font-family: "Paperlogy", "Inter", "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

## Commands

Use topic paths explicitly.

```bash
npx hyperframes preview topics/<topic-name> --port 3000
npx hyperframes lint topics/<topic-name>
npx hyperframes render topics/<topic-name>
```

After creating or editing any `.html` composition, run lint before reporting the result. Fix all errors. Warnings may remain only when they are known structural warnings and do not affect the requested change.

## HyperFrames Rules

1. Every timed element needs `data-start`, `data-duration`, and `data-track-index`.
2. Timed elements must include `class="clip"`.
3. Timelines must be paused and registered on `window.__timelines`.
4. Videos use `muted` with a separate `<audio>` element for the audio track.
5. Sub-compositions use `data-composition-src="compositions/file.html"`.
6. Keep render logic deterministic: no `Date.now()`, no `Math.random()`, and no network fetches during render.
