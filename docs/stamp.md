# Stamp documentation

Stamp adds page approval to Confluence: ask named people to approve a page, see the state under the page title, and find out when an approved page was edited.

## Request approval

Open the page, choose **Approval** under **Apps** in the page's more-actions menu (the three dots). Pick the approvers, choose whether everyone must approve or one approval is enough, add a due date or a note if you like, and press **Request approval**. The byline under the title changes to **In review 0/N**. If the space allows comments, a page comment mentions the approvers so they are notified.

## Approve or request changes

Approvers open the same **Approval** item. They can add a note and press **Approve** or **Request changes**. When the rule is met the state becomes **Approved vN**, naming the page version that was approved; one request for changes puts the page in **Changes requested**.

## Changes after approval

When the body of an approved page is edited, the state becomes **Changed since approval (vN)** within a few seconds. Changing only the title does not count. Press **Request approval again** to start a new review of the current version; the approved version stays linked from the byline popup.

## The byline

Click the state under the page title to see who requested approval, the approvers and their decisions, the due date, and a link to the approved version.

## The space dashboard

Open **Approvals** under the space's apps in the sidebar. It shows counts by state and a table of every page under approval that you can see, with a switch to show only the pages waiting for your decision.

## Space settings

Space settings > Apps > **Approvals**: default approvers, the default rule, and whether to post the request and decision comments.

## Data and privacy

See the [privacy policy](../stamp).

## Support

Email vinit@vinitshah.dev.
