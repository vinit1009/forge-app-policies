---
title: Crash Twin documentation
---

# Crash Twin

A Forge app for Jira that recognises the same crash across bug reports by its stack trace, and tells you when a crash that was fixed comes back.

## The problem

The same crash gets reported many times. QA files it as "Checkout fails with a 500", support files it as "Customers cannot order to PO boxes", and an engineer files it as "NullPointerException in shipping quote". The titles have nothing in common, so text-based duplicate finders miss it. The stack traces are the same failure, but they do not look the same either: line numbers shift with every release, a wrapper exception changes the top of the trace, the bundle hash changes, and the thread and library versions differ.

So triage spends time rediscovering known bugs, and a fix that did not hold goes unnoticed because the new report does not look like the old one.

## What the app does

1. **Reads the stack trace in every bug report.** When a work item is created, edited or commented on, the app finds the stack trace in its text and stores a small crash record on the work item. It reads Java and Kotlin, JavaScript and TypeScript (Node, Chrome, Firefox, Safari), Python, .NET and Go.
2. **Fingerprints the crash.** The fingerprint is built from the exception that started the failure and the frames in the team's own code. It ignores what changes between reports: line numbers, library and runtime frames, generated names, bundle hashes, thread names and the error message.
3. **Tells the team.** When a new report matches a known crash, the app comments once: which work items already report it, and whether it was fixed before. On a service project the comment is an internal note, so it never shows in the customer portal.
4. **Spots regressions.** A crash that was closed and is then reported again is marked "Came back after a fix" and sorted to the top.
5. **Answers "have we seen this?"** Paste a stack trace into the Crash Twin page, ask the Rovo agent, or let a coding assistant ask through the Atlassian MCP server. The answer names the work item and says whether the crash is open, fixed, or back.

## For coding agents

The app exposes three tools through the Atlassian MCP server (`rovo:mcp`): `find-known-crash`, `get-crash-for-work-item` and `list-top-crashes`. A developer debugging in an editor can hand the stack trace to their assistant, which asks Jira whether the crash is already tracked and in which version it was fixed, before anyone spends time on it.

`skills/check-known-crash/SKILL.md` is an open skill file that teaches an agent when and how to use those tools. It works with the Rovo agent in this app and can be added to third-party agents.

## Forge modules used

| Module | What it does here |
|---|---|
| `trigger` | Reads a work item when it is created, edited or commented on |
| `jira:issuePanel` | The Crash Twin panel, shown only on work items that contain a stack trace |
| `jira:globalPage` | Crash list, trace lookup, and setup |
| `jira:dashboardGadget` | "Top crashes" gadget |
| `jira:entityProperty` | Indexes the fingerprint, language, exception type, title and time seen for JQL |
| `jira:jqlFunction` | `issue in sameCrashAs("SHOP-12")` |
| `rovo:agent` | The Crash Twin agent |
| `action` (3) | The tools the agent uses |
| `rovo:skill` | `check-known-crash` |
| `rovo:mcp` | The same three tools for agents outside Atlassian |
| Forge key-value storage | Settings |

No external services are called. The manifest declares no egress.

## Getting started

Install the app from the Atlassian Marketplace (a Jira administrator does this under Apps > Explore more apps). Then in Jira:

1. Open **Apps > Crash Twin** and go to **Setup**.
2. Choose a project and press **Create the sample reports**. This creates 15 bug reports for an invented product, in five languages, including a crash that was fixed and came back.
3. Open the **Crashes** tab: 15 reports become 9 crashes, with the regression first.
4. Open one of the sample work items to see the Crash Twin panel.
5. Go to **Look up a trace** and paste a stack trace from any sample report, or one of your own.
6. In Rovo chat, choose **Crash Twin** and ask "Which crashes came back after a fix?"

To use the tools from an outside agent, an administrator turns them on under Atlassian Administration > Apps > Sites > your site > Connected apps. The endpoint is `https://mcp.atlassian.com/forge/<appId>`.

## How matching works

For a chain of exceptions the app uses the one that started the failure: the last "Caused by" in Java, the innermost exception in .NET, the first traceback in Python. For Java it puts back the frames that "... 12 more" stands for, so a wrapped and an unwrapped report of the same failure match.

It then takes the first five frames in the team's own code, most recent call first, with generated parts removed: lambda and anonymous class numbers, proxy class names, async state machine names, bundle content hashes. Recursion is collapsed so the depth does not matter.

When a trace has no frames in the team's own code, the app falls back to library frames and says so, because such a match is weaker.

Crashes with different fingerprints that share most of their path are shown as "similar", never as the same crash.

## Privacy

The app stores a fingerprint and the names of up to twelve frames on each work item. The trace itself stays where the reporter put it. The error message is shown to people who can see the work item and is never used for matching, since messages often contain identifiers and personal data.

All sample data is synthetic.

## Third-party components

Runtime dependencies are the Forge SDK packages (`@forge/api`, `@forge/bridge`, `@forge/kvs`, `@forge/react`, `@forge/resolver`) and React.

---

Support: see the [Crash Twin privacy and support page](../crash-twin). Email vinit@vinitshah.dev.
