# Syft

Syft tells you which accounts to go after and why, with evidence that is checked for accuracy, filtered for relevance, and cited so you can verify it. This plugin connects Claude, Cursor, and Codex to Syft and adds two skills: prioritizing accounts and a guide to Syft workflows.

Requires a Syft account. [Request access](mailto:support@syftai.com?subject=Syft%20access%20request).

## Set up in Claude

Two steps in the Claude desktop app. The connector gives Claude access to your Syft data. The plugin adds guided workflows on top of it.

### 1. Add the Syft connector

1. Open **Customize** in the sidebar, then **Connectors**.
2. Find **Syft** and select **Connect**. If Syft is not listed, select **Add custom connector** and enter `https://api.syftai.com/mcp`.
3. Sign in with your Syft account when the sign-in window opens.

### 2. Add the Syft plugin

1. Open **Customize**, then **Plugins**.
2. Select **Add**, then **Add marketplace**.
3. Paste `Syft-AI/syft-plugin` in the URL field and select **Sync**.
4. Find **Syft** in the list and select **+** to install it.

### 3. Check the connection

In a new conversation, open the **+** menu, choose **Connectors**, make sure Syft is on, and ask: "Which Syft workspace and role am I connected as?"

## Set up in Grok Bot

Grok Bot installs plugins from the Cursor marketplace.

1. Open plugins and search for **Syft**.
2. Select **Install**.
3. When prompted, sign in with your Syft account.

## Other tools

Syft is a standard MCP server at `https://api.syftai.com/mcp`, and the plugin works in any host that reads Claude plugin marketplaces.

### Claude Code

```sh
claude plugin marketplace add Syft-AI/syft-plugin
claude plugin install syft@syft-plugins
```

Restart Claude Code, run `/mcp`, and authenticate `plugin:syft:syft`. Then use `/syft:prioritize-accounts` or `/syft:syft-guide`.

### Cursor

1. Open **Customize** in the sidebar and find **Syft** in the marketplace.
2. Select **Install** and choose a project or user scope.
3. Open MCP settings, select Syft, and sign in with your Syft account.

Or load it from a checkout: `cursor-agent --plugin-dir /path/to/syft-plugin`.

### Codex

```sh
codex plugin marketplace add Syft-AI/syft-plugin
codex plugin add syft@syft-plugins
```

Then open Codex's MCP settings, select Syft, and authenticate.

### MCP only

To use the tools without the plugin, add the server directly. Sign-in is OAuth; there is no API key.

```sh
claude mcp add --transport http syft https://api.syftai.com/mcp
codex mcp add syft --url https://api.syftai.com/mcp
```

In Cursor, open **Settings** › **MCP** and add a server named `syft` with that URL.

## Try it

- "Who should I be reaching out to this week?"
- "Is [company] worth my time right now?"
- "Give me my top 5 accounts and why."

## Skills

| Skill | What it does |
|---|---|
| `prioritize-accounts` | Ranked list of priority accounts with the reason for each, then next actions |
| `syft-guide` | How to use Syft, which workflow fits your situation, and what to connect |

## Tools

| Tool | What it does |
|---|---|
| `get_top_priority_accounts` | Accounts Syft rates a priority, ranked by score, with a rationale, the value proposition to lead with, and evidence that is checked for accuracy, filtered for relevance, and cited so you can verify it |
| `get_account_priority_history` | How one account's priority score has changed over time |
| `get_account_relevant_context` | Source documents about one account that Syft judged relevant to what you sell |
| `search_accounts` | Look up a company by name or domain |
| `search_contacts` | People at one company, up to 25 |
| `enrich_contacts` | Email, LinkedIn, and work history for 1 to 5 contacts. Spends credits; requires confirmation |
| `whoami` | The connected user, workspace, and role |

Reps see their territory. Managers and admins see the whole workspace, including accounts Syft found that nobody is tracking yet.

## Support and policies

[Support](mailto:support@syftai.com) · [Website](https://syftai.com) · [Privacy](https://www.syftai.com/legal/privacy) · [Terms](https://www.syftai.com/legal/terms) · [MIT license](LICENSE)
