# Recheck: privacy policy and support

*Last updated: November 8, 2026.*

Recheck is a Forge app for Confluence Cloud, built by Vinit Shah. It finds pages that nobody has edited or confirmed for a while, shows each page's review state under its title, lets people mark a page reviewed or snooze it, lists stale pages per space, and can remind page owners once a week.

## What the app stores

For each page someone reviews, snoozes or gives its own interval, the app keeps one record in Forge storage inside your Atlassian site: the page and space ids, when it was last reviewed and by whom (an Atlassian account id), an optional note, the page's own review interval, a snooze date, and when its owner was last reminded. Space settings (the review interval, the "due soon" window, and whether reminders are on) are stored per space. No page content is stored.

## What the app reads and changes

The app reads page titles, owners and last-edit dates, with the signed-in person's permissions when they use it and with its own permissions for the state under the title and the weekly reminders. When a space turns reminders on, the app posts a footer comment on newly stale pages that mentions the page owner, at most 20 pages per space per week. It never edits, restricts, moves, archives or deletes pages.

## Personal data

Review records hold the Atlassian account id of the person who last reviewed each page, with their optional note. Page owners are read from Confluence each time and not stored. Once a week the app reports the stored ids to Atlassian through the Personal Data Reporting API. When Atlassian reports an account as closed, the app removes that person and their note from the records and keeps the review dates, so pages keep their state. Reminder comments the app posted are Confluence content and follow Confluence's own handling of closed accounts.

## Where data goes

Nowhere outside Atlassian. The app has no servers of its own, declares no external endpoints, and uses no analytics, telemetry or language models.

## Permissions

`storage:app` for the records and settings; `read:page:confluence` to read page titles, owners and last-edit dates; `write:comment:confluence` for the optional reminder comments; `read:confluence-content.summary` and `write:confluence-content` only because Confluence requires them for the page-trashed and page-deleted events the app uses to delete its records; `report:personal-data` for the weekly personal data report.

## Removal

Trashing or deleting a page deletes its record. Uninstalling the app deletes all of its storage.

## Support

Email vinit@vinitshah.dev. Security reports go to the same address and are answered within two business days. Fixes ship as new versions, which Forge rolls out automatically.
