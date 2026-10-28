# Rubber Duck

A small skill for thinking out loud with AI.

I think out loud a lot, in long, messy messages. An AI with no instructions handles that badly in three ways: it drifts after the most vivid detail, it runs off with ideas of its own, and it agrees with whatever I seem to want. This skill is a light framework that stops those three things. You dump what's in your head; the AI listens, then hands it back as one short map you can take in at a glance.

It follows the open Agent Skills format, so it installs in Claude Code, Codex, the Claude apps, and other agents that support skills, on whatever model you already use there.

**Before** (what you type):

> ok so I keep thinking about building a little app for my climbing gym friends to log routes, everyone uses notes or nothing, I think there's already an app for this? not sure people would switch. also I kind of want to learn Swift anyway, and maybe it could make money but honestly that's not the point. my friend said they'd use it but they say that about everything. I only have weekends. oh and the gym owner might want a leaderboard. is this dumb?

**After** (the first reply):

> **What you're figuring out:** whether to build a route-logging app for your gym friends. *(yours: "is this dumb?")*
>
> **Through-line:** there are two reasons in here, learning Swift and fixing a real problem for friends, and they lead to different first versions. *(mine, check it)*
>
> **Parts**
> - Problem: friends log routes in notes or not at all *(yours)*
> - Demand: one friend would use it, but "says that about everything" *(yours)*; people would switch from notes *(no basis yet)*
> - Competition: "there's already an app?" *(no basis yet)*
> - Why you'd build it: learn Swift *(yours)*; money is "not the point" *(yours)*
> - Limit: weekends only *(yours)*
>
> **Conflicts:** "build it to learn" and "build it so friends use it" pull in different directions.
>
> **Settled:** nothing yet. **Open:** who it's for.
>
> **Parked:** the gym owner's leaderboard; making money.
>
> **One question:** if nobody but you ever used it, would it still be worth building?
>
> **Next:** I'd check the two *no basis yet* claims first: does an app like this exist, and do climbers switch from notes? Or I can argue against the whole idea, or you can keep talking.

## How it works

A few things are fixed; everything else is left to the AI's judgment.

| Fixed | Against |
|---|---|
| Your purpose sits at the top of every map. Anything that doesn't connect to it is parked. | Drift |
| Every claim is tagged *yours*, *mine*, *sourced*, or *no basis yet*. At most one new idea of its own per reply. | Running off |
| No praise. Things you said that conflict are shown side by side. | Agreeing |
| The map is always Markdown in the same template, so it reads the same in any chat app. | A wall of text |
| At most one question per reply. A wrap-up that ends with a final map. | Interviews that go nowhere |

On top of that, and only when it fits: checking the *no basis yet* claims against sources, arguing the other side, a one-page HTML version of the map, and a log file so you can pick the conversation up later, even in a new session.

It's for any topic: a decision, a plan, something you're learning, a piece of writing. It's not a code reviewer (GitHub Copilot CLI has an experimental "Rubber Duck" for that), not a debugging checklist, and not an interviewer.

## Installation

### Claude Code

```text
/plugin marketplace add jingyibuilds/rubber-duck
/plugin install rubber-duck@rubber-duck
```

Installed as a plugin, the skill answers to `/rubber-duck:rubber-duck`. On older Claude Code versions, use `npx skills add jingyibuilds/rubber-duck --global --agent claude-code`.

### Codex

```bash
npx skills add jingyibuilds/rubber-duck --global --agent codex
```

### Claude.ai and Claude Desktop

Download this repository as a ZIP (**Code → Download ZIP**) and upload it as a skill in Settings.

### Other agents

```bash
npx skills add jingyibuilds/rubber-duck --global --agent '*'
```

Leave off `--global` to install it only in the current project. For an agent the Skills CLI doesn't know, copy `SKILL.md` into its skill folder. For an assistant without skills, paste everything in `SKILL.md` below the frontmatter into its instructions.

## Usage

Say "I want to rubber-duck something", then dump.

- "Just listen": map only, no questions, no offers.
- "Push me": a challenge every round.
- "Check it": verify the *no basis yet* claims.
- "Keep a log": save the conversation so you can come back to it.
- "Wrap up": the final map.

## Notes

This came out of one long thinking session of my own, where every move the AI made was logged next to how I reacted. Most direct questions went unanswered. What helped was a map I could react to, and having the question underneath what I was saying named out loud. That's a small evidence base, so treat this as a first version. The design decisions are in [docs/DECISIONS.md](docs/DECISIONS.md).

## License

MIT
