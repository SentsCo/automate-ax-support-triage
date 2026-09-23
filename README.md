# Triage support emails into Linear and Slack

A new Inbox message in a dedicated Gmail support account starts this Automate.ax automation. Platform AI returns a short title, summary, category, and priority. The automation creates a Linear issue, then posts the issue link and summary to Slack. The Slack step depends on the created issue, so it cannot post a link before the issue exists.

This is a starting point for a human support queue. Review the AI summary and priority before acting on a customer request. The automation does not reply to the sender or close the email.

## Set it up with a coding agent

Copy the prompt from [the article](https://automate.ax/articles/triage-support-emails) into your coding agent. The prompt points to this repository and asks the agent to initialize, typecheck, and deploy it. Tell the agent which dedicated Gmail support account, Linear team, and Slack channel to use. During deployment, connect the three accounts and set the Linear team ID and Slack conversation ID in Parameters & Accounts. The Slack bot must be able to post in that channel.

The `generate` action uses Automate.ax Platform AI by default. It receives the sender address, subject, and up to 6,000 characters of the message body. Its model use counts toward your organization's Platform AI allowance. No separate AI provider key is required.

## Manual setup

```sh
git clone https://github.com/SentsCo/automate-ax-support-triage.git
cd automate-ax-support-triage
bun install
bunx automate.ax login
bunx automate.ax init
bun run typecheck
bunx automate.ax deploy
```

Create a new Automate.ax project when `init` prompts you. Connect Gmail, Linear, and Slack in Parameters & Accounts, then set the two IDs. Credentials stay in Automate.ax, outside this repository. Every new Inbox message in the connected account starts the automation after deployment; older messages are not replayed. Do not connect a personal or shared mailbox with unrelated mail.

## Check the handoff

Send a clearly labeled synthetic support email with disposable details to the connected inbox. Look for a Linear issue with the sender, subject, Gmail message ID, AI category, and summary. Check that the Slack message links to that issue. Review the generated title and priority. If either action fails, inspect the run in Automate.ax and verify the connected accounts, team ID, and channel access.

Change the project parameters to reuse the same code for another Linear team or Slack channel. Edit the automation if you need different categories, priority rules, or message content. Automate.ax deduplicates repeated Gmail notifications for one message, but downstream actions can still fail or be retried; inspect runs before treating the handoff as exactly once.
