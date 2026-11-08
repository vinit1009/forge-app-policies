# Ratecard documentation

Ratecard turns the time logged on Jira worklogs into cost: hours times the hourly rate in force in the worklog's month.

## Set up rates (Jira administrators)

Open **Apps > Ratecard** in Jira settings.

- Choose the **currency**.
- Add a **default rate** and the month it starts. Everyone without their own rate uses it.
- Add **people's rates**: pick a person, enter their hourly rate and the month it starts. Add another entry with a later month for a raise; earlier months keep the old rate.
- Press **Save rates**.
- Under **Who can see costs**, search for a group (for example team leads or finance) and share costs with it. Without a group only Jira administrators see costs. Rates and per-person costs are always administrators only.

## The Cost page of a project

Open **Cost** in the project's sidebar. Choose a period (this month, last month, this quarter, the last 90 days, this year or last year) to see the cost and hours logged, and tabs by epic, by work item, by month and (for administrators) by person.

- **Project budget**: enter an amount and the month it counts from. The burn shows Under budget below 80%, Near budget up to 100%, and Over budget beyond.
- **Export**: press **Show CSV** and copy the text into a spreadsheet. One row per work item, month and (for administrators) person.

## The Cost panel on a work item

Open **Cost** from the app actions of a work item. It shows the item's cost and hours by month. On an epic it totals the epic and its child work items, and the epic can carry its own budget.

## The Project cost gadget

Add **Project cost** to a dashboard, choose a project, and save. It shows this month's and last month's cost, and the budget burn.

## Notes

- Costs come from Jira worklogs. Time logged in Tempo appears in Jira under the Tempo app rather than the person, so it uses the default rate.
- Worklogs restricted from you are not counted on your screens.

## Data and privacy

See the [privacy policy](../ratecard).

## Support

Email vinit@vinitshah.dev.
