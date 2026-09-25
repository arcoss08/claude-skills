---
name: optimizar_memoria
description: Loop skill, triggered manually by the user (e.g. every ~30 min via /loop), that reviews the FULL current conversation and does two things in parallel — extracts actionable/relevant items into tareas.md, and optimizes memoria.md (the project's persistent memory) so it stays concise, current and free of duplicates. Logs one summary sentence per run to yo-robot.md. Never runs automatically as a side effect of other work — only when explicitly asked ("usando la skill optimizar_memoria", "optimiza la memoria", "corre el loop de memoria/tareas").
---

# Optimizador de memoria — una pasada de loop

Esta skill es independiente de `desarrollar_web`. Su único trabajo es, cuando
se le pide, mirar hacia atrás en la conversación actual y dejar el estado del
proyecto (memoria + tareas) al día. No construye webs, no toca imágenes, no
despliega nada.

El usuario la dispara manualmente en loop (p. ej. cada 30 minutos con
`/loop`). Cada disparo es **una pasada completa**, independiente de las
anteriores salvo por lo que ya quedó escrito en los archivos.

---

## Archivos que gestiona

Todos viven en la raíz del proyecto donde se invoque la skill:

- **`memoria.md`** — memoria persistente del proyecto (identidad, datos
  importantes, preferencias, stack, proyectos activos). Ya existe.
- **`tareas.md`** — tareas y datos relevantes extraídos de la conversación
  actual. Créalo si no existe.
- **`yo-robot.md`** — log de ejecuciones: una línea por pasada, en una sola
  frase, resumiendo qué se optimizó. Créalo si no existe.

## Qué hacer en cada pasada (en paralelo, no en serie)

Ambos pasos leen la misma conversación pero escriben en archivos distintos —
trátalos como dos lecturas independientes del mismo contexto, no como una
depende de la otra.

### 1. Extraer a `tareas.md`
- Repasa toda la conversación de la sesión actual (no solo el último mensaje).
- Saca lo accionable: tareas pendientes, decisiones tomadas, preguntas
  abiertas, próximos pasos.
- Formato: checklist agrupado por tema/proyecto (`- [ ] ...` / `- [x] ...`
  para lo ya resuelto).
- No dupliques: si un ítem ya está, actualízalo o márcalo hecho en vez de
  volver a añadirlo.
- No es un transcript — solo lo destilado y accionable.

### 2. Optimizar `memoria.md`
- Lee el archivo tal cual está.
- Fusiona o elimina entradas duplicadas u obsoletas que la conversación
  actual haya dejado claro que ya no aplican.
- Añade solo hechos nuevos y **duraderos** (preferencias del usuario, stack,
  proyectos activos, convenciones) — lo que de verdad vale la pena recordar
  en la próxima sesión, no detalles de una tarea puntual (eso va en
  `tareas.md`).
- Mantenlo corto y escaneable — este archivo no debe convertirse en un log.
- Si tienes dudas sobre si algo sigue vigente, consérvalo: ante la duda, no
  se borra.

## Después de cada pasada

Añade **una sola línea** a `yo-robot.md`, al final del archivo:

```
- [YYYY-MM-DD HH:MM] <una frase resumiendo qué se optimizó en esta pasada>
```

Una frase, no un párrafo. Ejemplo:
`- [2026-07-30 21:15] Añadí la conexión Vercel MCP a memoria.md y marqué como hechas las tareas de la skill desarrollar_web.`

## Cuándo se ejecuta

Solo cuando el usuario lo pide explícitamente (él la corre en loop manual,
p. ej. cada 30 min con `/loop`). Nunca se dispara sola como efecto colateral
de otro trabajo, ni se encadena con `desarrollar_web` u otras skills.
