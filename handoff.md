# Handoff: privacy policy and support

*Last updated: November 8, 2026.*

Handoff is a Forge app for Jira Cloud, built by Vinit Shah for Atlassian Codegeist 2026. It builds a handoff brief for a person going on leave from the Atlassian Teamwork Graph, lets the team mark work items as covered, and shows what changed when the person is back.

## What the app reads

When someone builds a brief, the app reads, through the Teamwork Graph API and Jira as the signed-in person, what that person could already see: work items assigned to or reported by the person on leave, their recent work, pull requests, Confluence pages and blog posts they created, goals and projects, calendar events linked to their account, and the teams they belong to. Nothing is read with elevated rights; a source the person cannot see comes back empty.

## What the app stores

Inside the Atlassian site it is installed on, the app stores:

- A snapshot of each brief in Forge storage: the person's name and account id, the leave dates, who built it, the keys, summaries, statuses, assignees and due dates of the work items in the brief, and who covers which item. It is used to show who is away and to work out what changed when the person returns. It is removed when someone marks the person as back, and a week after the return date by a daily job.
- A cover mark on each covered work item, as a Jira entity property: the account ids and names of the person away and the person covering, the leave dates, and whether the item was reassigned. It is indexed so JQL can find covered items. It is removed when the handoff ends or the work item is deleted.
- A comment on each covered work item saying who is away until when and who covers, and, if chosen, a change of assignee. These are ordinary Jira changes made as the person using the app.
- Optionally, a work item holding the brief, created in a project the user chooses.

## Personal data

Snapshots and cover marks hold Atlassian account ids and display names: the person away, who built the brief, the assignees of the work items in it, and the people covering. Email addresses are not stored. Once a week the app reports the stored ids to Atlassian through the Personal Data Reporting API. When Atlassian reports an account as closed, the app deletes that person's own handoff (its snapshot and its cover marks), removes their id elsewhere and shows them as "Former user" where they were covering. When Atlassian reports an account as updated, the app refreshes the stored name. Comments the app posted and brief work items it created are Jira content and follow Jira's own handling of closed accounts.

## Where data goes

The app runs entirely on Atlassian's Forge platform. It declares no external addresses, so the platform blocks any call to a service outside Atlassian. The Rovo agent and the MCP tools return the same information to the person asking; the app calls no language model of its own.

## Permissions

Jira: read and write work items (comments, assignee, properties, creating the brief), read users (to search people and show names), app storage, and the personal data report (`report:personal-data`). Teamwork Graph: read-only scopes for Jira work items, comments and statuses, Jira projects, Atlassian users and teams, Confluence pages, blog posts and spaces, Atlassian goals and projects, external pull requests and external calendar events. Every action a person takes in the app runs with that person's own permissions.

## Removal

Uninstalling the app removes its Forge storage. Cover marks on work items are removed when a handoff ends or by Jira administrators through the work item's properties; comments and the saved brief are ordinary Jira content and stay unless deleted.

## Support

Questions and problems: vinit@vinitshah.dev. Security issues: see the [security and incident response page](security).
