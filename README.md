# MyLaserTools MCP for Makers

Find existing vector artwork and open free design generators from your AI assistant. MyLaserTools connects artwork search, previews, eligible file downloads, and personalized maker projects through a hosted MCP server.

**Server URL:** `https://www.mylasertools.com/mcp`  
**Transport:** Streamable HTTP  
**Authentication:** OAuth with your MyLaserTools account

[Official MCP Registry entry](https://registry.modelcontextprotocol.io/v0.1/servers/com.mylasertools%2Fmakers/versions/latest): `com.mylasertools/makers`, version `1.0.0`.

[Connect your assistant](https://www.mylasertools.com/connect-ai-assistant) · [Setup guide](https://www.mylasertools.com/learn/business-integrations/connect-ai-assistant-mcp) · [Art Library](https://www.mylasertools.com/art-library) · [Support](https://www.mylasertools.com/contact)

## Connect

Add the server URL in an MCP client that supports remote Streamable HTTP and OAuth, then sign in to your MyLaserTools account and review the requested permissions.

### Codex

```sh
codex mcp add mylasertools --url https://www.mylasertools.com/mcp
```

Complete the browser sign-in flow. If you need to sign in later:

```sh
codex mcp login mylasertools
```

### Claude Code

```sh
claude mcp add --transport http mylasertools https://www.mylasertools.com/mcp
```

Use Claude Code's MCP connection controls to complete OAuth.

### Other MCP clients

Clients that accept an MCP settings file may use:

```json
{
  "mcpServers": {
    "mylasertools": {
      "url": "https://www.mylasertools.com/mcp"
    }
  }
}
```

Some clients require an explicit `streamable-http` transport setting. Follow your client's remote MCP and OAuth instructions. Public directory listings have their own approval process; this configuration connects directly to MyLaserTools.

## Artwork and design workflows

Start with a focused project request, such as:

- "Find three botanical designs for engraving a wooden box. Show previews, source information, rights, and available file formats."
- "Open a free plant stake generator with the name Rosemary and my chosen dimensions."
- "Prepare a personalized backpack tag for 3D printing and give me the generator link."
- "Check whether my account can download this artwork before spending any Sparks."

Artwork tools return the actual formats and access conditions for each result. Generator tools return links that open the website with supported settings filled in; finish the design and export it there. Export formats depend on the selected generator. Artwork eligible for a layered workflow is identified individually. Print contours are not currently validated by the MCP service.

## Available tools

| Tool | Purpose |
| --- | --- |
| `search_art` | Search the Art Library for a specific project |
| `preview_art` | Inspect one artwork, its formats, source, rights, and access |
| `quote_download` | Check download eligibility and any Spark cost |
| `unlock_art` | Unlock quoted artwork after the user agrees to the Spark cost |
| `download_art` | Obtain temporary links to artwork the account can already access |
| `open_in_editor` | Open selected artwork and optional text in the website editor |
| `get_usage` | Check the connected account's plan, allowances, and permissions |
| `find_maker_tools` | Find suitable website design generators |
| `get_maker_tool` | Inspect a generator's supported inputs and exports |
| `design_connected_text` | Open a personalized connected text project |
| `design_plant_stake` | Open a personalized plant stake project |
| `design_backpack_tag` | Open a personalized backpack tag project |
| `design_print_box` | Open a personalized 3D printable box project |

## Access and permissions

The same MyLaserTools account supplies your existing plan benefits, artwork unlocks, and account-wide download limits. Free generators remain free. Some artwork requires an eligible plan or a Spark unlock. Ask the assistant to quote costs first; Spark spending requires a separate opt-in permission and your agreement to the quoted cost. The MCP tools never purchase Sparks.

Permissions cover artwork reading, artwork downloads, editor handoffs, generator use, optional Spark spending, and remaining connected through OAuth refresh. Review them on the consent screen. You can revoke an assistant connection through MyLaserTools.

Searches, previews, generator links, and downloads are bounded by account allowances. Bulk catalogue extraction and library replication are unsupported. Download links are temporary and should be kept private.

## Privacy and support

MyLaserTools receives the tool calls your assistant sends to it, rather than the assistant's entire conversation. See the [privacy policy](https://www.mylasertools.com/privacy), [terms of service](https://www.mylasertools.com/terms), and [connection guide](https://www.mylasertools.com/connect-ai-assistant) for service details. Contact [support@mylasertools.com](mailto:support@mylasertools.com) for connection issues.

This repository contains integration metadata and documentation. The license below applies to these files. Artwork, fonts, and generated exports have their own rights and service terms; inspect each item's terms before using it.

## License

[MIT](LICENSE), copyright 2026 Julia Malkov.

## Package formats

The root `plugin.json` and `mcp.json` use the portable Agent Plugins format. Claude Code uses `.claude-plugin/plugin.json` and `.mcp.json`. OAuth is discovered from the hosted server.

For an OpenAI directory submission, package the root `plugin.json`, `assets/`, and `submissions/openai/mcp.json` renamed to root `mcp.json`. This variant adds OpenAI's documented OAuth registration settings. It requests artwork and maker permissions without Spark spending. The portable MCP 1.0.0 schema currently rejects server extensions, so the root portable configuration omits those OpenAI-specific fields.
