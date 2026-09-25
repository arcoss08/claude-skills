# 🚀 Compartir borrador (Vercel preview)

Purpose: give the user a **shareable draft link** for a site they can send to a
potential client — not a final publish, not a domain setup, not production
hosting. Vercel here is a **scratchpad for sharing**, nothing more.

**Out of scope reminder still applies** (`04-critical-gotchas.md` /
`SKILL.md`): this is not about connecting/publishing on a client's own hosting
(e.g. Hostinger). Vercel previews are the agency's own throwaway drafts, used
only to get client feedback before real delivery.

---

## When this capability runs

Only when explicitly asked, per the golden rule. Triggers:
- "compárteme un enlace para que lo vea el cliente"
- "súbelo a Vercel para enseñárselo"
- "pásame un borrador / un preview"

Never chain into this from a build automatically. Finishing a build does **not**
imply "now deploy it" — offer it as the one optional next-step sentence at most,
per the golden rule in `SKILL.md`.

## Precondition

The Vercel MCP connection must already exist (`claude mcp add --transport http
vercel https://mcp.vercel.com`, run once by the user in their terminal — this
skill cannot run that for them, it requires their own Vercel login via OAuth).
If the MCP tools aren't available when this capability is invoked, say so in
plain language ("necesito que conectes tu cuenta de Vercel una vez, dime y te
paso el paso") and stop — don't try to work around it with the Vercel CLI
unless the user explicitly has it installed and asks for that instead.

## What "draft" means here

- Every deploy is a **preview deployment**, never promoted to a production
  domain unless the user explicitly asks to make it the client's real site.
- The project name should make it obvious it's a draft, e.g.
  `<slug>-borrador` or `<slug>-preview`, not the client's real brand domain.
- No custom domain is attached. The `*.vercel.app` preview URL **is** the
  deliverable — that's what gets sent to the potential client.

## Flow

1. Confirm the local site folder is the finished/current state the user wants
   to share (don't deploy mid-edit unless asked).
2. Use the Vercel MCP tools to create/link a project and deploy the folder as
   a **static site** (no build step — same no-npm/no-build stance as the rest
   of this skill; the folder already contains `index.html`/`styles.css`/
   `main.js`/assets as-is).
3. Get the resulting preview URL back from the deploy result.
4. Hand the user just the link, in plain language: "aquí tienes el enlace
   para que se lo mandes: <url>". No jargon about builds/deployments/CLI.
5. If asked to update the draft after edits, redeploy the same project (new
   preview URL each time is fine — mention the link may have changed).

## Guardrails

- Never attach a paid/production custom domain during this capability.
- Never send API keys, `.env`, or the OpenAI image-generation key along in the
  deployed folder — same rule as `08-pre-deploy-checklist.md`: secrets and
  working files stay out of what gets shared.
- If the user asks to make the draft "the real site" (i.e. actually publish
  for the client), that's a bigger decision (custom domain, client's own
  hosting or a promoted Vercel production deploy) — ask explicitly rather than
  assuming, since it goes beyond "borrador para compartir".
