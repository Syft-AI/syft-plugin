# Syft

Syft tells you which accounts to go after and why, with evidence that is checked for accuracy, filtered for relevance, and cited so you can verify it. This plugin connects Claude, Cursor, and Codex to Syft and adds a skill for prioritizing accounts.

Requires a Syft account. [Request access](mailto:support@syftai.com?subject=Syft%20access%20request).

## Install

This package supports custom installation before catalog availability. The public GitHub repository is not available yet; the release commands below are for after publication, not a claim of a marketplace listing.

### Claude Code

Release installation, once `Syft-AI/syft-plugin` is published:

```sh
claude plugin marketplace add Syft-AI/syft-plugin
claude plugin install syft@syft-plugins
```

Local checkout installation, available now (replace `/absolute/path/to/syft-plugin`):

```sh
claude plugin marketplace add /absolute/path/to/syft-plugin
claude plugin install syft@syft-plugins
```

### Cursor

Load the local checkout in Cursor Agent:

```sh
cursor-agent --plugin-dir /absolute/path/to/syft-plugin
```

### Codex

Install from the local checkout with Codex CLI:

```sh
codex plugin marketplace add /absolute/path/to/syft-plugin
codex plugin add syft@syft-plugins
```

After publication, the Codex marketplace command can use `Syft-AI/syft-plugin` instead of the local path.

## Connect

Restart your host session after installation. Open its MCP controls, select Syft, and choose Connect or Authenticate to complete OAuth with your Syft account. In Claude Code, run `/mcp` and authenticate `plugin:syft:syft`. Installation alone does not sign you in. All hosts use `https://api.syftai.com/mcp`; no API key belongs in this package.

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
