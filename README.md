# 🏗️ Agent Team Builder

A framework for creating persistent, personality-driven AI dev teams as Claude skills.

Each team is a squad of specialized subagents with distinct voices, opinions, and rivalries.
They run together in a "team meeting" and give brutally honest, multi-perspective feedback
on your software project — architecture, UX, security, QA, and more.

---

## What This Is

This repo contains the **process** for building a dev team skill — not a specific team.
You interview your agents into existence, one character at a time, then ship them as a
installable `.skill` file for Claude.

The result: type `"team meeting"` and get a full room of specialists who know your codebase,
argue with each other, and give you real opinions.

---

## Quickstart

```bash
# 1. Clone this repo
git clone https://github.com/your-username/agent-team-builder
cd agent-team-builder

# 2. Read the interview guide
cat interview/questions.md

# 3. Copy the team template
cp -r template/ my-team/

# 4. Fill in your agents (one file per agent)
# See template/agents/_template.md for the format

# 5. Package as a .skill file
python -m scripts.package_skill my-team/

# 6. Install in Claude and say "team meeting"
```

---

## Repo Structure

```
agent-team-builder/
├── README.md                        ← You are here
├── interview/
│   └── questions.md                 ← Character creator interview guide
├── template/
│   ├── SKILL.md                     ← Team room template (copy & customize)
│   └── agents/
│       └── _template.md             ← Single agent template
├── examples/
│   └── cloudblocks-sample/          ← Example: AWS app dev team
│       ├── SKILL.md
│       └── agents/
│           ├── foreman.md
│           ├── backend.md
│           ├── frontend.md
│           ├── product-ux.md
│           ├── qa.md
│           └── security.md
├── sprites/
│   ├── README.md                    ← How sprites work
│   └── archetypes/                  ← ASCII art for common roles
│       ├── foreman.txt
│       ├── backend.txt
│       ├── frontend.txt
│       ├── product-ux.txt
│       ├── qa.txt
│       └── security.txt
└── docs/
    ├── how-it-works.md              ← Deep dive on skill architecture
    ├── adding-agents.md             ← How to extend a team
    └── publishing.md                ← How to share your team
```

---

## The Team Meeting Format

When you say **"team meeting"**, your agents run in sequence:

```
🔨 [FOREMAN]     — Opens with agenda. Closes with action items.
🔐 [SECURITY]    — Audits everything. Speaks early.
⚙️  [BACKEND]    — Sees what breaks at scale. Interrupts freely.
🎨 [FRONTEND]    — Owns the interface. Allied with Product.
📐 [PRODUCT/UX]  — Future-focused. Challenges scope cuts.
🧪 [QA]          — Last word before Foreman closes. Nothing ships without sign-off.
```

The order can flex based on topic — but Security always speaks early, QA always speaks last.

---

## Sprites

Agents can have ASCII art portraits that render in Claude Code (terminal) or SVG icons
for web-based Claude interfaces. See `sprites/README.md` for how to attach sprites to agents.

---

## Design Principles

- **One SKILL.md per team** — the "team room" that loads all agents
- **One file per agent** — each character is isolated and swappable
- **Personalities create accountability** — agents check each other, not just you
- **Names are yours to assign** — templates use placeholders like `[Foreman]`
- **Project context is baked in** — agents know your stack and give real advice

---

## Contributing

PRs welcome for:
- New agent archetypes (DevOps, Data Engineer, Legal/Compliance, etc.)
- New sprite designs
- Example teams for different stacks (mobile, ML pipeline, CLI tool, etc.)
- Translations of the interview questions

---

## License

MIT — build your team, ship your product, share the process.
# agent-team-builder
