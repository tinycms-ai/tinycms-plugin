---
name: social-posts
description: Write, schedule and manage social media posts and campaigns through a tinycms site's Social channels (X, Bluesky, Threads, Facebook, Instagram, LinkedIn, YouTube, TikTok, Mastodon). Use when the person asks to post about an article, draft a social post, schedule posts or plan a campaign.
---

# Social posts and campaigns

Social is part of the tinycms Pro plan. If `list_social_accounts` and `create_social_post` are not in the tool list, the connected site's plan does not include Social: tell the person and stop.

## Draft a post

1. `list_social_accounts` first. It returns the `socialProfileId` for each connected channel and what each platform accepts (post types, formats, whether media is required). Pass `includeInactive: true` to see disconnected channels, which cannot be posted to.
2. Write the text as plain text. Markdown is stripped. Keep inside the platform's length: on X a link counts as its shortened length and "…" counts as two characters.
3. `create_social_post` with `socialProfileIds`, `text` and, as needed, `postType`, `format`, `mediaUrl` or `mediaAssetId`, `linkUrl` and `scheduleTime`. Omit `scheduleTime` for a draft, which never posts on its own.
4. One post per channel, all or none. YouTube needs a `title`; TikTok needs its own settings, so ask for the privacy choice and never assume one.

## Links

- Link to the article's live address on the site: the site's host from `get_site` plus the article's path from `get_article`. Never link to a source feed, a preview URL or a draft.
- If the article is not published yet, schedule the post for after it goes live.
- Ask whether the post should carry a link at all. An image post without a link is fine when the person only wants to share a thought.

## Schedule and approval

1. `scheduleTime` takes ISO-8601 with a UTC offset, epoch milliseconds or `"now"`. It must be in the future.
2. On an "Ask me first" channel (the default) a scheduled post waits for the person. The answer carries an `approvalUrl`: send it to them. They publish or ask for changes in tinycms, not in this chat. Never say a post is approved yourself.
3. `update_social_post` edits a draft, scheduled or missed post. `unschedule_social_post` sends one back to draft. Statuses from `list_social_posts`: waiting, skipped, draft, scheduled, due, missed, publishing, published.
4. Each post is checked against the site's rules. A blocking finding holds it until fixed or the person decides. A warning never holds a post: fix it or mention it.

## Campaigns

- `find_campaigns` lists them. `save_campaign` creates one (give `name`, `goal`, `plan`, `endDate`) or edits one; only the fields you pass change.
- An always-on campaign repeats from the site's articles under its `rules` (words to include or exclude, how old an article may be, times and days). A dated campaign has a board of work and a colour.
- Pass `campaignId` on a post that belongs to a campaign.
