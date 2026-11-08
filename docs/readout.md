# Readout documentation

Readout gives your Jira Service Management customers a Service report in the customer portal: what they asked for, how fast it was resolved, and how you did against the service levels you choose to publish. Nothing shows until a project administrator turns it on.

## Turn it on

Open the service project's **Project settings > Apps > Customer reports** (project administrators only).

- **Show the Service report to this project's customers**: the main switch. Off by default.
- **Service levels to publish**: tick the SLAs customers may see, for example Time to first response and Time to resolution, and give each the label customers see.
- **Other figures**: the average satisfaction rating (never per request on organization tabs) and hours spent.
- **Organizations**: a tab for each organization a customer belongs to, optionally only for the organizations you tick, and whether those tabs show who raised each request.
- **Report**: the period shown first (last 30 days, 90 days, 12 months or all time), the most requests one report reads (50 to 1,000, newest activity first), and which statuses count as waiting on the customer.

## What customers see

In the portal, the profile menu (their avatar) gets **Service report**. It opens a report for each service project that turned reports on:

- **My requests**: requests they raised or take part in. One more tab per organization, with the requests shared with that organization.
- **Tiles**: open now, waiting on them, created and resolved in the period, the typical (median) resolution time, the time within which 9 in 10 requests were resolved, and each published SLA as a share met with its met and breached counts. Satisfaction and hours appear only if published.
- **Charts**: created and resolved per week, month or year; open requests by status; requests by type.
- **Table and CSV**: every request in the period with its status, created date, resolution time and published SLA results. **Export CSV** downloads the same rows; if the browser blocks the download, the CSV appears in a box to copy.

Each request's page in the portal also gets a **Service levels** panel with the published SLAs: met, breached, running with the time left, or paused, with the goal.

## Who sees what

A customer only ever sees requests the portal already shows them. Organization tabs use Jira Service Management's own sharing: the requests shared with that organization, which its members can already open. Readout reads SLA results, the resolution date and published figures only for those requests.

## Limits

A report reads up to the request limit you set, starting with the most recently active requests; the footer says when older requests were left out. Times are calendar time from creation to resolution; SLA results use your SLA calendars.

## Data and privacy

Readout stores only each project's settings. See the [privacy policy](../readout).

## Support

Email vinit@vinitshah.dev.
