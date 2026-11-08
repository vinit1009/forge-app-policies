# Ratecard: privacy policy and support

*Last updated: November 8, 2026.*

Ratecard is a Forge app for Jira Cloud, built by Vinit Shah. It turns the time logged on Jira worklogs into cost, using hourly rates that a Jira administrator sets, and shows cost and budget burn per project, epic, work item, person and month.

## What the app stores

In Forge storage inside your Atlassian site: the rate table (a currency, a default hourly rate and per-person hourly rates, each with the month it starts, keyed by Atlassian account id), the group allowed to see costs (its id and name), project and epic budgets (amount and start month), and a five-minute cache of each project's cost summary. Worklogs themselves are not copied; they are read from Jira when a screen opens.

## Who can see what

Only Jira administrators see rates and per-person costs. Project and work item costs are visible to Jira administrators and, if an administrator chooses one, to members of one group. Everyone else sees a notice instead of numbers. All screens read Jira with the signed-in person's own permissions, so nobody sees worklogs of work items they cannot browse.

## Personal data

The rate table holds Atlassian account ids. Once a week the app reports these ids to Atlassian through the Personal Data Reporting API and deletes the rates of any account that has been closed. To keep pages fast, the app also caches each computed cost view, which includes people's names and per-person costs, for five minutes; cached views expire after an hour and Forge deletes expired entries within 48 hours.

## Where data goes

Nowhere outside Atlassian. The app has no servers of its own, declares no external endpoints, and uses no analytics, telemetry or language models.

## Permissions

`read:jira-work` to read worklogs, work items, projects and the signed-in person's permissions; `read:jira-user` to show people's names and check group membership; `storage:app` for the rates, budgets, access setting and cache; `report:personal-data` for the weekly personal data report.

## Removal

Removing a budget or a rate deletes it. Uninstalling the app deletes all of its storage.

## Support

Email vinit@vinitshah.dev. Security reports go to the same address and are answered within two business days.
