---
title: Promised documentation
---

# Promised

A Forge app for Jira that tracks the dated promises a team makes to customers in comments, reminds the team before one is broken, and keeps count of how many were kept.

## The problem

Support, account and delivery teams make promises all day, in comments: "we will have a fix out by Friday", "your refund will be processed within 3 to 5 business days", "I'll call you tomorrow with an update". Nothing in Jira knows these were said. The work item's due date is the team's own plan, an SLA measures how fast the team responds, and neither is the thing the customer was told.

So the promise lives in one person's memory. Friday comes, the customer has heard nothing, and the first anyone notices is the follow-up asking where the fix is. Most broken promises are not broken because the work was hard. They are broken because nobody saw the date coming.

## What the app does

1. **Reads each new comment for a promise.** A promise is a sentence that commits the team to something and names a date. The app works out the day the words mean from the day the comment was written: "by Friday", "tomorrow", "within 3-5 business days", "by EOD Monday", "the end of November".
2. **Tracks firm promises and suggests the rest.** "We will send the report by Friday" is tracked at once. "This should be fixed next week" is an expectation with a vague date, so it is shown as a suggestion for a person to confirm or dismiss. A suggestion nobody confirms is dropped two weeks after its date, or when the work item is finished.
3. **Shows them on the work item.** The Promised panel lists what was promised, by whom and for when, with buttons to record what happened: Kept, Move the date, Broken, Withdraw. A promise made on a call can be added by hand.
4. **Reminds before the date passes.** The day before, on the day, and once after, the app adds a note to the work item that mentions the assignee. On service projects the note is internal, so the customer never sees it.
5. **Settles promises when the work is finished.** Finished on or before the promised day counts as kept; finished later counts as broken, with the number of days.
6. **Shows the whole picture.** The Promised page lists every open promise by urgency, with the totals: overdue, due today, due in the next seven days, and the share that were kept, overall and by person. A dashboard gadget shows the same at a glance.
7. **Makes promises searchable.** `issue in promisesDueWithin(3)` finds work items with an open promise that is overdue or due within three days, for filters, boards and automation rules.
8. **Answers questions.** The Promised agent in Rovo answers "what have we promised that is due this week?" and "what did we promise on this work item?" from the recorded promises, and records what happened when told.

## What counts as a promise

| Comment | What the app does |
|---|---|
| "We will have a fix out by Friday." | Tracks it, due Friday |
| "Our billing team will issue the refund within 3-5 business days." | Tracks it, due on the fifth working day |
| "Sam will call you by end of day tomorrow." | Tracks it, due tomorrow |
| "You should receive the refund within 5 business days." | Suggests it: an expectation, not a commitment |
| "We will try to get this done by Friday." | Suggests it: hedged |
| "Once we have your logs, we will send a fix by Friday." | Suggests it: depends on a condition |
| "We will ship the fix next week." | Suggests it: the date is vague, read as that Friday |
| "We will deliver it by 12/04." | Suggests it: could be December 4 or 12 April |
| "Please send us the logs by Friday." | Nothing: a request to the customer |
| "We won't be able to fix this by Friday." | Nothing: a refusal |
| "We will refund the charge from Nov 2." (written on November 4) | Nothing: the date is in the past |
| "I will send you the logs by Friday." (written by the customer) | Nothing: not the team's promise |

Every tracked promise keeps the sentence it came from, the words that were read as the date, and the reason it was read as a promise, so a person can check the reading at a glance.

Detection is deliberately cautious. A promise the app missed can be added by hand in a few seconds. A promise it invented would make people stop trusting the reminders.

## Why rules and not a language model

- **The same comment always gives the same answer**, and the app can say why. A reminder that fires on a date nobody wrote is worse than no reminder.
- **Nothing leaves Atlassian.** Comments are read inside Forge. The manifest declares no outside addresses, so the platform itself blocks any call out.
- **It costs nothing to run** on every comment in a busy service project.

The Rovo agent then works from the recorded promises instead of re-reading comments, which keeps its answers consistent with the panel, the reminders and the search.

## For agents

