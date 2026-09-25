---
name: desarrollar_web
description: One skill bundling several INDEPENDENT capabilities for building studio-grade static websites — never force-chained; each runs on its own when asked. (a) BUILD studio-grade static websites (HTML/CSS/vanilla JS, no build, no npm) with real wow factor. (b) GENERATE bespoke on-brand images with OpenAI gpt-image-2, or fetch free stock. (c) design direction, surgical edits, and a pre-launch verify pass. (d) SHARE a draft preview link via Vercel MCP so a potential client can see it, never a real publish. Ask for a web without images and it only builds; ask to add images and it only does that; ask to share a draft and it only deploys a preview. Use it to create or edit any website (landing, portfolio, restaurant, agency, SaaS, shop, blog), generate images for one, or share a draft link. Triggers include haz una web, crea una landing, genera imagenes para la web, súbelo a Vercel para que lo vea el cliente, pásame un borrador, usando la skill desarrollar_web, and their English equivalents. Not for connecting or publishing to a client's own hosting provider (e.g. Hostinger) — that is out of scope for this skill; Vercel here is only for throwaway agency-side draft links.
---

# Web Studio — build · imagine, each on demand

This is **one home for a few independent capabilities**. Think of it as a
studio with different rooms, not an assembly line. You can:

- 🎨 **Build** a studio-grade static website (HTML/CSS/vanilla JS, no build/npm).
- 🖼️ **Imagine** — generate bespoke, on-brand imagery with OpenAI (gpt-image-2).
- 🚀 **Share a draft** — deploy a Vercel preview link to show a potential client.
- (plus 🎯 design direction, ✏️ surgical edits, ✅ verify.)

The person pulls **whichever they need, when they need it**. Your job is to read
which capability the current message is asking for and serve **exactly that**.

**Out of scope:** connecting to or publishing/deploying on a client's own
hosting provider (Hostinger or otherwise) — that's the client's territory, not
this skill's. This skill covers building the site itself — files, code, and
images — plus, only when asked, sharing a **throwaway Vercel preview link**
with a potential client (`12-vercel-preview-deploy.md`). If asked to connect
an account or put a site online on the client's real hosting, say that's
outside what this skill handles.

---

## THE GOLDEN RULE: do only what was asked, then stop

**Do not chain capabilities.** Do not turn one request into a full pipeline.
Read the message, do that one thing, verify it, and stop — even if "obvious
next steps" exist.

Concretely, this is the experience the skill must deliver:

- User: *"hazme una web para X, sin imágenes de momento"* → you **only** build
  the site with placeholders. You do **not** fetch/generate images.
- Later, User: *"vale, rellénala con imágenes"* → you **only** produce images
  and drop them in. Nothing else.

Never assume the next room. **Read the state from context** each time — does a
project folder already exist? does it already have images? — and serve just the
current ask. At the very end you may offer **one** optional sentence naming a
natural next step ("¿quieres que le genere imágenes a medida, o la dejo así?"),
but you **never start it unprompted**.

If a request is genuinely ambiguous, ask **one** short question to pick the
capability — not a multi-question intake.

---

## Route the request → capability

| What they say / the situation | Capability | Primary ref |
|---|---|---|
| "haz una web / crea una landing / necesito una web para mi [negocio]", no project exists | 🎨 **Build** | `02`, `06`, `01`, `03` + `intake-template.md` |
| A project exists and "cambia…/ añade…/ otro color / otra sección" | ✏️ **Surgical edit** | the existing files + invariants |
| "genera/haz imágenes", "mis fotos del proveedor son feas", "necesito una foto de portada a medida" | 🖼️ **Image genie** | `reference/11-ai-image-generation.md` |
| "qué diseño le pondrías", "dame ideas" | 🎯 **Design direction** | `02`, `03`, `06` |
| "¿está lista?", "la subí y se ve rota/vieja" | ✅ **Verify / cache** | `08`, `07`, `10` |
| "súbelo a Vercel", "pásame un link/borrador para el cliente" | 🚀 **Share draft** | `12-vercel-preview-deploy.md` |

