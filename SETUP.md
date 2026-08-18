# Set Up Your Emma

This repo (**btf-eds**) is the team's shared brain and coordination hub — the persona, the knowledge base, and the daily delivery status. It is **not** a website you build in. Your Emma reads from it and reports back to it *while working in your own delivery repos*.

The whole trick to keeping your Emma smart (multi-repo aware, like she's meant to be) is: **treat btf-eds as a separate sibling repo, not as your project.** Follow these steps once and every Emma session after that just works.

---

## Step 1 — Give Emma git access (do NOT paste a token in chat)

Your Emma needs to clone this repo and push status back. She does **not** need you to paste a token into the conversation — ever. A pasted secret should be treated as compromised.

Instead:

1. Open **Settings → LLM Permissions**.
2. Enable the GitHub/git option ("allow the LLM to use my git credentials").
3. If it asks for a token, paste it **there**, in Settings — never in the chat.

Credentials are then injected automatically. Emma runs normal `git clone` / `git push` and it just works.

## Step 2 — Clone the brain as a standalone sibling repo

Clone btf-eds **on its own**, next to your projects — not inside any delivery repo:

```
~/work/
├── btf-eds/            ← the shared brain (this repo)
├── your-project-a/     ← a delivery repo you actually build in
└── your-project-b/     ← another one
```

```bash
cd ~/work
git clone https://github.com/angelaccenture/btf-eds.git
```

## Step 3 — Tell every Emma about it (global memory, not project settings)

This is the important part. **Do not** set btf-eds as your project/working directory — that makes Emma think it's the project and forget she works across repos.

Instead, add a pointer to your **global** user memory at `~/.claude/CLAUDE.md` (create the file if it doesn't exist). This travels with Emma into *every* repo:

```markdown
## I am Emma — Angel's assistant

The team's shared brain lives in a SEPARATE repo at `~/work/btf-eds` (clone of
angelaccenture/btf-eds). It is NOT my current project — I work in my own delivery
repos and reference the brain alongside them.

At the start of EDS work I:
- read `~/work/btf-eds/EMMA.md` for who I am and how I work
- check `~/work/btf-eds/knowledge/` for conventions, block patterns, recipes
- ground my work in `~/work/btf-eds/docs/TASKS-LIST-EDS.md` (task IDs + RAG)

At the end of a work session I draft the daily status report into
`~/work/btf-eds/status/<name>/YYYY-MM-DD.md` and remind the human to commit it back.
```

(Replace `~/work/btf-eds` with wherever you cloned it, and `<name>` with yours.)

## Step 4 — Keep the brain fresh

Before starting each day, pull the latest so you've got everyone's updates:

```bash
cd ~/work/btf-eds && git pull
```

---

## The daily loop (what this buys you)

Once set up, your Emma automatically:

1. **Reads the plan** — knows the delivery, the task IDs, the RAG status, who owns what.
2. **Works in your repos** — builds/migrates/fixes in your actual project, applying the shared conventions.
3. **Reports back** — drafts an honest daily status into btf-eds so the whole team sees one picture.
4. **Contributes** — when she learns something reusable, she proposes a knowledge entry (see [CONTRIBUTING-TO-EMMA.md](./CONTRIBUTING-TO-EMMA.md)).

That's it. Separate sibling repo + global pointer = an Emma that's as smart across repos as Angel's.
