---
title: Denial Desk documentation
---

# Denial Desk

A Forge app for Jira that turns a health payer's remittance file into tracked appeal work, with the deadline on every denied claim.

## The problem

When an insurer does not pay a medical claim, the practice has a limited window to appeal, and the window differs by payer. The denials arrive inside a remittance file (an X12 835) that mixes them with hundreds of routine adjustments. Billing teams pull them out by hand into spreadsheets, look up what each reason code means, and track the dates themselves. When a date is missed, the money is gone.

## What the app does

1. **Reads the remittance file.** Upload or paste an 835. The app parses it inside Forge, checks that it adds up, and separates denials from routine adjustments (the contractual write-off, the patient's deductible and copay).
2. **Creates one Jira work item per denial.** Each has the payer deadline as its due date, the reason in plain language, the recommended next step, and a packet checklist.
3. **Shows where every deadline comes from.** Deadlines are computed from payer rules that a site maintains. Each date shows its arithmetic, the rule behind it, and whether that rule has been verified. A payer with no rule gets a clearly marked placeholder.
4. **Drafts the letter.** Appeal letters, corrected claim notes and records cover letters are built from the facts on the remittance. Anything the file cannot know is left as a marked blank. Nothing is invented.
5. **Tracks the outcome.** Mark a denial as sent and the due date moves to the day to check back. Record the payer's decision and the dashboard shows dollars recovered and the overturn rate.
6. **Answers questions through Rovo.** The Denial Desk Assistant agent lists what is due, explains a denial, and drafts letters, using actions that return computed facts.

## Forge modules used

| Module | What it does here |
|---|---|
| `jira:globalPage` | The Denial Desk page: work queue, import, payer rules, settings |
| `jira:issuePanel` | The panel on each denial work item, shown only when a denial record exists |
| `jira:dashboardGadget` | "Denials at risk" gadget |
| `jira:entityProperty` | Indexes nine values from each denial for JQL, for example `denialAmount > 500 AND denialStage = "open"` |
| `jira:jqlFunction` | `issue in denialsDueWithin(7)`, kept current by the daily check |
| `jira:workflowValidator` | Optional "Denial packet is complete" validator |
| `rovo:agent` | Denial Desk Assistant |
| `action` (8) | Tools for the agent: list, summarize, get, explain a code, draft a letter, save it, mark sent, record the decision |
| `rovo:skill` | `work-a-denial`, a reusable procedure for taking one denial from to-do to sent |
| `rovo:mcp` | Exposes the five read-only tools to outside agents through the Atlassian MCP server |
| `scheduledTrigger` | Daily check: deadline reminders, due date sync, JQL function refresh |
| Forge key-value storage | Payer rules, settings, and import sessions |

No external services are called. The manifest declares no egress.

## Getting started

Install the app from the Atlassian Marketplace (a Jira administrator does this under Apps > Explore more apps). Then in Jira:

1. Open **Apps > Denial Desk**.
2. Go to **Import** and choose **Try it with a sample file**. The sample is synthetic, with dates relative to today.
3. Pick a project and a work type (Task works in any project) and create the work items.
4. Open the **Work queue** tab, then open any work item to see the Denial Desk panel.
5. Open Rovo chat, choose **Denial Desk Assistant**, and ask "What is due this week?"

To use the dashboard gadget, add **Denials at risk** to any Jira dashboard.

To let outside agents use the read-only tools, an administrator turns them on under Atlassian Administration > Apps > Sites > your site > Connected apps. The endpoint is `https://mcp.atlassian.com/forge/<appId>`.

## Patient privacy

- A work item's title never names the patient. By default its description does not either, because titles and descriptions travel in notifications, chat integrations and exports. Patient details appear in the Denial Desk panel, to people who can open the work item. A site can choose to show initials or the full name in descriptions.
- Agent tools that list or summarize denials return no patient identifiers. Only the letter draft does, because a letter to a payer must name the patient.
- The remittance file itself is not kept. Parsed denials are held in Forge storage only until the import finishes, and the daily check deletes anything from an import that was started and abandoned.
- The comments the app adds (deadline reminders, appeal sent, outcome recorded) are internal notes. On a service project they never show in the customer portal.
- All calls made for a person use that person's own Jira permissions.

The sample data is entirely synthetic. An organization that wants to process real patient data in Jira is responsible for having the agreements with Atlassian that its regulations require.

## About the reason codes

Remittance files explain each unpaid amount with claim adjustment reason codes and remark codes. The code numbers are industry identifiers that appear in every file. The labels, explanations and next steps in this app are original plain-language guidance written for billing staff. They are not the official code descriptions, which are published and licensed by X12. A code that is not in the app's library is shown by number and routed to review; the app never guesses what it means.

The built-in Medicare rule comes from federal regulation (42 CFR 405.942, 405.950 and 424.44). Rules for other payers are entered by each site from the payer's provider manual or contract.

## Third-party components

Runtime dependencies are the Forge SDK packages (`@forge/api`, `@forge/bridge`, `@forge/kvs`, `@forge/react`, `@forge/resolver`) and React. The sample file uses HCPCS Level II procedure codes, the alphanumeric code set that CMS maintains. It contains no CPT codes and no dental codes.

---

Support: see the [Denial Desk privacy and support page](../denial-desk). Email vinitshah209@gmail.com.
