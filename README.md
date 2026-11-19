# Gymvio MCP server for ChatGPT and Claude

Gymvio publishes no public API or official MCP server, according to the Cotlet.dev page checked 17 November 2026. Cotlet.dev connects ChatGPT, Claude and other AI agents to your own signed-in Gymvio coach account through 23 hosted tools. The 5 read tools run directly; the 18 write tools ask for confirmation by default.

## What you can ask

> Review weekly check-ins and draft replies.

> Spot failed sets in logged workouts.

> Assign a training block to many clients after my approval.

> Build a diet plan with macros calculated.

> Draft a nudge for clients who are off plan.

## Connect in 2 minutes

Sign up at https://cotlet.dev/signup?app=gymvio, enable Gymvio and sign in at https://gymvio.com/login in your Cloud Browser. Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run the local MCP bridge

Python 3.10+, with no dependencies. Clone this repository, set your Cotlet.dev API key, then run:

```bash
export COTLET_API_KEY="your-key"
python3 gymvio_agent.py serve
```

This local stdio bridge lists seven browser helper tools: `gymvio_guide`, `gymvio_status`, `gymvio_open`, `gymvio_read`, `gymvio_click`, `gymvio_type` and `gymvio_close`.
It forwards calls to the hosted Cotlet.dev MCP server.
The 23 task tools described on the integration page are available through the hosted connection.

Without a key, the local bridge can list its helpers; calls return setup instructions.

```bash
python3 gymvio_agent.py connect
python3 gymvio_agent.py guide
python3 gymvio_agent.py status
```

## Questions from Gymvio users

**Does Gymvio have an API or official MCP server?**

The Cotlet.dev page checked 17 November 2026 found no public Gymvio API documentation, official MCP server or official ChatGPT or Claude connector.

**How do I connect Gymvio to ChatGPT or Claude?**

Sign up at https://cotlet.dev/signup?app=gymvio, enable Gymvio and sign in at https://gymvio.com/login in your Cloud Browser. Add https://cotlet.dev/mcp/v1/connect as the connector URL and sign in to Cotlet.dev.

**Do my clients need anything for this?**

No. Clients keep using Gymvio on their phones; Cotlet.dev works in your coach account.

**Is this an official Gymvio integration?**

No. Cotlet.dev is independent and is not affiliated with Gymvio.

## Integration details

[Gymvio tools and setup on Cotlet.dev](https://cotlet.dev/integrations/gymvio-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=gymvio)

---

More: https://cotlet.dev/integrations/gymvio-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=gymvio

Start free: https://cotlet.dev/signup?app=gymvio&utm_source=github&utm_medium=readme&utm_campaign=gymvio
