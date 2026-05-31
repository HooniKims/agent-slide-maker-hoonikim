# agent-slide-maker-hoonikim

> Original source: [Canine89/agent-slide-maker-easy](https://github.com/Canine89/agent-slide-maker-easy.git)
>
> This repository is a customized distribution based on the original project. It adds local workflow rules, design assets, HyperFrames overview editing improvements, Undo/Redo behavior, and export-oriented slide-making guidance.

## Overview

`agent-slide-maker-hoonikim` is a local skillset bundle for creating editable presentation decks with HyperFrames.

It is designed to help an AI coding agent create slide decks, generate an editable overview page, review slides visually, apply text/layout edits, and prepare outputs such as PNG, PDF, PPTX, or rendered video when needed.

## What Is Included

- HyperFrames-related agent skills under `.codex/skills/`
- Claude and Cursor skill links under `.claude/skills/` and `.cursor/skills/`
- Project guidance files: `AGENTS.md`, `CLAUDE.md`, `PROJECT.md`
- Design reference assets under `design_asset/`
- Example design references under `design_examples/`
- Overview editing support, including text edit, selector aiming, resize, delete, Undo, and Redo behavior

## Main Features

- Create 16:9 presentation slides with HyperFrames
- Use default slide templates including `title`, `quote`, `steps`, `title-bullets`, `compare`, `title-image`, `image-right`, and `image-left`
- Generate a static `overview.html` for review
- Edit slide text directly in the overview
- Select elements with Aim-style selectors
- Resize selected text or layout elements
- Delete and restore selected elements
- Undo and Redo edits with buttons and keyboard shortcuts
- Export deck results as image, PDF, or PPTX when the project template supports it
- Use local design tokens, typography, and visual style references

## Overview Edit Safety

Generated overview pages should include these behaviors:

- Undo button: `#nav-undo`
- Redo button: `#nav-redo`
- Undo shortcut: `Ctrl+Z`
- Redo shortcuts: `Ctrl+Y`, `Ctrl+Shift+Z`
- Text edit history tracking
- Element size, deletion, and restoration history tracking
- Protection against `contenteditable` key conflicts, so Backspace, Delete, Space, and arrow keys do not accidentally trigger global slide navigation or element deletion

## Recommended Folder Usage

Copy this whole folder into the target workspace.

Important files and folders should stay together:

```text
agent-slide-maker-hoonikim/
├── .claude/
├── .codex/
├── .cursor/
├── design_asset/
├── design_examples/
├── AGENTS.md
├── CLAUDE.md
├── PROJECT.md
├── hyperframes.json
├── meta.json
├── skills
└── skills-lock.json
```

Do not copy only part of the bundle unless you know exactly which skill or asset you need.

## Basic Workflow

1. Create or update a HyperFrames topic project.
2. Build the slide deck inside `topics/<topic-name>/`.
3. Generate or refresh `topics/<topic-name>/overview.html`.
4. Review and edit the overview first.
5. Apply requested changes to the source deck.
6. Run lint before considering the work complete.
7. Render video only when the user explicitly requests final video output.

## Common Commands

Run commands from the project root and target a topic folder explicitly.

```bash
npx hyperframes lint topics/<topic-name>
npx hyperframes preview topics/<topic-name> --port 3000
npx hyperframes render topics/<topic-name>
```

## Design Defaults

This bundle prefers the local `design_asset/` files before inventing new visual styles.

Default typography guidance:

- Korean web font: Paperlogy
- Letter spacing: `-0.02em`
- Line height: around `1.5`
- Prefer visual metaphors for conceptual slide images

## Slide Templates

The bundle includes side-image templates for editable teaching decks:

- `image-right`: text, bullets, note, or QR on the left; one main image on the right
- `image-left`: one main image on the left; text, bullets, note, or QR on the right

These templates explicitly lock text and image into separate grid columns, so the image stays beside the text instead of falling below it.

## Notes

This is not the original upstream repository. It is a customized working bundle intended for local AI-assisted slide production with HyperFrames.
