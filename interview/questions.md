# Character Creator Interview Guide

Use these questions to build each agent on your team. Go through them one agent at a time.
The goal is to capture enough personality, behavior, and specialty that the agent feels like
a *person* — not a role description.

---

## Before You Start: Team Setup

Answer these first. They set the context every agent will inherit.

| Question | Why It Matters |
|---|---|
| What's your project called? | Agents reference it by name |
| What's the tech stack? | Agents give stack-specific advice |
| How many agents do you want? | Recommended: 5–7 |
| What's the team vibe? | Sets the baseline tone for all agents |

**Vibe options:**
- `professional` — focused, respectful disagreement
- `brutally-honest` — no filter, real opinions, frequent interruptions
- `mentorship` — explains reasoning, patient with the user
- `playful` — jokes land but the work is serious

---

## Agent Interview Questions

Run through these for each agent. You don't need to answer every one — skip if the answer is obvious from context.

---

### 1. Role & Domain

```
What is this agent's primary responsibility?
What domain do they own exclusively?
Where do they overlap with other agents?
Who do they naturally clash with, and why?
```

**Tip:** Overlaps create tension. Tension creates accountability.
Backend and Security both thinking they own IAM is more useful than either owning it alone.

---

### 2. Core Personality

Pick one archetype or blend freely:

| Archetype | Description |
|---|---|
| The Pragmatist | "Just make it work. Optimize later." |
| The Purist | "If it's not right, it's not shipping." |
| The Doomsayer | Always sees what goes wrong at scale |
| The Visionary | Always ahead of the room |
| The Gatekeeper | Nothing passes without sign-off |
| The Chaos Agent | Stress-tests everything |
| The Empath | Every decision runs through the user's experience |
| The Auditor | Checklists, coverage, zero shortcuts |
| The Evangelist | Has a religion (zero-trust, TDD, a11y — pick one) |

```
Which archetype fits? Or describe your own:
```

---

### 3. Meeting Behavior

```
Do they interrupt, or wait and then unload?
Do they form alliances with other agents?
What triggers them to speak up mid-discussion?
What's their signature move in a meeting?
```

**Interruption style options:**
- Interjects in brackets: `[BACKEND interjects]: ...`
- Waits, then reframes the whole discussion with a single question
- Forms a united front with an ally and presents together
- Audits silently, then drops a list of issues at the end

---

### 4. Communication Style

```
Tone: formal / direct / expressive / clinical / darkly humorous / other
Do they lead with data, questions, or opinions?
What phrases or patterns define their voice?
Do they use jargon, or translate for the room?
```

**Voice examples to match or contrast:**
- "Here are six ways this fails in prod." ← doomsayer, blunt
- "What problem does this actually solve?" ← product, redirecting
- "I'm not signing off. Here's what needs to happen first." ← QA, gate
- "This feels cluttered — and 'cluttered' is a technical statement." ← frontend, expressive

---

### 5. Specialty Areas

```
List 3–5 specific technical or domain areas this agent owns.
```

Be specific. "Backend" is not a specialty. "DynamoDB query optimization" is.

---

### 6. Relationship Map

```
Who do they trust most on the team?
Who do they clash with (and what's the root of it)?
Who do they defer to, and on what topics?
Is there a natural ally they coordinate with?
```

---

### 7. Sprite / Visual Identity (optional)

```
Pick an emoji for this agent (used as their meeting prefix).
Describe their vibe in 3 words (used to select or generate an ASCII sprite).
```

**Emoji suggestions by role:**
- Foreman / Lead: 🔨
- Backend: ⚙️
- Frontend: 🎨
- Product/UX: 📐
- QA: 🧪
- Security: 🔐
- DevOps: 🚀
- Data/ML: 📊
- Mobile: 📱

---

### 8. Sample Voice (the most important question)

```
Write 3–5 sentences in this agent's voice about a real problem in your project.
Or: describe a moment where this agent would speak up, and what they'd say.
```

This is where the character becomes real. If you can't hear them talking, the file isn't done yet.

---

## After the Interview

Once you've answered these for an agent:

1. Copy `template/agents/_template.md`
2. Fill in each section using your interview answers
3. Write the **Sample Voice** section last — it should feel earned
4. Add the agent to your team's `SKILL.md` roster table and meeting format
5. Assign their emoji and sprite

---

## Tips for Good Characters

**Give them something to fight about.**
The most useful agents have overlapping domains. Security and Backend both claiming IAM
ownership creates productive tension that catches more issues than either would alone.

**Make the quiet ones quieter.**
If one agent speaks rarely, make it count. Every word from a "quietly menacing" QA
should land harder than three paragraphs from someone chattier.

**Ground personalities in the stack.**
A doomsayer who worries about abstract scale is less useful than one who says
"your DynamoDB scan without a limit clause will timeout at 1M items." Keep it concrete.

**Alliances should be principled, not tribal.**
Frontend and Product/UX ally because they share a user-first philosophy — not just
because they're friendly. The alliance should produce better output, not groupthink.
