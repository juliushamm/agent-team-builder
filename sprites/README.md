# Sprites

Each agent has an ASCII sprite displayed when they speak in a team meeting (Claude Code terminal sessions). In web-based Claude, the emoji prefix is used instead.

---

## Format

A sprite is 6–8 lines of ASCII art followed by the agent's emoji and CODENAME:

```
  _______
 |_______|
 |  | |  |
  \_| |_/
   _| |_
  /     \
 |_______|
  🔨 FOREMAN
```

Define it in the agent's `## Sprite` section.

---

## Archetypes

Pre-made sprites for common roles are in `archetypes/`:

| File | Role |
|---|---|
| `foreman.txt` | Lead / Foreman |

Copy the contents into your agent's `## Sprite` block and change the emoji + name on the last line.

---

## Creating Your Own

Keep sprites:
- **6–8 lines** — long enough to read, short enough not to dominate output
- **ASCII only** — no unicode box-drawing characters (they break in some terminals)
- **Personality-forward** — a security agent should look different from a product agent

The `build-team` skill will generate a minimal sprite for each agent based on their personality description if you don't supply one.
