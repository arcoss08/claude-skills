# Skills para Claude Code

Colección de 54 skills para [Claude Code](https://claude.com/claude-code): marketing,
SEO, analítica, copywriting, diseño web y utilidades varias.

Son portátiles: ninguna depende de un proyecto concreto ni guarda credenciales.

## Instalación

Las skills viven en `~/.claude/skills/`. Para instalarlas todas:

```bash
git clone https://github.com/<usuario>/claude-skills.git
mkdir -p ~/.claude/skills
cp -R claude-skills/skills/* ~/.claude/skills/
```

Reinicia Claude Code y aparecerán disponibles.

### Instalar solo algunas

Copia únicamente las carpetas que te interesen:

```bash
cp -R claude-skills/skills/copywriting ~/.claude/skills/
cp -R claude-skills/skills/seo-audit   ~/.claude/skills/
```

### Antes de sobrescribir

Si ya tienes skills con el mismo nombre, `cp -R` las reemplaza sin avisar.
Haz una copia primero:

```bash
cp -R ~/.claude/skills ~/.claude/skills-backup-$(date +%Y%m%d)
```

## Uso

Cada skill se invoca por su nombre con barra inclinada:

```
/copywriting
/seo-audit
/graphify
```

O simplemente describe la tarea y Claude Code elige la skill que corresponda.

## Qué hay dentro

**Marketing y crecimiento** — `ads`, `ad-creative`, `ab-testing`, `attribution`,
`churn-prevention`, `co-marketing`, `cold-email`, `community-marketing`,
`competitor-profiling`, `competitors`, `content-strategy`, `customer-research`,
`directory-submissions`, `emails`, `events`, `influencer-marketing`, `launch`,
`lead-magnets`, `marketing-council`, `marketing-ideas`, `marketing-loops`,
`marketing-plan`, `marketing-psychology`, `offers`, `onboarding`, `paywalls`,
`popups`, `pricing`, `product-marketing`, `prospecting`, `public-relations`,
`referrals`, `revops`, `sales-enablement`, `signup`, `sms`, `social`

**SEO y analítica** — `ai-seo`, `analytics`, `aso`, `free-tools`,
`programmatic-seo`, `schema`, `seo-audit`, `site-architecture`

**Contenido** — `copywriting`, `copy-editing`, `image`, `video`

**Web y producto** — `desarrollar_web`, `Webs_futuro`, `cro`

**Utilidades** — `graphify` (convierte cualquier carpeta en un grafo de conocimiento
navegable), `optimizar_memoria`

## Notas

- **No incluye las skills oficiales de Anthropic** (`pdf`, `docx`, `xlsx`, `pptx`,
  `skill-creator`). Esas se sincronizan solas desde tu cuenta de Claude y tienen su
  propia licencia.
- `graphify` genera su salida en un `graphify-out/` dentro de la carpeta que analices.
  Conviene añadirlo al `.gitignore` de tus proyectos.
- Algunas skills traen scripts en Python en `scripts/`. Revísalos antes de correrlos,
  como con cualquier código de terceros.
