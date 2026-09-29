---
name: refine-review
description: >-
  Use when uploading a manuscript or paper to Refine.ink, starting or watching a
  proofreading review, listing sessions, checking credits, or acting on Refine
  comments. Prefer Refine MCP tools over the REST API when the connector is
  connected.
---
# Refine review

Refine.ink proofreads academic documents. This plugin wires the hosted MCP at
`https://api.refine.ink/mcp` (same endpoint as the Claude directory listing
https://claude.ai/directory/refine-ink). Auth is OAuth by default.

## When to use

- User asks to refine, proofread, or review a paper/manuscript/PDF/DOCX
- Check Refine credits, history, or in-flight processing
- Address or dismiss feedback comments from a prior session

## Workflow

1. Confirm the Refine connector is connected (`GetMcpServerStatus` / tools
   available under the refine namespace). If not, add
   `https://api.refine.ink/mcp` and complete OAuth.
2. Prefer MCP tools exposed by the server. Typical loop from the public REST
   docs (MCP tool names may differ; discover with GetDynamicTools):
   - Upload the document
   - Wait for upload completion (SSE / watch tool)
   - Start process (`preview: true` for a cheap pass; full review costs 1 credit)
   - Watch processing until complete
   - Fetch session details and present comments
3. Do not invent comment IDs or session IDs. Read them from tool results.
4. Credits: check balance before a full (non-preview) review. Say when a run
   will spend a credit.
5. Organization context: if acting for an org, pass the organization the tools
   expect (REST uses `X-Refine-Organization` or `personal`).

## Reporting

Summarize for the user: document title, preview vs full, comment count, top
issues, and a link or session id they can open on refine.ink. Stay quiet on
healthy in-flight progress unless they asked for updates or something blocks.
