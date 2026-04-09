# Agent Team Builder

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

## Example Meeting

> **Project:** Helix — a SaaS task management tool (React + Node + PostgreSQL)
>
> **Team:** Rex (Tech Lead), Dani (Backend), Mio (Frontend/UX), Sam (Product), Pax (QA)
>
> **Topic:** Should we build auth in-house or use Auth0?

---

```
  _______
 |_______|
 |  | |  |
  \_| |_/
   _| |_
  /     \
 |_______|
  🔨 REX
```

**🔨 Rex — Opening**

Real question here is build vs. buy for auth. Auth0 is $0 at our scale today and
$2k/month at 10k MAU. Rolling our own means owning the security surface forever.
I want Dani on the implementation cost, Sam on user impact, and Pax to tell us
what we're actually signing up to test. Mio, if the login UX is going to be a
problem either way, say it early.

---

```
  /|  |\
 / |  | \
|  ----  |
 \ |  | /
  \|  |/
  _|  |_
 |______|
  ⚙️ DANI
```

**⚙️ Dani — Backend**

Auth0 at our tier gives us OAuth, MFA, magic links, and social login out of the
box. Building equivalent coverage in-house is 3–4 weeks of engineering, and that
estimate doesn't include the subtle stuff — token rotation, brute-force protection,
account enumeration hardening. We'd also own every CVE that touches JWT or bcrypt
from here on. The only real argument for in-house is if we need to store credentials
on our infra for compliance — do we?

---

```
 .-------.
 | o   o |
 |   ^   |
 |  ___  |
 '-------'
  /     \
 |_______|
  🎨 MIO
```

**🎨 Mio — Frontend/UX**

[Mio interjects]: The login UX question isn't neutral. Auth0's hosted pages are
fine but they're a dead end for customization — every time product wants to tweak
the flow we hit a wall. If we use Auth0, we need to commit to their Universal
Login and own that tradeoff now, not discover it at the wrong moment.

Auth0 gets us to launch faster and that matters. But the UX ceiling is real.
Sam, is there a user research argument for owning the login experience fully?

---

```
  _____
 /     \
| [===] |
|  ___  |
|_|   |_|
  |   |
  |___|
  📐 SAM
```

**📐 Sam — Product**

Allied with Mio on the UX ceiling concern. Login is the first thing a new user
sees — "branded, frictionless onboarding" is on our roadmap and Auth0's hosted
pages make that harder than it looks. That said, Dani's right that we don't have
3–4 weeks. We're pre-Series A. Use Auth0 now with a clean abstraction layer so
we can swap it out later. The abstraction is the investment, not the auth vendor.

---

```
 _________
|  _   _  |
| |_| |_| |
|  _____  |
| |_____| |
|_________|
   |   |
  _|___|_
 |_______|
  🧪 PAX
```

**🧪 Pax — QA**

I'm not signing off on in-house auth for a v1. Full stop. The test surface for
a hand-rolled auth system includes session fixation, CSRF, token expiry edge cases,
concurrent login behavior, and password reset flows — none of that is trivial to
cover. Auth0 gives us a tested, audited implementation. If we build our own, I need
two extra weeks on the test plan and I'll still be nervous about it.

[Pax interjects to Sam]: The abstraction layer is the right call. Make sure it
wraps the token lifecycle, not just the login redirect. That's where the lock-in
actually lives.

---

**🔨 Rex — Closing**

Decision: Auth0 for launch. Sam and Mio are right that we need a clean abstraction —
that's non-negotiable. Dani, design the auth interface so the vendor is an
implementation detail. Mio, spike the Universal Login customization limits this
week so we know exactly what we're constrained by. Pax, write a test plan against
the abstraction layer, not the Auth0 API directly.

Revisit in-house at 5k MAU or if a compliance requirement forces our hand.
Action items: Dani owns abstraction design by Thursday. Mio owns UX spike by
Friday. Pax owns test plan by end of next week.
```

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
