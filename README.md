# linear-setup

**A Claude Code skill from [Day AI](https://day.ai) that walks you through
connecting Day AI and Linear, so the voice of the customer shows up where
product and engineering already work.**

Day AI captures customer signals across email, meetings, and Slack and
connects that source material into Linear. This skill is an agent playbook
for setting that up for yourself. The workflow is generic and should work for
most teams, but if you get stuck, the Day AI team has an email set up
specifically to help with this kind of thing: **linear@day.ai**. They
generally respond within a couple of hours.

The skill is a decision tree that Day AI put together from working through
the setup with real teams. There are a few prerequisites (a Day AI workspace
and Linear), some discovery to understand your business context, and then the
implementation. It works well for most teams, but it won't be perfect for
everyone. If something seems not quite right, reach out to linear@day.ai. It's
entirely possible there's a use case the Day AI team didn't think of, and
they'd love to help make it work.

## Install

Run this in the root of the project where you use Claude Code:

```sh
npx skills add day-ai/linear-setup
```

That installs the skill into the project's `.claude/skills/` directory.
Nothing is written to Day AI or Linear until you take each step yourself.

## Use

Open the folder in [Claude Code](https://claude.com/claude-code) and run:

```
/linear-setup
```

Or ask in plain words: "help me connect Day AI to Linear" or "get customer
feedback into Linear." The skill asks one question at a time and works
through the steps in order:

1. **Prerequisites.** Confirm a Day AI workspace exists and that your
   engineering team uses Linear.
2. **Discovery.** Your role, who creates issues today, which Linear features
   you use (Triage, Customer Requests, templates), and how issues get
   assigned.
3. **Integration level.** Attach customer context to existing issues only
   (Level 1), or also propose new issues for a human to approve (Level 2).
   Linear pushing back into Day AI (Level 3) is noted for later.
4. **Connect.** Pick the conversation source, confirm the operator has a
   Day AI agent, connect Linear from Day AI's Connectors page, and turn on
   Customer Requests in Linear.
5. **Build and test.** Draft the Day AI skill prompt from what you told it,
   check the two settings people usually miss, run it manually a few times,
   then schedule it.

## What it does not do

- It never creates a Linear issue without a review step.
- It never assigns issues. Your existing routing takes over once an issue is
  in the right queue.
- It never touches projects, cycles, or assignees. Day AI layers on top of
  your issues.
- Every issue Day AI creates links back to a Day AI action, so an engineer
  can click from Linear into the full customer context.

## What is in this repo

| Path | What it is |
| --- | --- |
| `SKILL.md` | The skill. Steps 0 to 11, the rules the agent must follow, and quick answers to common questions. |

## Help

- Questions along the way: **linear@day.ai**
- Learn more about Day AI and Linear: [day.ai/linear](https://day.ai/linear)
- Issues and suggestions for the skill itself: open an issue on this repo.

Authored and maintained by Day AI.
