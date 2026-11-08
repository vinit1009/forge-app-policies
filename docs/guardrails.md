# Guardrails documentation

Guardrails adds the workflow rules most teams need to Jira's workflow editor. Open a workflow, select a transition, choose **Add rule**, and pick a Guardrails rule from the Marketplace rules list. Each rule has a short settings form; what you choose is shown next to the rule in the editor.

## Validators (block the transition unless...)

- **Required fields**: every chosen field has a value. Works with the values entered on the transition screen.
- **Comment required**: a comment is added on the transition screen. Give the transition a screen that includes the comment field.
- **Field matches a pattern**: a text, option or user field matches a regular expression, for example a ticket reference in the summary.
- **Related work must be finished**: subtasks, linked work items of chosen link types, or the parent are in a Done status category.
- **Date check**: a date field is today or later, or after another date field.

Each validator takes an optional message shown to the person when the transition is blocked. If a rule cannot be evaluated, for example because a field was deleted, it lets the transition through and writes a log entry rather than locking the workflow.

## Conditions (hide the transition unless...)

- **Only these people**: the assignee, the reporter, the project lead, or named people.
- **Field has one of these values**: priority, work type, labels, components, fix versions or resolution.
- **All subtasks are done**, **Linked work is done** (optionally for chosen link types), **Has an attachment**.

Conditions are Jira expressions evaluated by Jira itself, so they cost nothing and apply everywhere the transition is offered, including the REST API and automation.

## Post functions (after the transition)

- **Set the assignee**: the reporter, the project lead, the person making the transition, a named person, or nobody.
- **Set fields**: resolution, add or remove labels, clear fields, or set the due date a number of days ahead.
- **Add a comment** from a template. Placeholders: `{{issue.key}}`, `{{issue.summary}}`, `{{issue.status}}`, `{{issue.assignee}}`, `{{issue.reporter}}`, `{{issue.priority}}`, `{{transition.from}}`, `{{transition.to}}`, `{{user.displayName}}`, `{{today}}`. Comments can be internal notes on service projects.
- **Transition related work**: move the parent, the subtasks or linked work items to a status, for example closing subtasks when the parent closes, or closing the parent once the last subtask is done.
- **Add a watcher**: the reporter or a named person.

Post functions run after the transition has happened. A post function that fails is logged and does not undo the transition.

## Notes

- Works in company-managed and team-managed projects.
- Rules run as the app. People do not need permission to see what a validator checks.
- Support: vinit@vinitshah.dev.
