# Readout: privacy policy and support

*Last updated: November 8, 2026.*

Readout is a Forge app for Jira Service Management Cloud, built by Vinit Shah. It gives customers a Service report in the customer portal (their own requests, or the requests shared with an organization they belong to: counts, resolution times, and the service levels a project chooses to publish), and shows published service levels on each request's page in the portal.

## What the app reads

- **For a customer**, with that customer's own permissions: the service projects they can use, the organizations they belong to, and the requests the portal already shows them (requests they raised or take part in, and requests shared with their organizations): key, summary, request type, status, created date and, on organization tabs if the project allows it, who raised each request.
- **For those request keys only**, with the app's permissions: the resolution date, and only what a project administrator has published: chosen SLA fields, the satisfaction rating (shown as an average) and time spent. The app never reads a request the customer could not already open in the portal.
- **For a project administrator** on the settings page: their own project permissions, the project's statuses and organizations, and the site's list of SLA and satisfaction fields.

## What the app stores

Only each service project's settings, in Forge storage inside your Atlassian site: whether reports are on, which SLA fields are published and the label customers see, whether satisfaction and hours are shown, whether organization tabs are on and an optional list of allowed organization ids, whether requester names are shown, which statuses count as waiting on the customer, the default period and the request limit. Reports are computed when a customer opens them and are not stored or cached.

## Personal data

None is stored. Names, account ids and request contents are read when a report is opened and are never written to storage, so the app has nothing to report to Atlassian's personal data reporting API.

## Where data goes

Nowhere outside Atlassian. The app has no servers of its own, declares no external endpoints, and uses no analytics, telemetry or language models. The CSV export is built for the customer who asked for it and downloaded in their browser.

## Permissions

`read:servicedesk-request` to list the service projects, request types and requests a customer can see; `read:organization:jira-service-management` to list the organizations a customer belongs to; `read:servicedesk.organization:jira-service-management` to list a project's organizations on the settings page; `read:jira-work` to read the resolution date and published fields of requests the customer can see, the field list, project statuses and the administrator's permissions; `storage:app` for the settings. The app asks for no write or manage permissions.

## Removal

Turning reports off hides them at once. Uninstalling the app deletes all of its storage.

## Support

Email vinit@vinitshah.dev. Security reports go to the same address and are answered within two business days. Fixes ship as new versions, which Forge rolls out automatically.