Capabilities **can** compose when the user asks for a lot at once ("hazme esta
web con imágenes a medida" → 🎨 → 🖼️). That's fine — but you compose because
*they asked for the whole thing*, never by reflex.

---

## The capabilities

Each is self-contained. Read its ref before acting; skip the rest.

### 🎨 Build a website
Infer the brief; ask at most the few things you can't infer, once
(`intake-template.md`). Pick **one** archetype (`reference/02-archetypes.md`),
honor the diversity rules (`06`), generate `index.html` / `styles.css` /
`main.js` / `lib/manifest.js` per `reference/01-stack-and-conventions.md` and the
invariants below, copy `templates/htaccess.template` → `.htaccess`, verify, and
preview. **If they said "without images", use placeholders and don't touch the
image genie.**

### 🖼️ Image genie (AI or stock or their photos)
Three sources — user photos, Openverse stock (free, CC), or **AI-generated**
(OpenAI gpt-image-2, bespoke, ~few $). Pick by context;
`reference/05-image-and-asset-pipeline.md` for the pipeline and
`reference/11-ai-image-generation.md` for the full AI method (photographic
script, anchor images, **banner contract**, chained series, masks). All sources
end as WebP in `assets/img/`. AI is opt-in and costs money — **offer, explain the
cost, get a yes**. Can run standalone ("genérame una foto de portada") or inside
a build.

### 🚀 Share a draft (Vercel preview)
Only when explicitly asked ("súbelo a Vercel", "pásame un link para el
cliente") — never automatically after a build. Uses the Vercel MCP connection
(the user sets this up once with `claude mcp add --transport http vercel
https://mcp.vercel.com`, outside this skill — you can't run that for them).
Deploys the current site folder as a **preview** (not production, no custom
domain), hands back just the `*.vercel.app` link. Full flow, guardrails
(no secrets in the deploy, draft naming) and what to say if Vercel isn't
connected yet: `reference/12-vercel-preview-deploy.md`.

### 🎯 Design direction / ✏️ Surgical edit / ✅ Verify
As on-demand as the rest: an art-direction opinion (`02`/`03`/`06`), the smallest
change to an existing site in its own style, or a pre-launch pass
(`08` + the 3-machine test in `07`). Never the whole funnel unless asked.

---

## Always-on invariants (they hold in every capability)

**Communication (both capabilities — build, imagine):**
- **Idioma: responde SIEMPRE al usuario en castellano** mientras esta skill esté
  activa (aunque estas notas internas estén en inglés y aunque él escriba en otro
  idioma), salvo que él pida explícitamente otro idioma.
- **Registro: cero tecnicismos.** El usuario es **no técnico** y no debe sentirse
  abrumado. Nunca digas "npm", "API", "asset", "repositorio", ni le muestres
  comandos, rutas, nombres de herramientas o errores en crudo. Traduce todo: "los
  archivos del diseño", "preparar las imágenes". Si algo falla por dentro, para
  él es "estoy afinando un detalle, un momento" — nunca un volcado de error.
- Anuncia antes de cada paso visible, celebra los hitos (✅) y **verifica antes de
  afirmar** que algo funciona.
- Estas notas de referencia son técnicas **a propósito, porque las lees tú (el
  LLM)** — son tu guía interna, no un guion para leerle al usuario.

**Web quality (build / images), full detail in `reference/04-critical-gotchas.md`:**
1. No `<script type="module">` with relative imports — classic `<script defer>` +
   IIFE + `window.__BRAND__`.
2. `.htaccess` in every root + `?v=YYYYMMDD` on every asset ref (bump per deploy).
3. Native scroll by default (Lenis opt-in only).
4. Reduced-motion gates only *intrusive* effects — never tilt/hover/fade/mesh
   (Windows ships it ON; you'd hand them a dead site).
5. All images WebP, never mixed formats.
6. Hardcode content in HTML; JS only enriches (must read with JS off).
7. `safe()` around every `init*`; IntersectionObserver threshold ≤ 0.05 + safety
   timeout; splash double safety net.
8. Content first, animation second. 9. Robustness > spectacle. 10. One archetype,
   never two. 11. Verify before claiming.

If an invariant and a flourish conflict, the invariant wins.

---

## Environment (handle once, silently, when a capability needs it)

- 🖼️ **Image genie (AI)** needs **Node 18+** and an OpenAI key the user provides.
- 🎨 **Build** helper scripts run on Python *or* Bash; everything degrades
  gracefully (`reference/09-environment-detection.md`).
- 🚀 **Share a draft** needs the Vercel MCP connection already set up by the
  user (one-time, outside this skill). If it's missing, say so in plain
  language and stop — don't substitute the Vercel CLI unless they ask for it.

Install what's missing yourself where you can; only ask the user to install
something if every automatic path failed.

---

## Files index

```
SKILL.md                                ← this file — the multi-capability router
intake-template.md                      ← the few questions worth asking (build)
recommended-settings.json               ← optional zero-prompt pre-authorization
evals/evals.json                        ← capability-routing evals
reference/
  01-stack-and-conventions.md           ← file structure, IIFE, script order
  02-archetypes.md                      ← 10 archetypes (pick ONE)
  03-effects-catalog.md                 ← 40+ copy-paste effects
  04-critical-gotchas.md                ← the web invariants, in full
  05-image-and-asset-pipeline.md        ← photos: user / Openverse / AI / WebP
  06-diversity-guardrails.md            ← never clone; rotate archetypes
  07-windows-troubleshooting.md         ← reduced-motion + the 3-machine test
  08-pre-deploy-checklist.md            ← the verify pass
  09-environment-detection.md           ← Node/Python/curl detection
  10-deployment-and-cache.md            ← cache-busting + .htaccess strategy
  11-ai-image-generation.md             ← 🖼️ OpenAI gpt-image-2 image genie
  12-vercel-preview-deploy.md           ← 🚀 Vercel MCP: draft link to share with a client
templates/
  htaccess.template                     ← copy as `.htaccess` to every root
scripts/
  download_libs.py / .sh                ← GSAP/ScrollTrigger to lib/
  openverse_fetch.py / .sh              ← free stock images (CC-licensed)
  webp_convert.py                       ← any image → optimized WebP
  verify_project.py                     ← post-generation sanity check
  generar-foto.mjs                      ← 🖼️ OpenAI gpt-image-2 generator
  recortar-banner.ps1 / .sh             ← 🖼️ crop to exact banner ratio
```

---

## Zero-prompt mode

If the user wants the skill to run without approving each command, have them
merge `recommended-settings.json` into their `~/.claude/settings.json` once. It
pre-authorizes only this skill's own scripts and a few safe helpers. Nothing
destructive.

---

## Final note

One studio, a few doors. Read which door the person walked through, do
that well, verify it, and stop. When they say *"hazme la web"* you hand them a
site; when they say *"ponle imágenes"* you hand them imagery; when they say
*"pásame un link para el cliente"* you hand them a Vercel preview URL —
each on its own, each finished, never forced together. Connecting or
publishing to a client's own hosting provider is not something this skill
does; Vercel here is only ever a throwaway draft to get feedback.
