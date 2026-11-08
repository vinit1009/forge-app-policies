# Denial Desk: privacy policy and support

*Last updated: November 6, 2026.*

Denial Desk is a Forge app for Jira Cloud, built by Vinit Shah for Atlassian Codegeist 2026.

## What the app stores

The app stores, inside the Atlassian site it is installed on, the denial work items it creates from a remittance file: the claim number, dates of service, the billed and paid amounts, the payer, the reason codes, and the patient name and member number that the remittance carries. Settings are kept in Forge storage for that site.

The patient details appear only in the Denial Desk panel on a work item, to people who can open that work item. Work item titles and, by default, descriptions do not name the patient. The remittance file itself is not kept: parsed claims are held in Forge storage only until the import finishes, and anything from an abandoned import is deleted by the daily check.

## Personal data

Forge storage holds Atlassian account ids only to tie a file import to the person running it: a pointer to that person's latest import, and the import sessions and uploads themselves, which are deleted when the import finishes or by the daily check. Records on work items hold no account ids; the assignee is read from Jira each time. Once a week the app reports the stored account ids to Atlassian through the Personal Data Reporting API and deletes the pointer, sessions and uploads of any account that Atlassian reports as closed.

## Where data goes

The app runs entirely on Atlassian's Forge platform. It declares no external addresses, so the platform blocks any call to a service outside Atlassian. Nothing is sent to the developer or to any third party. The developer has no access to any customer's site or data.

## Permissions

The app asks only for the Jira scopes it needs to read and write work items and their properties, for Forge storage, and for `report:personal-data` to send the weekly personal data report. Every action a person takes in the app runs with that person's own Jira permissions.

## Removal

Uninstalling the app removes its Forge storage. Records stored on work items are removed with the work items, or by the app's own actions.

## Support

Questions and problems: vinitshah209@gmail.com.
