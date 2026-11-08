# Handoff documentation

Handoff builds the brief of everything someone leaves behind when they go on leave, from the Teamwork Graph, helps the team assign cover, and shows what changed when the person is back. Open it from Apps > Handoff in Jira.

## Build a brief

Choose the person and the first and last day away, then press **Build the brief**. Handoff reads the Teamwork Graph as you, with your own permissions, and shows:

- **In flight**: open work items assigned to the person, with status, due date and assignee.
- **Due while away**: the items among them whose due date falls inside the leave. These are preselected for cover.
- **Waiting on others**: open items the person reported that are assigned to someone else.
- **Recent work, pull requests, pages, goals, meetings and teams**, each as a short list with links.

Sources your site does not have (for example pages when Confluence is not connected, or goals without Atlas) are listed as "not available"; the rest of the brief still works.

## Assign cover

Under the brief, tick the work items that need cover, pick the covering person (suggestions come from the person's teams and from the people already on the work; anyone can be searched) and press **Assign cover**. Each covered item receives:

- a comment that mentions the person away and the covering person, with the dates and your note;
- a cover mark stored on the work item, searchable with JQL: `handoffCover is not EMPTY`, `handoffAway = <account id>`, `handoffUntil < endOfMonth()`;
- optionally the covering person as the new assignee (the **Reassign** toggle).

A panel on each covered work item shows who is away until when and who covers. It appears only while the mark is present.

## Save the brief as a work item

Choose a project and a work type and press **Save as a work item**. The brief, with every section and link, becomes a work item that can be shared, watched or attached to the leave request.

## Who is away

The tab lists everyone with a handoff on record, the days left, who covers, and a button to end the handoff early. Handoffs expire by themselves a week after the return date.

## Back from leave

Pick the person who is back and press **What changed while they were away?** Handoff compares a snapshot taken when the brief was built with the graph now, and lists: new work items assigned while away, items resolved, items whose status changed, items reassigned, and new comments from other people.

## The Handoff agent in Rovo

The free edition shared by installation link includes a Rovo agent (the Marketplace edition does not yet). Choose the **Handoff** agent in Rovo chat and ask, for example:

- "I am off from Monday for two weeks, what do I need to hand over?"
- "Who is away?"
- "Let Priya cover PAY-12 and PAY-15 for Sam until the 20th"
- "What changed for Sam while they were away?"

The same read-only tools are available to coding agents through the Atlassian MCP server once a site administrator enables them.

## Data and privacy

Handoff keeps one record per handoff in Forge storage (the person, the dates, the covering people, the work item keys and a snapshot of the brief) and a cover mark on each covered work item. Nothing leaves Atlassian. See the [privacy policy](../handoff).

## Support

Email vinit@vinitshah.dev. Fixes ship as new versions, which Forge rolls out automatically.
