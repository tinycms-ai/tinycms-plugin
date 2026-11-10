---
name: troubleshooting
description: What to do when a tinycms tool refuses or fails. Use when a call answers "Ask first", "Not allowed" or "Waiting for approval", when a publish is refused for a hash or approval reason, when a social channel is disconnected or expired, when a tool is missing from the list, or when the person hits a bug or a limit and wants to tell the tinycms team.
---

# Troubleshooting

## The call answers "Ask first"

The site's owner set this agent to ask before that kind of change. Approval happens in the tinycms app, not in this chat.

1. Call `confirm_agent_action` with `kind` (drafts, surface, delete, or code) and `what`: a plain description of exactly what will change.
2. It answers with an `approvalUrl`. Send that link to the person. They say yes or decline it in tinycms.
3. Once they have, make the original call again within the time the answer gives (minutes, not hours). Never say it is approved yourself.
4. "Waiting for approval" means the request is still open. Send the link again if needed and wait.
5. If the person declined with a note, change the plan to match what they asked before asking again.

For publishing and scheduling under "Ask first", the chat is never enough: say the work is ready, send the preview URL and the `approvalUrl` that `get_article`, `get_page`, `get_forms` or `get_site` returns, and let the person publish it in tinycms.

## The call answers "Not allowed"

This agent may not do that on this site. Tell the person where to change it: the tinycms app, Account → AI Agents, this agent's row. Do not try another way round it.

## Publish or schedule is refused

- **Hash mismatch:** the content changed after the person said yes. Read it again, show the new version with its `workingHash`, and ask again.
- **Approval too old or missing:** `approvedAt` must be within the last 24 hours and must describe a yes given in this chat for this version. Ask again.
- **Blocking findings:** run `run_preflight` and `run_copy_edit`, fix every blocking finding, and run again. Only pass `override` with a reason when the person has explicitly agreed to publish despite them. Held findings cannot be overridden from here: an owner or admin decides in the app.
- **Copy edit required:** the last create or update needs `copyEdit: true`, or run `run_copy_edit` on that exact version.

## A social channel is disconnected or expired

`list_social_accounts` with `includeInactive: true` shows channels that cannot be posted to. A post to such a channel cannot go out. The person reconnects it in the tinycms app under Social › Channels. A campaign keeps its lane for that channel and its cards pause until then. Do not create posts for an expired channel; say which channel needs reconnecting.

## A tool is missing

The tool list follows the site and its plan: Social tools need Pro, and the style guide and voice tools need Enterprise. If a tool the person expects is missing, say which plan it belongs to, and that the owner changes the plan in the app. Each connection is bound to one site: another site needs its own connection.

## Something is wrong or missing in tinycms

Use `send_feedback` to tell the tinycms team about a bug, a limit, a wish, a design change or praise. Something wrong with the site's own content goes to the site's Inbox with `report_issue` instead.

1. Write the exact text you will send: `summary` (one line), `details` (what happened, what would help), `kind` and `priority` (high: security, data loss, site down or they cannot publish; medium: wrong behaviour or a blocked workflow; low: polish or a nice-to-have).
2. Show it to the person and ask whether to send it. Call only after they agree, with `personAgreed: true`. No secrets or private details.
3. If a result carries a `checkIn`, ask that one question once. If they do not want to be asked again, send `stopAsking: true`.

## Still stuck

Say plainly what you did, what was refused, and what the person can do in the app. The help centre is at https://tinycms-help.tinycms.ai.
