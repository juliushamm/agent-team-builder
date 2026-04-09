# 🏗️ Agent Team Builder

A framework for creating persistent, personality-driven AI dev teams as Claude skills.

Each team is a squad of specialized agents with distinct voices, opinions, and rivalries.
They run together in a "team meeting" and give brutally honest, multi-perspective feedback
on your project — architecture, UX, security, QA, and more.

---

## Quickstart

### Option A: Interactive Builder (recommended)

Install the `build-team` skill in Claude Code, then run:

```
/build-team
```

Claude will interview you about your project and each agent, then write all the files.

### Option B: Manual

```bash
# 1. Copy the team template
cp -r template/ my-team/

# 2. Read the interview guide, answer questions for each agent
cat interview/questions.md

# 3. Fill in template/agents/_template.md for each agent
# 4. Update template/SKILL.md with your team

# 5. Install to your project
cp -r my-team/ /path/to/project/.claude/skills/my-team/
```

---

## Installing the Builder Skill

Copy `build-team.md` to your Claude skills directory:

```bash
# User-level (available in all projects)
cp build-team.md ~/.claude/skills/build-team.md

# Project-level
cp build-team.md /path/to/project/.claude/skills/build-team.md
```

Then in Claude Code: `/build-team`

---

## What You Get

After running the builder (or filling templates manually), you have:

```
my-team/
├── SKILL.md              ← The team room — loads all agents, defines meeting format
└── agents/
    ├── foreman.md        ← Lead: opens and closes every meeting
    ├── agent-2.md
    ├── agent-3.md
    ├── agent-4.md
    └── agent-5.md
```

Install to your project:
```bash
cp -r my-team/ .claude/skills/my-team/
```

Then say **"team meeting"** to run it.

---

## The Team Meeting

When you say **"team meeting"**, your agents run in sequence:

- **Lead** opens with agenda, closes with named action items
- **Specialists** give their domain take, interrupt when something is wrong
- **Alliances** form along principled lines — shared philosophy, not just friendliness
- **No one defers** to you for decisions they can make themselves

The speaking order flexes based on topic. The lead always speaks first and last.

---

## Repo Structure

```
agent-team-builder/
├── README.md                        ← You are here
├── build-team.md                    ← Interactive builder skill for Claude
├── interview/
│   └── questions.md                 ← Character creator interview guide (manual use)
├── template/
│   ├── SKILL.md                     ← Team room template
│   └── agents/
│       └── _template.md             ← Single agent template
├── sprites/
│   ├── README.md                    ← How sprites work
│   └── archetypes/
│       └── foreman.txt              ← ASCII art for the Lead/Foreman role
└── examples/
    └── README.md                    ← Links to example teams
```

---

## Design Principles

- **One SKILL.md per team** — the team room loads all agents
- **One file per agent** — each character is isolated and swappable
- **Personalities create accountability** — agents check each other, not just you
- **Names are yours** — templates use placeholders, the builder asks for yours
- **Project context is baked in** — agents know your stack and give real advice
- **5 agents is the sweet spot** — enough coverage, not too many voices

---

## Tips for Good Characters

**Give them something to fight about.**
The most useful agents have overlapping domains. Two agents who both claim ownership of the same thing catch more issues than either would alone.

**Make the quiet ones quieter.**
If one agent speaks rarely, make every word land. A QA who rarely speaks but always stops a bad decision is more valuable than someone who talks constantly.

**Ground personalities in the stack.**
"Worried about scale" is vague. "Worried about your DynamoDB scan without a limit at 1M items" is useful.

**Alliances should be principled, not tribal.**
Frontend and Product ally because they share a user-first philosophy — not just because they get along.

---

## Contributing

PRs welcome for:
- New agent archetypes (DevOps, Data Engineer, Legal/Compliance, ML, Mobile)
- New sprite designs
- Example teams for different stacks
- Translations of the interview questions

---

## License

MIT
