# Guardrails: privacy policy and support

*Last updated: November 8, 2026.*

Guardrails is a Forge app for Jira Cloud, built by Vinit Shah. It adds workflow validators, conditions and post functions to Jira's workflow editor: required fields, comment required, field patterns, related work finished, date checks, who may move a work item, field-value conditions, and post functions that set the assignee, set fields, add comments, move related work items and add watchers.

## What the app stores

The only thing the app stores is the configuration of each rule, which Jira keeps with the workflow (field names and ids, patterns, messages, comment templates, label names, status names, and the account ids and display names of people chosen in a rule). The app has no storage of its own and keeps no copies of work items.

## What the app reads and changes

When a transition runs, Jira calls the app with the work item key, the transition and the rule's configuration. Validators read the work item's fields, subtasks, links and parent to decide whether the transition may proceed and return a message when it may not. Conditions are evaluated by Jira itself from a Jira expression. Post functions read the work item and then, as configured, change its assignee, resolution, labels, other fields or due date, add a comment, add a watcher, or transition related work items. Settings screens read the site's fields, link types, statuses, resolutions, priorities and work types, and search people by name, as the administrator editing the workflow.

## Where data goes

The app runs entirely on Atlassian's Forge platform. It declares no external addresses, so the platform blocks any call to a service outside Atlassian. The app calls no language model.

## Permissions

Jira: read and write work items, read users, manage Jira configuration (required by Jira for workflow rule settings). Rule evaluation runs as the app; settings screens run as the administrator.

## Removal

Uninstalling the app removes its rules from the workflows that used them, following Jira's handling of app-provided workflow rules; nothing else is left behind.

## Support

Questions and problems: vinit@vinitshah.dev. Security issues: see the [security and incident response page](security).
