# asms MCP server

Phone numbers for AI agents. Connect [asms.ai](https://asms.ai) to Claude, ChatGPT, Codex, Cursor, Grok or any MCP client, and your agent can:

- **get SMS verification codes**: a one-time number for a service, charged only when the code arrives and refunded automatically when none does;
- **rent phone numbers**: a number of your own for a day to a year that receives every SMS sent to it, for testing your app's SMS login or an account you'll verify again later;
- **check the account**: balance, prices, stock and open orders.

Everything is paid from your asms wallet, and the tools that spend are marked so your client asks you first.

```
https://asms.ai/mcp
```

Remote server, Streamable HTTP. Sign in with your asms account (OAuth), or send an API key from your [dashboard](https://asms.ai/dashboard) as `Authorization: Bearer <key>`.

## Setup

Full step-by-step pages, including a prompt your agent can follow on its own, are at **[asms.ai/agents](https://asms.ai/agents)**.

| Client | Quick setup |
|---|---|
| [Claude Code](https://asms.ai/agents/claude-code) | `claude mcp add --transport http asms https://asms.ai/mcp`, then `/mcp` to sign in |
| [Claude](https://asms.ai/agents/claude) (claude.ai, Desktop) | Customize → Connectors → Add custom connector → `https://asms.ai/mcp` |
| [Codex](https://asms.ai/agents/codex) | `codex mcp add asms --url https://asms.ai/mcp --bearer-token-env-var ASMS_API_KEY` |
| [ChatGPT](https://asms.ai/agents/chatgpt) | Plugins → Add custom MCP server → `https://asms.ai/mcp`, OAuth |
| [Cursor](https://asms.ai/agents/cursor) | [Add to Cursor](https://asms.ai/agents/cursor) or `~/.cursor/mcp.json` |
| [VS Code](https://asms.ai/agents/vscode) | [Install in VS Code](https://asms.ai/agents/vscode) or `.vscode/mcp.json` |
| [Windsurf](https://asms.ai/agents/windsurf) | `serverUrl` entry in Cascade's `mcp_config.json` |
| [Gemini CLI](https://asms.ai/agents/gemini-cli) | `gemini mcp add --transport http asms https://asms.ai/mcp` |
| [opencode](https://asms.ai/agents/opencode) | `remote` entry in `opencode.json` |
| [Grok](https://asms.ai/agents/grok) | grok.com Connectors → Custom, or the xAI API `mcp` tool |
| [OpenAI API](https://asms.ai/agents/openai-api) | Responses API `{"type": "mcp", "server_url": "https://asms.ai/mcp"}` |

Most clients that take a URL and headers accept:

```json
{
  "mcpServers": {
    "asms": {
      "url": "https://asms.ai/mcp",
      "headers": { "Authorization": "Bearer <ASMS_API_KEY>" }
    }
  }
}
```

## Tools

| Tool | What it does | Needs your OK |
|---|---|---|
| `get_balance` | Wallet balance | |
| `get_pricing` | Verification code prices by country and service | |
| `get_inventory` | Numbers in stock by country and service | |
| `create_otp_order` | Order a number for one verification code | yes |
| `poll_sms` | Check for the code on an order | |
| `list_active_orders` | Orders waiting for a code or already received | |
| `cancel_order` | Cancel an order (rarely needed: unfilled orders refund themselves) | yes |
| `get_rental_offers` | Rental countries, periods and prices | |
| `rent_number` | Rent a number for a period | yes |
| `list_rentals` | Your rented numbers and their end dates | |
| `read_rental_sms` | SMS received by a rented number | |
| `cancel_rental` | Cancel a rental for a refund (5 to 120 minutes after renting, before any SMS) | yes |

## Pricing

Connecting is free. Verification codes are priced per service and country and charged only when the code arrives; rentals are priced per country and period. See [asms.ai/pricing](https://asms.ai/pricing).

## Also

- [Agent skills](https://github.com/asms-ai/agent-skills) for Claude Code, Codex, Cursor and other agents
- [REST API](https://asms.ai/api-docs), same key and wallet
- [llms.txt](https://asms.ai/llms.txt)

## License

MIT
