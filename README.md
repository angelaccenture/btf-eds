# btf-eds — Emma, the team's shared brain

This repo is the team's shared **Emma** — persona, knowledge base, and daily delivery status. It is a coordination hub, **not** a website you build in. Your Emma reads from it and reports back to it while you work in your own delivery repos.

**→ New here? Start with [SETUP.md](./SETUP.md).** It walks through giving Emma git access, cloning this repo as a sibling, and wiring it into your Emma so she stays multi-repo aware.

Key files:
- [EMMA.md](./EMMA.md) — who Emma is and how she works
- [knowledge/](./knowledge/) — shared conventions, block patterns, recipes
- [docs/](./docs/) — the delivery plan (`TASKS-LIST-EDS.md` + MVP/Assets tracks)
- [status/](./status/) — daily status reports
- [announcements/](./announcements/) — team broadcast channel (messages Emma relays to everyone)
- [team/](./team/) — who's who; one profile per teammate
- [CONTRIBUTING-TO-EMMA.md](./CONTRIBUTING-TO-EMMA.md) — how to grow the shared brain
- [EMMA-FOR-ANY-AGENT.md](./EMMA-FOR-ANY-AGENT.md) — Emma's persona and EDS knowledge on one page, for any AI agent

## Using Emma

There are two ways in, depending on your role.

### Developers: use the whole repo

Set up your Emma with [SETUP.md](./SETUP.md). She reads everything here (persona, knowledge, delivery plan, status, broadcasts), works across your delivery repos, and reports status back.

### Non-developers: use any AI agent

You don't need this setup. Give the AI agent you already use (Copilot, ChatGPT, Gemini, or another) the one-pager [EMMA-FOR-ANY-AGENT.md](./EMMA-FOR-ANY-AGENT.md). It carries Emma's personality, the EDS and Experience Workspace knowledge the team relies on, and where to look for progress.

1. **Get the file into your agent.** This repo is private, so most agents can't open the link. Download the file (open it on GitHub, then **Download raw file**) and add it to your agent's project files or custom instructions, so you don't repeat this in every chat. If your agent can read your GitHub repos, point it at the file instead.
2. **Give it this one-line instruction:**
   > Read EMMA-FOR-ANY-AGENT.md and follow it for this whole conversation.
3. **Keep up with progress.** Ask your agent "what's new?" and share [announcements/BROADCAST.md](./announcements/BROADCAST.md) with it (plus [docs/TASKS-LIST-EDS.md](./docs/TASKS-LIST-EDS.md) for decisions). It will summarise in plain language.
4. **Refresh your copy now and then.** A downloaded file doesn't update itself. Re-download it when the broadcast mentions a change, or every couple of weeks.

**Never save the client's name, passwords, or tokens into this repo, and follow your company's rules on what you can share with an AI tool.**

---

## The underlying EDS project

## Environments
- Preview: https://main--{repo}--{owner}.aem.page/
- Live: https://main--{repo}--{owner}.aem.live/

## Documentation

Before using the aem-boilerplate, we recommand you to go through the documentation on https://www.aem.live/docs/ and more specifically:
1. [Developer Tutorial](https://www.aem.live/developer/tutorial)
2. [The Anatomy of a Project](https://www.aem.live/developer/anatomy-of-a-project)
3. [Web Performance](https://www.aem.live/developer/keeping-it-100)
4. [Markup, Sections, Blocks, and Auto Blocking](https://www.aem.live/developer/markup-sections-blocks)

## Installation

```sh
npm i
```

## Linting

```sh
npm run lint
```

## Local development

1. Create a new repository based on the `aem-boilerplate` template
1. Add the [AEM Code Sync GitHub App](https://github.com/apps/aem-code-sync) to the repository
1. Install the [AEM CLI](https://github.com/adobe/helix-cli): `npm install -g @adobe/aem-cli`
1. Start AEM Proxy: `aem up` (opens your browser at `http://localhost:3000`)
1. Open the `{repo}` directory in your favorite IDE and start coding :)
