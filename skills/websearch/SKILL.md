---
name: web-research
description: >-
  Performs web research by first searching for relevant URLs with Tavily
  and then extracting the full page content with the fetch tool.
  Use when the user asks to search the web, research a topic, or find
  up-to-date information that is not in the repository.
triggers:
  - search
  - research
  - "find information"
  - "look up"
  - "web search"
  - "latest"
---

# Web Research Workflow

When you need to find information from the internet, follow this two-step
pipeline to keep the context small and the results accurate.

## Step 1: Search with Tavily

Always start by using the Tavily search tool (the `search` tool provided by
the Tavily MCP server). Do **not** start by guessing URLs or using `fetch`
on a search-engine result page.

- Send a concise, specific query.
- Tavily returns structured results with titles, URLs, and short snippets.
- Review the snippets to choose the most relevant sources.

## Step 2: Extract content with `fetch`

For the **one or two most relevant** URLs from the search results, use the
`fetch` tool to retrieve the full page content.

- `fetch` returns clean Markdown, which is much smaller than raw HTML.
- Do **not** fetch every result. Only fetch what you actually need to
  answer the user's question.

## Step 3: Answer from the extracted content

Base your answer **only** on the content you retrieved in Step 2.
If the fetched content does not answer the question, go back to the search
results and pick another URL, or refine your Tavily query.

## Important rules

- Never use `fetch` with a search-engine URL (e.g., `duckduckgo.com/?q=...`).
  That is not a real search; it only reads the search page itself.
- Prefer the official Tavily `search` tool for discovery.
- Keep the workflow efficient: search → select 1–2 links → fetch → answer.
