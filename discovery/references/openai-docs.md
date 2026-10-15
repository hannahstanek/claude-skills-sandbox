# OpenAI Docs route

Use this route for Codex, ChatGPT, OpenAI API, model, SDK, prompting, agent, eval, pricing, setup, customization, or troubleshooting questions.

1. If an OpenAI-docs skill or connector is available in this environment, load it and let it own source selection and citations.
2. Otherwise, use web search restricted to official OpenAI domains (platform.openai.com, developers.openai.com, help.openai.com, openai.com, github.com/openai) and fetch the specific pages you cite.
3. Check page dates or changelogs for anything version-, model- or price-sensitive; preserve exact model names as written in the docs.
4. Mark the result `degraded` when only secondary sources or stale pages support a claim.
5. For a cross-domain request, return the OpenAI evidence packet to the discovery router and reconcile it with the other lanes without weakening its source restrictions.
