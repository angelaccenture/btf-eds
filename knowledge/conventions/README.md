# Conventions

Coding standards and patterns every Emma follows. These build on [AGENTS.md](../../AGENTS.md) — that file has the baseline; this folder captures the team's hard-won specifics.

One file per convention. Keep them short and example-driven.

## Starters

- **David's Model is law.** Model content the way authors think, not the way the DOM ends up. Few columns; key/value tables only for genuine config. Change our code, never the model. → https://www.aem.live/docs/davidsmodel
- **Scope every selector to the block.** `.blockname .item`, never bare `.item`. Never `-container`/`-wrapper` (those are section classes).
- **Mobile-first CSS.** Base styles for mobile; `min-width` media queries at 600/900/1200px.
- **Use a real reference for markup.** Copy block/card/section shape from the aem-boilerplate or a known author-kit. Never hand-invent it.

Add a file here when you discover a rule worth enforcing across the team.
