---
name: nexplora
description: Work in the user's Nexplora account. Use when the user mentions Nexplora, their connected apps, their CRM or support records, what Nexplora remembers, their skills, their AI models, or asks to do something across their business apps.
---

Nexplora is connected to this conversation as a connector. Sign-in and the list of things Claude may do are chosen by the user on Nexplora's own consent screen, so a tool can be refused for a scope the user did not grant. Say so plainly and do not retry around it.

How to work:

1. The common actions in the apps Nexplora runs for the user's company have their own tools, named for the app and the action: for example `crm_people_create`, `crm_notes_create`, `crm_opportunities_list`, `support_conversations_list`, `support_conversations_reply`, `projects_work_items_create`, `email_emails_create` (a draft; nothing is sent) and `analytics_overview_get`. Call one directly with the fields its schema names.
2. For anything else, in those apps or the user's connected apps, call `search_actions` to find the action and its parameters, then `run_action`. Actions run one at a time. This connection does not offer actions that move money or generate AI images, video or audio; if one is refused, tell the user.
3. To recall or save something, use `memory_search` and `memory_save`. Save only what the user asked to be remembered.
4. To look at earlier work, use `sessions_list` and `session_read`.
5. To see the user's skills, use `skills_list`.
6. To use the user's own AI models, call `models_list` to see them by provider, then `model_ask` to ask one model by name, or `council_ask` to put several on one request together (a lead assigns roles, one builds, one reviews). They run on the user's own keys where the user has added them. They only return text: they change nothing in the user's apps. Only name models that `models_list` shows as ready; if one is not, tell the user to add their key in Nexplora.
7. `apps_list` shows the apps the user can work in: the apps Nexplora runs for their company (CRM, support, analytics, projects, ERP, email, experiments, social) and their connected apps. Each app's own tools are listed with it; every action, those included, can be found with `search_actions`.
8. If you are unsure which account is connected, call `whoami`.

Approvals:

- Reading runs straight away.
- Any change to the user's apps waits for the user's approval in Nexplora. When a result says something is waiting, tell the user what is waiting and where to approve it. Do not claim it was done.
- After the user approves, call `approval_status` with the `approval_id` you were given. That call runs the approved action and returns its result.

More of Nexplora (a second, fuller connector):

This connection is the listed one: reads, memory, one action at a time, and the user's own models. Nexplora also has a fuller connector at https://nexplora.ai/api/mcp that the user adds themselves. It reaches the same account with more: a plain-words request that Nexplora carries out across their apps, building a custom tool they then own, running their skills, continuing a Nexplora conversation, and workers. Changes still wait for the user's approval in Nexplora.

Mention it when the user asks for something this connection cannot do (a custom tool, a skill run, a plain-words task across their apps, a worker, continuing a Nexplora conversation). Say that it is a separate connection they add, and how:

- Claude (claude.ai): Settings, then Connectors, then Add custom connector. Name it Nexplora Full and paste https://nexplora.ai/api/mcp. Choose Connect, sign in to Nexplora, and choose Allow.
- Claude Code: `claude mcp add --transport http nexplora-full https://nexplora.ai/api/mcp`, then sign in when asked.
- Codex and other apps that speak MCP: add a remote MCP server with that address and sign in to Nexplora. Setup steps for each app: https://nexplora.ai/mcp

Do not add it for the user, and do not suggest it unless the request needs it. The fuller connector is separate: nothing above changes that no tool of this connection moves money or generates images, video or audio.

Report what Nexplora actually returned. If a call fails or is refused, say what happened.
