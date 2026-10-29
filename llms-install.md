# Installing the asms MCP server (for AI agents)

asms is a **remote** MCP server. There is nothing to clone, build or run locally.

- Endpoint: `https://asms.ai/mcp`
- Transport: Streamable HTTP
- Auth: OAuth sign-in with an asms account, or an API key sent as `Authorization: Bearer <key>`

## Steps

1. Ask the user for their asms API key. They create one at https://asms.ai/dashboard#api-keys (sign up at https://asms.ai/register if they have no account). Never create an account, a key or a top-up for the user, and never print the key back.
2. Add the server to the client's MCP settings.

   **Cline** (`cline_mcp_settings.json`, opened from the MCP Servers icon → Configure):

   ```json
   {
     "mcpServers": {
       "asms": {
         "url": "https://asms.ai/mcp",
         "type": "streamableHttp",
         "headers": { "Authorization": "Bearer <ASMS_API_KEY>" },
         "disabled": false,
         "autoApprove": []
       }
     }
   }
   ```

   Keep `type: "streamableHttp"`; without it Cline falls back to legacy SSE. Leave `autoApprove` empty: `create_otp_order`, `rent_number`, `cancel_order` and `cancel_rental` spend or refund wallet money and must be confirmed by the user.

   Other clients: see https://asms.ai/agents for the exact setup per client.
3. Verify: call `get_balance`. It returns the wallet balance in USD. A 401 means the key is missing or wrong.

## Using it

- One verification code: `get_pricing` → confirm the price with the user → `create_otp_order` → `poll_sms` every few seconds until the code arrives. If none arrives, order again rather than cancelling; unfilled orders refund automatically.
- A number to keep: `get_rental_offers` → confirm → `rent_number` → `read_rental_sms`.