Five actions are available to the Promised agent and to any other Rovo agent: `list-promises`, `get-promises-for-work-item`, `promise-summary`, `record-promise` and `update-promise`. The three read-only ones are also exposed through the Atlassian MCP server (`rovo:mcp`) for assistants outside Atlassian.

`skills/keep-promises/SKILL.md` is an open skill file. It teaches an agent that drafts customer replies to check what was already promised first, so the reply does not contradict it, and never to hide a missed date.

## Forge modules used

| Module | What it does here |
|---|---|
| `trigger` (2) | Reads each new comment; settles promises when a work item is finished |
| `scheduledTrigger` | The daily check: reminders, and keeping the search function current |
| `jira:issuePanel` | The Promised panel on every work item |
| `jira:globalPage` | Open promises, totals, and setup |
| `jira:dashboardGadget` | "Promises due" gadget |
| `jira:entityProperty` | Indexes the next due date, the number of open promises and the status for JQL |
| `jira:jqlFunction` | `issue in promisesDueWithin(3)` |
| `rovo:agent` | The Promised agent |
| `action` (5) | The tools the agent uses |
| `rovo:skill` | `keep-promises` |
| `rovo:mcp` | Read-only tools for agents outside Atlassian |
| Forge key-value storage | Settings |

The promises themselves are stored on the work item, as an entity property. They move, archive and delete with it, and Jira's own permissions decide who can see them.

## Getting started

Install the app from the Atlassian Marketplace (a Jira administrator does this under Apps > Explore more apps). Then in Jira:

1. Open **Apps > Promised** and go to **Setup**.
2. Choose a project and press **Create the sample requests**. This creates six support requests for an invented company, with promises that are overdue, due today, kept and broken, and posts replies on three of them.
3. Open the **Promises** tab to see them by urgency, with the totals and the breakdown by person.
4. Open one of the sample work items. The Promised panel shows its promises. Try **Kept**, **Move the date** and **Add a promise**.
5. Add a comment of your own, such as "We will send the corrected invoice by Friday", and reopen the panel.
6. In Jira search, run `issue in promisesDueWithin(3)`.
7. In Rovo chat, choose **Promised** and ask "What have we promised that is due this week?"

The daily check runs once a day. Reminders appear for promises due the next day, due that day, or newly overdue.

To use the tools from an outside agent, an administrator turns them on under Atlassian Administration > Apps > Sites > your site > Connected apps. The endpoint is `https://mcp.atlassian.com/forge/<appId>`.

## Settings

| Setting | Default | What it does |
|---|---|---|
| Read only comments the customer can see | On | On service projects, internal notes are not read |
| Post reminders | On | Adds the reminder notes described above |
| Read numeric dates day first | Off | Reads 03/04 as 3 April instead of March 4 |
| Time zone | That of the first person who opens the app | Decides which day a comment was written on, and when a promise is due and overdue |

Only a Jira administrator can change them.

## Limits worth knowing

- English only.
- Comments only. A promise made in a description, an email or a call is added by hand, or by telling the agent.
- An edited comment is not read again on its own. **Read the comments again** on the panel does it.
- Working days are Monday to Friday. Public holidays are not known.
- A work item holds up to 20 promises.
- The record is one value on the work item. If two comments with promises arrive in the same instant, the later write can win; **Read the comments again** recovers the other.
- The kept rate by person is a count, not a judgement. Someone who makes more promises has more to keep.

## Privacy

The app stores, on each work item, the sentence that held the promise, the due date, who wrote it and what became of it. Anyone who can open the work item in Jira can see its promises. The customer portal of a service project does not show them. Settings are kept in Forge storage. Nothing is sent outside Atlassian.

Reminders are internal notes. Comments written by service-project customers and by apps or automation rules are not read.

All sample data is synthetic.

## Third-party components

Runtime dependencies are the Forge SDK packages (`@forge/api`, `@forge/bridge`, `@forge/kvs`, `@forge/react`, `@forge/resolver`) and React.

---

Support: see the [Promised privacy and support page](../promised). Email vinit@vinitshah.dev.
