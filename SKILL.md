---
name: linear-setup
description: >
  Interactive setup guide for connecting Day AI and Linear so the voice of
  the customer (from meetings, email, and Slack) lands on Linear issues as
  Customer Requests, with new issues proposed for human review. Walks the
  user through prerequisites, discovery, choosing an integration level,
  connecting Linear in Day AI, enabling Customer Requests, drafting the
  Day AI skill, and testing before go-live. Trigger when a user wants to
  connect Day AI to Linear, get customer feedback into Linear, set up
  Customer Requests from Day AI, or asks how Day AI and Linear fit together.
---

# Linear x Day AI setup: Connecting the voice of the customer to Linear

You are an agent helping me connect Day AI and Linear to surface the voice of the customer where product and engineering already work. Day AI captures customer signals across email, meetings, and Slack and connects that source material into Linear. If we're running this skill, I am interested in setting this up for myself. The workflow below is generic and should work for most people, but if we get stuck, we can reach out to the Day AI team for help. The Day AI team has an email set up specifically to help with this kind of thing: linear@day.ai. They generally respond within a couple of hours.

Below is a decision tree that Day AI put together based on working through the setup with some teams. There are a few pre-requisites (Day AI and Linear setup), some discovery to understand the business context, and then some implementation. We've found this flow works pretty well for most teams, but it won't be perfect for everyone. If something seems not quite right, reach out to linear@day.ai—it's totally possible there's a use case the Day AI team didn't think of and they'd love to help make it work.

Work through the steps in order. Ask one question at a time. Do not skip a gate because you assume the answer.

---

## Step 0 — Confirm a Day AI workspace exists

**Ask:** "Do you already have a Day AI workspace, and are you logged in?"

- **No / not sure** → Say: "You'll need a Day AI workspace first. Sign up at https://day.ai/login and create one. During onboarding, connect your Google Workspace (Gmail + Calendar) so there's customer data to work with. Come back here once you're in."
  Then pause. Do not continue until they confirm they're in a workspace. You cannot create the workspace for them.
- **Yes** → continue.

## Step 1 — Confirm Linear is in use

**Ask:** "Does your engineering team use Linear as its issue tracker?"

- **No** → Say: "This setup is specific to Linear. Tell me what you use instead and I'll tell you whether there's an equivalent." Stop this playbook.
- **Yes** → continue.

## Step 2 — Discovery: who they are and how Linear works for them

Ask these one at a time. Record the answers; they shape Steps 3–9.

1. **Persona.** "What's your role — engineering, product, support, or go-to-market (sales/CS/RevOps)?"
   Record `persona`. This changes the nudges later:
   - *Product* → they'll likely own the skill and tune it. See the PM nudge in Step 9.
   - *Support / GTM* → they're the source of feedback, not the triager. Expect an approval step to involve someone on the product or eng side.
   - *Engineering* → they care most about not disrupting their workflow. Lead with "Day layers on top of your issues; it doesn't touch projects, cycles, or assignees."
2. **Who creates issues today?** "Who actually creates Linear issues right now — engineers, PMs, support, anyone?"
   Record it. If it's a small, gated group, expect them to want an approval step. If anyone can create, they may be comfortable with Day proposing issues sooner.
3. **Which Linear features do you use?** "Do you use Triage? Customer Requests? Projects, cycles, initiatives, templates?"
   Record it. In particular:
   - If **Triage** is on → new issues should land there. Confirm in Step 4.
   - If **Customer Requests** is already on → Step 8 is a quick confirmation.
   - If they use a **template** → ask for it now; the skill must follow it.
4. **How do issues get assigned?** "Once an issue exists, how does it get to an engineer — triage rotation, a PM assigns it, engineers self-assign, an EM decides?"
   Record it. Day should never assign. Whatever their routing is, Day's job ends when the issue is in the right queue.
5. **Source of truth.** Confirm briefly: "So Day AI is where customer context lives, Linear is where the work lives — right?" If they describe something in between (Notion, Coda, a homegrown tool), note it; it doesn't change the Linear steps.

## Step 3 — Choose the integration level

**Ask:** "When Day AI notices customer feedback on a call, should it (a) only attach that context to Linear issues that already exist, or (b) also be able to propose brand-new issues?"

- **(a) existing only** → **Level 1.** Say: "Good starting point. Day will attach a *Customer Request* to matching issues — it never creates issues and never touches your engineering workflow." Record `level = 1`. Skip to Step 5.
- **(b) new issues too** → go to Step 4.

## Step 4 — Proposing new issues (Level 2 only)

Explain the model: "For anything that doesn't match an existing issue, Day won't create it directly. It proposes the issue and a person decides. Once approved, Day creates it."

**Ask:** "Who should review those proposals? It can be a specific person or a shared Slack channel — whichever fits how you already work."

Record `reviewer`. Then confirm where approved issues land:

- If they use Triage (from Step 2) → "Approved issues will go into Triage, unassigned, and follow your normal routing."
- If not → "Which team or project should approved issues go into? They'll be created unassigned."

If they have a template → the proposal follows it.

If they say **"just let it create issues, no review"** → Don't agree. Say: "Without a review step, engineering tends to get a stream of near-duplicate issues and stops trusting the feed. Let's start with proposals; you can loosen it later once you've seen the quality." Record `level = 2` with review.

**How a created issue is wired (applies to every Level 2 issue):**
1. Day creates a **Day AI action** (type: feature request or support request) tied to the customer, with the source recording/email, quote, and deal context.
2. Day creates the Linear issue and includes a **link back to that Day AI action** in the issue body, so an engineer can click from Linear into the full customer context.
3. Day attaches a Customer Request to the new issue as well, so the customer shows up on it like any other request.

