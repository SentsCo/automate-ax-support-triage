# Triage support emails into Linear and Slack

A new Inbox message in a dedicated Gmail support account starts this Automate.ax automation. Automate.ax's built-in AI returns a title, summary, category, and priority. The automation creates a Linear issue, then posts the issue link and summary to Slack.

This is a starting point for a human support queue. Review the AI summary and priority before acting on a customer request. The automation does not reply to the sender or close the email.

## Set it up with a coding agent

Copy the prompt from [the article](https://automate.ax/articles/triage-support-emails) into your coding agent. It links to this code and tells the agent to create an Automate.ax project, check it, and turn on the automation. Tell the agent which dedicated Gmail support account, Linear team, and Slack channel to use. When Automate.ax asks you to connect Gmail, Linear, and Slack, authorize them. The agent will handle the project settings and show you how to find any team or channel details it cannot retrieve. The connected Slack bot needs permission to post in your chosen channel.

The automation uses Automate.ax's built-in AI to read the sender address, subject, and up to 6,000 characters of the message body. Its use counts toward your organization's [monthly AI allowance](https://docs.automate.ax/concepts/platform-resources#count-platform-ai-usage). No separate AI account is required.

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

Create a new Automate.ax project when `init` prompts you. When Automate.ax opens the account connection screen, authorize Gmail, Linear, and Slack. Enter the Linear team ID and Slack channel ID as project parameters (settings that choose where issues and messages go). Credentials stay in Automate.ax, outside this repository. Every new Inbox message in the connected account starts the automation after deployment; older messages are not replayed. Do not connect a personal or shared mailbox with unrelated mail.

## Check the handoff

Send a clearly labeled test support email with made-up details to the connected inbox. Look for a Linear issue with the sender, subject, Gmail message ID, AI category, and summary. Check that the Slack message links to that issue. Review the generated title and priority. If a step fails, open its run record in Automate.ax to see what happened and verify the connected accounts, chosen team, and channel access.

Change the project settings to reuse the same code for another Linear team or Slack channel. Edit the automation if you need different categories, priority rules, or message content. Automate.ax ignores repeat Gmail notifications for the same message. Later steps can still fail or retry, so check the run before assuming each email produced one handoff.
