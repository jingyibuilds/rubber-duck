# Design decisions

Why Rubber Duck looks the way it does. Each entry records what was chosen, what was rejected, and why.

## Where the evidence comes from

- **One observed session.** A long thinking session between one person and an AI (nine rounds, about two and a half hours). An observer logged every move the AI made (summarize, ask, structure, extend, research, argue the other side, point out a pattern) and how the person reacted: used it, changed it, rejected it, or ignored it. After the session, a fresh AI session rebuilt what happened from the log alone, to test whether the log was enough.
- **Existing skills.** We read the full text of the closest skills: [superpowers brainstorming](https://github.com/obra/superpowers), [Claudest brainstorm](https://github.com/gupsammy/Claudest), [grill-me](https://github.com/mattpocock/skills), [socratic-method](https://github.com/malkreide/socratic-method-skill), and four skills that describe themselves as a rubber duck ([Claude-Skill-Potions](https://github.com/ElliotJLT/Claude-Skill-Potions/blob/main/skills/rubber-duck/SKILL.md), [KiroCrew](https://github.com/kirodotdev/KiroCrew/blob/main/skills/rubber-duck/SKILL.md), [duck-critic](https://github.com/aktsmm/Agent-Skills/blob/master/duck-critic/SKILL.md), [Heimdall](https://github.com/kinncj/Heimdall/blob/main/.claude/skills/rubber-duck/SKILL.md)).

This is a small evidence base: one person, one kind of task (working out a definition). Treat the rules as a first version.

## 1. Listening and sorting are the core; checking and challenging are offers

- **Chosen:** every round is the same loop: take it in, go one step past a summary, draw the map, ask at most one question, offer next steps.
- **Rejected:** six modes the user picks from (listen, structure, challenge, research, draft and compare, converge). Someone who is thinking out loud usually doesn't know which mode they want, and choosing a mode is work the skill should save them.
- **Why:** the person in the observed session valued having their thoughts sorted far more than any single move. Research and pushback were useful, but only after the content had taken shape.

## 2. A map every round, not one deliverable at the end

- **Chosen:** each reply is a map: anchor, through-line, tagged parts, settled / open, parked. Its shape depends on what the user is circling (a decision, a plan, an idea, a problem, an argument).
- **Rejected:** agreeing on one deliverable in the first turn (a one-page plan, a decision memo) and building toward it.
- **Why:** people who are thinking out loud rarely start with a goal, so the skill has to pick the output for them. A map every round also gives them something to react to straight away.

## 3. Three rules against three failures

The three failures (drift, running off, agreeing) are what an AI does by default when nobody instructs it.

- **Hold the anchor (against drift).** In the observed session the person had to correct the same drift twice: the AI kept going deeper into the example (a specific field) instead of the general question. The first correction was acknowledged but not turned into a rule, so it happened again. Hence: an anchor at the top of every map, examples kept to one line, and corrections restated as rules that get stricter if they repeat.
- **Label everything you add (against running off).** When the person moved on with a single line and no new material, the AI filled the turn with its own content and became the lecturer. Hence: four tags, and at most one idea per reply that doesn't come from the user.
- **Don't just agree (against confirming).** Proposals backed by evidence were decided quickly; pure inference hung unanswered. Hence: the *no basis yet* tag, which also turns into the list of claims to check.

## 4. One question at most

- **Chosen:** one question per reply, at the top or the bottom; a stated default instead of a question where one makes sense; stop asking after two skipped questions.
- **Rejected:** batches of questions (the style of Anthropic's [doc-coauthoring](https://github.com/anthropics/skills/tree/main/skills/doc-coauthoring), 5–10 numbered questions at once), or 2–3 per round (Claudest brainstorm style).
- **Why:** in the observed session, 1 of 6 direct questions got an answer. The one that worked asked what the output was for. Questions that asked the person to recall or introspect were skipped, even when well phrased. One question that sat at the very end of a long reply, just above the source list, went unanswered too.

## 5. "One step past a summary" means the through-line

- **Chosen:** each round names the through-line (often the question under the question), the unsaid assumptions, and the conflicts.
- **Why:** the most useful thing the AI did in the observed session was to take a worried aside, about whether their direction was right at all, and name it as the real question: how does a beginner know they're on the right track? That became the backbone of the final result, though the person only confirmed it several rounds later. Hence: the through-line is tagged *mine* until confirmed, and silence is not read as rejection.

## 6. Draft-and-compare is a fallback, not a main move

- **Rejected as a main move:** the AI writes its own version and the user marks the differences.
- **Why:** in the observed session it worked once, when the person asked for it. But someone rubber-ducking usually says their version out loud anyway. It stays as a single line for when the user is stuck.

## 7. An optional log, with notes on how the user is thinking

- **Chosen:** if the host can write files, offer once to keep a log: the current map, one line per round, and up to three observations about how the user is thinking, shared at wrap-up. The log can be read back in a new session to rebuild the map.
- **Why:** long conversations lose their early parts. The observed session kept exactly this kind of log, and a fresh session could rebuild what happened from it. The test also found what such a log misses: it doesn't record which move a reaction was to, and it doesn't keep the user's own words. Comments about how the person was thinking, made mid-flow, were mostly ignored, so the observations are saved for the end.

## 8. Name

- **Chosen:** `rubber-duck`. It is what people say when they want to think out loud.
- **Known clash:** GitHub Copilot CLI has an experimental built-in "Rubber Duck" that reviews an agent's plans and code with a second model. The other skills that use the name do debugging-style questioning, or have a second model review the agent's own work. The description says "for thinking, not for debugging or reviewing code", and the README has a "What it is not" section.

## 9. Length

- **Chosen:** about 1,550 words.
- **Rejected:** a 2,100-word first draft with modes, a dial table, a trigger table, and checkpoints. Most of it repeated itself. The comparable skills we read run from about 300 to 2,400 words (word counts of their SKILL.md files); what matters is that every line is an instruction.

## 10. Markdown first, HTML optional

- **Chosen:** the map is always Markdown in a fixed template. A one-page HTML version of the same map is offered when the user will come back to it or share it, shown where the host can render it and saved as a file where it can't.
- **Rejected:** letting the agent pick "the best form" each time, with diagrams or HTML as equals to text.
- **Why:** HTML and Mermaid only render in some interfaces (artifacts, canvases, GitHub), not in terminals. A fixed Markdown template means every user gets the same result in every host, and it doubles as the log format. The HTML page adds the at-a-glance view without becoming a dependency.

## 11. A light framework with five fixed points

- **Chosen:** five things never change: the anchor on top, a tag on every claim, the Markdown template, at most one question, and a wrap-up that ends with the final map. Everything else is left to the agent's judgment.
- **Rejected:** a full procedure for every situation.
- **Why:** the skill is meant to be a small tool. Fixing the points that prevent drift, running off, and agreeing keeps the result predictable; leaving the rest open keeps it light.

## Known gaps

- Turning the map into an action plan (priorities, first step, stop criteria) never came up in the observed session. The "plan" shape is untested.
- The rules come from one person who wanted to be challenged. "Adjust to the person" is the hedge; it needs testing with people who want a gentler duck.
