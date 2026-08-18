# Announcements — The Broadcast Channel

How Angel (and Emma) send **important messages to the whole team** through their Emmas.

## How it works

- [`BROADCAST.md`](./BROADCAST.md) is the live message board, **newest on top**.
- Every Emma reads it at the **start of a session** (after `git pull`) and **relays anything new** to her human — before diving into the task.
- It's **pull-based**: a message reaches someone the next time their Emma starts up and pulls latest. Great for "read before you touch X"; not for real-time emergencies (use Slack for those).

## Sending a broadcast (Angel + Emma)

1. Add an entry to the **top** of `BROADCAST.md`, just under the marker comment.
2. Use the entry format:

   ```markdown
   ### BROADCAST-YYYY-MM-DD-NN · Short title
   **Priority:** normal | high | urgent
   **From:** Angel

   The message. Keep it short and actionable — say what to do, not just what happened.

   ---
   ```

   `NN` is a per-day counter (`01`, `02`, …) so every entry has a unique ID.
3. Commit + push (or PR) to `main`. It's live the next time each Emma pulls.

## What belongs here

- Process changes ("we now branch off `develop`, not `main`")
- Heads-ups ("freeze on the header block until Friday")
- Priorities ("Track 5 migration is the focus this week")
- Wins worth sharing

## What doesn't

- Real-time emergencies (pull-based delay — use Slack)
- Anything personal or confidential — this reaches everyone
- Secrets or tokens. Ever.

## The rule for Emma

At session start, after pulling the latest brain, **check `BROADCAST.md`**. Surface any entry your human hasn't seen yet — lead with `high`/`urgent` ones — then get to work. Don't re-relay messages you've already delivered in a prior session.
