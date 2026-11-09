---
title: Security and incident response
---

# Security and incident response

This page describes how the Forge apps published by Vinit Shah (Promised, Crash Twin, Denial Desk) are kept secure, and what happens if something goes wrong. It applies to every app listed by this partner on the Atlassian Marketplace.

## How the apps are built

- The apps run entirely on Atlassian's Forge platform. They declare no external endpoints, call no outside services, and store data only in Forge storage and in Jira entity properties on the customer's own site.
- Calls made for a person use that person's own Jira permissions. App-level calls are limited to scheduled checks and event triggers.
- The apps hold no secrets, API keys or credentials. Nothing is logged that could identify an end user beyond work item keys and counts.
- Runtime dependencies are limited to the Forge SDK packages and React. Dependencies are audited with `npm audit` before every release, and a release is not published while a known vulnerability in a production dependency has an available fix.
- Code changes reach the production branch only through pull requests. Source code is kept in private repositories with the Marketplace copy on a separate branch.
- Development happens on encrypted workstations with automatic operating system updates. Account passwords are generated, unique and kept in the macOS keychain.

## Operational practices

These are the practices behind the answers given in Atlassian's partner security questionnaire. They are reviewed at least once a year and whenever the apps change materially.

- **Access control.** One person operates the Marketplace partner account, the GitHub account and the Forge developer console. Two-step verification is enforced on all of them. Accounts, active sessions, API tokens and authorised applications are reviewed quarterly, and anything no longer needed is revoked.
- **Infrastructure and patching.** The apps have no servers of their own. They run on Atlassian Forge, which manages the runtime, operating system, backups and encryption at rest. Forge runtime deprecations are tracked and the apps are moved to a supported runtime before the old one reaches end of support. Workstations run a supported macOS version with automatic updates and full disk encryption.
- **Dependencies and software bill of materials.** Each app's lockfile is its software bill of materials. `npm audit` runs before every release and at least quarterly, and a release does not ship while a production dependency has a known vulnerability with an available fix.
- **Testing before release.** Changes are covered by unit tests and exercised in a Forge development environment before being deployed to production. Production changes are made only through pull requests.
- **Logs.** Forge invocation logs and account security logs are available only to the partner account. Logs never include credentials, tokens or personal data beyond work item keys and counts.
- **Incident response.** The incident plan below is reviewed and walked through at least once a year and after any real incident.
- **Business continuity.** Customer data lives in Forge storage and Jira entity properties on the customer's own site, so the apps hold nothing that needs a separate backup. Recovering the app itself is a redeploy from source control.
- **Compliance.** The apps are reviewed against the Marketplace security requirements and the Forge platform policies at every major release and at least once a year.
- **AI and machine learning.** The apps do not use AI or machine learning models. All logic is deterministic and runs inside Forge; no Atlassian data is sent to any model.

## Reporting a vulnerability

Email **vinit@vinitshah.dev** with the app name, the steps to reproduce, and the impact you believe it has. You will get an acknowledgement within two business days. Please do not test against customer sites you do not own.

## Fix timelines

Confirmed vulnerabilities are fixed within Atlassian's Marketplace security bug fix timelines for cloud apps: critical within 10 days, high within 4 weeks, medium within 12 weeks, low within 25 weeks. Fixes ship as minor versions, which Forge rolls out to every installation automatically.

## If an incident happens

1. **Contain.** The affected capability is disabled or the app version is rolled back on Forge as soon as the problem is understood.
2. **Tell Atlassian.** A P1 ticket is raised with Atlassian's developer support within 24 hours of identifying a security incident that affects customer data, with updates at least every 6 hours until it is contained.
3. **Tell customers.** Affected customers are notified within 72 hours of identification, with what happened, what data was involved, what was done, and what they should do.
4. **Fix and review.** The root cause is fixed, the fix is released, and the cause is written up so it cannot recur.

## Contacts

- Security and incident contact: vinit@vinitshah.dev (Vinit Shah, who also holds the Atlassian ecosystem support account vinit@vinitshah.dev).
- Support for each app: see the app's page on this site.

Last reviewed: 2026-11-07.
