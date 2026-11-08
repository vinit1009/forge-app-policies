# Stamp: privacy policy and support

*Last updated: November 8, 2026.*

Stamp is a Forge app for Confluence Cloud, built by Vinit Shah. It lets people request approval of a page from named approvers, shows the approval state under the page title, posts comments that mention the people involved, detects edits made after a page was approved, and lists every page under approval in a space dashboard.

## What the app stores

For each page under approval the app keeps one record in Forge storage, inside your Atlassian site: the page and space ids, the page title, the state, who requested approval and when, the approvers' Atlassian account ids with their decisions and notes, the due date and request note if given, the page version numbers involved, and a SHA-256 hash of the page body at request and approval time. Space settings (default approvers, the default rule, whether to post comments) are stored per space. No page content is stored, only its hash.

## What the app reads and changes

The app reads the pages under approval (title, version, body) with the permissions of the signed-in person when they use it, and with its own permissions when it reacts to a page edit. It posts footer comments on those pages when approval is requested or decided, if the space allows it. It never edits, restricts, moves or deletes pages.

## Where data goes

Nowhere outside Atlassian. The app has no servers of its own, declares no external endpoints, and sends nothing to third parties. It uses no analytics, telemetry or language models.

## Permissions

`storage:app` for the records and settings; `read:page:confluence` to read the pages under approval; `write:comment:confluence` to post the request and decision comments; `read:confluence-content.summary` and `write:confluence-content` only because Confluence requires them for the page-updated, trashed and deleted events the app listens to.

## Removal

Removing the approval from a page deletes its record. Trashing or deleting a page deletes its record. Uninstalling the app deletes all of its storage.

## Support

Email vinit@vinitshah.dev. Security reports go to the same address and are answered within two business days. Fixes ship as new versions, which Forge rolls out automatically.
