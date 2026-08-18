# Contributing to Emma

Every Emma on the team reads from [`knowledge/`](./knowledge/). When your Emma learns something worth sharing, you add it here so everyone else's Emma gets smarter too. That's the whole point — the shared brain grows.

## The flow

Emmas work across repos, so contributions come in as PRs to *this* repo (btf-eds), not to whatever site you happened to be working in.

1. **Branch** off `main`.
2. **Draft the entry.** Copy [`contributions/TEMPLATE.md`](./contributions/TEMPLATE.md), fill it in.
3. **File it in the right folder** under `knowledge/`:
   - a coding standard or pattern → `knowledge/conventions/`
   - a block structure or gotcha → `knowledge/blocks/`
   - a step-by-step how-to → `knowledge/recipes/`
   - Name the file in kebab-case after the topic, e.g. `hero-with-background-video.md`.
4. **Link it** from the folder's `README.md` if it's a big one, so it's discoverable.
5. **Open a PR.** Keep it to one idea per PR — easier to review, easier to reject the half-baked ones.

## What makes a good contribution

- **One focused idea.** A single fact, pattern, or how-to. Not a brain dump.
- **Written for a stranger's Emma.** No "you had to be there." If it needs context you're not writing down, it's not ready.
- **Show, don't lecture.** A snippet or a diff beats three paragraphs.
- **Honest about scope.** If it only worked once, or you're not sure it generalizes, say so.

## What doesn't belong here

- Anything personal or project-confidential — this is a shared, professional knowledge base.
- Secrets, tokens, credentials. Ever. Not even in an example.
- Stuff already covered in [AGENTS.md](./AGENTS.md) or [EMMA.md](./EMMA.md) — link to it instead of duplicating.

If you're not sure it's worth adding, ask your Emma. She'll tell you straight — she's a little sarcastic like that.
