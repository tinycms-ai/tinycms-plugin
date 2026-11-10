# tinycms

Run your website and social media from a conversation. tinycms is a content management system for websites and social media made for AI apps. With this plugin, Claude can draft pages, articles and forms on your tinycms site, run the checks, show you a preview on the real site, and publish or schedule once you say yes. On the Pro plan it can also write and schedule social posts and plan campaigns.

Nothing goes live until you say yes. Every publish is recorded with who said yes, when, and the exact version they saw.

## What you need

- A tinycms account. If you don't have one, connecting makes a free one: enter your email and the 6-digit code tinycms sends. More at https://www.tinycms.ai.
- A Claude plan that supports plugins and connectors.

## Install

1. Add the **tinycms** plugin from the Claude directory, or from **Customize › Plugins**.
2. On the plugin's **Connectors** tab, connect **tinycms**. A window opens: enter your email and the code tinycms sends, then pick the site this chat works on. A new account starts with one site for Claude to set up.
3. Start a new chat and ask for something. For example: "Write a page about our opening hours and show me a preview."

In Claude Code, install it in one step:

```
/plugin install tinycms --marketplace tinycms-ai/tinycms-plugin
```

Or run `claude --plugin-dir ./tinycms-plugin` from the folder that holds this one to try a working copy. The skills appear as `/tinycms:working-with-tinycms`, `/tinycms:social-posts`, `/tinycms:site-and-pages` and `/tinycms:troubleshooting`.

Each connection is bound to one site. To work on another site, add another connection and pick that site when you sign in.

## What the plugin does

The plugin bundles the tinycms connector (the MCP server at `https://mcp.tinycms.ai/mcp`) with four skills that teach Claude how to use it well:

- **working-with-tinycms**: draft articles, pages and forms; fix the blocking checks; copy-edit the final text; show the preview link; ask for your yes with the version it refers to before publishing or scheduling.
- **social-posts**: write and schedule social posts on your connected channels, link them to the right article, run campaigns, and make branded images with Prism AI.
- **site-and-pages**: change the site's look, header, footer, navigation and home page; apply a template; add media.
- **troubleshooting**: what Claude does when a call answers "Ask first" or "Not allowed", when a publish is refused, when a social channel has expired, or when you want to send feedback to the tinycms team.

If you already added the tinycms connector on its own, this plugin uses the same server, so you see one set of tools.

## How much Claude may do on its own

Every connected agent starts on **Ask first**: it drafts and proposes, and you say yes in tinycms before anything changes. You can change that per agent in the tinycms app under **Account › AI Agents**. Publishing always needs your yes for the exact version you saw.

## Data

The plugin sends the content you ask Claude to write or change (page text, article text, form fields, social post text, media links and site settings) to your tinycms account through `https://mcp.tinycms.ai`. It reads your site's content, settings, media library, social channels and approval history from the same place. It sends nothing anywhere else, runs no code on your computer, and stores nothing itself. Feedback to the tinycms team is sent only after you have seen the exact text and agreed.

## Privacy Policy

tinycms handles your account and site data as described in its privacy policy at https://www.tinycms.ai/privacy. Terms of service: https://www.tinycms.ai/terms.

## Support

Help centre: https://tinycms-help.tinycms.ai. Problems with the plugin itself: open an issue in this repository.

## License

MIT. See LICENSE.
