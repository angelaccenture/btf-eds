# Daily Status — Reporting Back

We're all delivering **one thing together**. The plan lives in [`docs/`](../docs/):

- [`TASKS-LIST-EDS.md`](../docs/TASKS-LIST-EDS.md) — the master task list, by work track. Every task has an **ID** (e.g. `1.1.2`), a **RAG** status (🟢/🟡/🔴), and a **Who** (🤖 Emma / 👤 Human / 🤝 Both).
- [`MVP-TRACK.md`](../docs/MVP-TRACK.md) — the client MVP build (cites bucket IDs).
- [`AEM-ASSETS-TRACK.md`](../docs/AEM-ASSETS-TRACK.md) — the DAM workstream.

Because every Emma works across her own repos, we sync up by **reporting back here daily**. That's how the team sees one shared picture of the delivery.

## How it works

1. **One file per person per day.** Your reports live in `status/<your-name>/YYYY-MM-DD.md`. Because it's your own folder and dated file, two Emmas reporting at once never conflict.
2. **Copy [`TEMPLATE.md`](./TEMPLATE.md)** to start today's report.
3. **Speak the plan's language.** Reference tasks by their **ID** from `TASKS-LIST-EDS.md` (e.g. "Progressed `1.2.4`"), and give each a RAG so status rolls up cleanly.
4. **Commit + push (or PR) at end of day.** This repo is the source of truth for delivery status.

## What a daily report covers

- **Done today** — tasks moved, by ID.
- **In progress** — what's mid-flight, by ID + current RAG.
- **Blocked** — what's 🔴 and *why* (waiting on a decision `Dxx`, a credential, another track).
- **Needs a human** — anything flagged 👤 or 🤝 that needs a sign-off, access, or a call.
- **Next** — what you pick up tomorrow.

## The rule for Emma

When you finish a work session, **draft the human's daily report** from what you actually did — real task IDs, honest RAG, blockers named plainly. Don't inflate status; a 🟡 that's really 🔴 helps nobody. Then remind the human to commit it back here.
