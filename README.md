# Nexplora for Claude

Use your Nexplora account from Claude. Ask in plain words and Claude works through your
Nexplora account: your connected business apps, your CRM and support records, your memory,
your skills and your own AI models. Anything that changes something in your apps waits for your
approval in Nexplora before it runs.

## What is in this plugin

- A connector to Nexplora's MCP server at `https://nexplora.ai/api/mcp/claude` (`.mcp.json`).
- One skill, `nexplora`, that tells Claude when and how to use the connector (`skills/nexplora/SKILL.md`).

There is no code, script or hook in this plugin: it is configuration and instructions only.

## Use it

1. Install the plugin, then open the plugin's **Connectors** tab and connect Nexplora.
2. Sign in to Nexplora and choose what Claude may do. You can untick any permission.
3. Ask, for example: "What do you remember about Acme?", "Find the three deals most likely to close this month." or "Add Ana Silva from Acme to my CRM." The common actions of your CRM, support desk, projects, email and the other apps Nexplora runs for you are their own tools; anything else is found and run one action at a time.
4. Use your own models: ask Claude to list your models, to ask one by name, or to put several on one request as a council. They run on the keys you have added in Nexplora, and they only think: they change nothing in your apps.

## Want more? The fuller connector

This plugin's connector is the listed one. Nexplora also has a fuller connector, `https://nexplora.ai/api/mcp`, that you add yourself (Claude: Settings, Connectors, Add custom connector; Claude Code: `claude mcp add --transport http nexplora-full https://nexplora.ai/api/mcp`; other apps: see https://nexplora.ai/mcp). It reaches the same account with more: plain-words requests Nexplora carries out across your apps, custom tools you build, your skills and workers. Changes still wait for your approval. Claude can tell you about it when you ask for something the listed connector cannot do. It is a separate connection: nothing about it changes what this plugin's connector does.

## Data

Claude sends your requests, and the details they need, to nexplora.ai. Nexplora then acts in the
apps you have connected to your Nexplora account, only within the permissions you granted. When you ask one of your models, or the council, your request is also sent to that model's provider on your own key. Memory is
saved only when you ask for it. Changes to your apps wait for your approval. This plugin stores nothing itself and sends data
to no other service.

- Privacy policy: https://nexplora.ai/privacy
- Terms: https://nexplora.ai/terms
- Security: https://nexplora.ai/security (report issues to security@nexplora.ai)
- Support: victor@nexplora.ai

## License

MIT, for the files in this repository. Nexplora the service is governed by the terms above.