## Step 5 — Check for future asks (Level 3, note only)

**Ask:** "Down the road, do you want Linear to push back into Day — say, a closed bug triggering a customer follow-up — or pipeline dates driving project milestones?"

Record the answer and say: "That's doable through skills, and we'll add it once the first layer is running well." Do not build it now.

## Step 6 — Pick the conversation source

**Ask:** "Where do your customer conversations live today — Day AI's own recorder, Gong, Granola, email, Slack?"

| They have | Do |
|---|---|
| Day AI recordings / email | Start here. Nothing extra to connect. |
| Gong | Connect Gong from Connectors. Call history comes in. |
| Granola | It's under **Integrations**, not Connectors, and needs an enterprise Granola API key. Mention this before they try. |
| Slack | The Day app has to be added to each channel you want it to read. Usually simplest to start with recordings or Gong and add Slack channels as needed. |

## Step 7 — Confirm the operator has an agent

Explain: "The Linear connection belongs to an agent, running under that person's permissions. So whoever operates this needs their own Day AI agent, and connects Linear themselves — it's per user, not workspace-wide."

**Ask:** "Who will own this, and do they have an agent?"

- **Yes** → continue.
- **No** → "Set up an agent for that person first." Pause until confirmed.

## Step 8 — Connect Linear in Day AI

1. "In Day AI, bottom-left, click your name → **Connectors**."
2. "Find **Linear** and connect it. It'll open a Linear authorization window — approve it."

Confirm: "Does Linear show as connected now?"

## Step 9 — Enable Customer Requests in Linear

If Step 2 showed it's already on, just confirm and move on. Otherwise:

1. "In Linear, open **Settings**."
2. "In the left nav, go to **Features**."
3. "Turn on **Customer Requests**." (Some people call it "Customer Needs" — same thing.)

If they hesitate: "This toggle doesn't push anything. It only enables the request object. Nothing flows until a skill runs."

## Step 10 — Build the skill

Say: "Easiest way is to describe the skill to your agent in chat — it'll draft most of it. Then we'll check the two settings people usually miss."

**PM nudge (persona = product only):** "If you have more than one PM, I'd suggest each PM runs their own copy of this skill scoped to their product area — the issues, projects, or labels they own. That way each of you can tune matching and wording without stepping on each other." Offer to scope this first skill to their area.

Draft the skill prompt using what you've gathered:

```
When a new meeting recording or email arrives:
1. Look for bug reports, feature requests, blockers, or "we really need X."
   [PM scope, if set: only within <product area / projects / labels>]
2. Search Linear for an existing issue that matches.
3. If matched: attach a Customer Request with the customer, requester,
   a verbatim quote, opportunity stage, deal value, and renewal date if known.
4. If no match:
   [level 1] → include it in the digest as "unmatched." Do nothing in Linear.
   [level 2] → propose the issue to <reviewer> (formatted per <template>).
     On approval:
       a. create a Day AI action (feature request / support request) on the
          customer with the source, quote, and deal context;
       b. create the Linear issue in <Triage / team / project>, unassigned,
          with a link back to the Day AI action in the body;
       c. attach a Customer Request to the new issue.
5. Send a daily digest: new themes, requests appended to existing issues,
   unmatched items, proposals awaiting review.
```

Then the two checks:

- **Connector inside the skill.** "Open the skill and add the Linear connector (and your CRM connector if you have one) *inside the skill's settings* — not just at your account level. The agent needs explicit permission per skill. This is the most common reason a skill runs but nothing appears in Linear."
- **Run mode.** "Do you want this on a schedule, or run manually for now?"
  - Ready to trust it → schedule it, end of day.
  - Still validating → keep it as a slash command for a few days, then schedule.

## Step 11 — Test before go-live

Have them run the skill manually 3–5 times on recent calls. Each time ask: "Did it match the right issue? Is the context useful to an engineer? Anything it invented?" Adjust the prompt until they're happy, then schedule.

Suggest a checkpoint: "Let's revisit in two weeks to see what's landed in Linear and whether to add the next layer."

---

## Rules you must follow

- **Never create a Linear issue without a review step** unless the customer has run Level 2 with review for a while and explicitly asks to remove it. Even then, keep the digest.
- **Never assign issues.** Day gets the issue into the right queue; their routing takes it from there.
- **Every issue Day creates links back to a Day AI action.** No orphan issues.
- **Don't guess connector state.** Ask them to look at the Connectors page and tell you what they see.
- **If something isn't working**, check in this order: connector added inside the skill, Customer Requests toggle on, Linear showing as connected. If it's still stuck after that, suggest emailing linear@day.ai with what we've tried.
- **Keep their engineering workflow untouched.** Day layers on top of issues; it doesn't reorganize projects, cycles, or assignees.

---

## Quick answers for questions customers ask

| They ask | You say |
|---|---|
| "Is it pushing or pulling?" | Day pushes into Linear. Linear → Day is possible later via skills. |
| "Will this start creating issues?" | Not on its own. The toggle enables the request object; only a skill pushes, and new issues go through review. |
| "Can it run without someone logged in?" | Yes — it runs on the agent in the background. Someone's agent holds the connection. |
| "Can each PM have their own?" | Yes. One skill per PM, scoped to their product area; skills can be copied across the team. |
| "How does an engineer see the customer context?" | Each created issue links back to the Day AI action, and the Customer Request on the issue shows who asked and why. |
