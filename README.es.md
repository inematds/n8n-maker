# n8n-maker — Skills de n8n para Claude Code

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

Conjunto de **7 skills** que ensinam o Claude Code a construir, configurar, validar y
depurar workflows de **n8n**. Se encuentran en `.claude/skills/` y se cargan solas cuando el
tema aparece en la conversación — no hace falta invocar nada manualmente.

## 📖 Guía de uso

Guía completa (landing + paso a paso): **https://inematds.github.io/n8n-maker/guia/es/**

> Antes eran skills globales (`~/.claude/skills/`). Se movieron a este
> proyecto para que queden versionadas junto con el trabajo de n8n.

---

## Las skills

| Skill | Para qué sirve | Cuándo se activa |
|---|---|---|
| **n8n-workflow-patterns** | Los 5 patrones arquitectónicos comprobados: webhook, integración HTTP/API, base de datos, AI agent y tareas programadas | Diseñar/estructurar un workflow nuevo |
| **n8n-node-configuration** | Configuración *operation-aware*: campos obligatorios, dependencias entre propiedades, niveles de detalle de `get_node` | Configurar un node específico |
| **n8n-expression-syntax** | Sintaxis `{{ }}`, variables `$json` / `$node`, datos de webhook y los errores clásicos | Escribir o corregir expresiones |
| **n8n-code-javascript** | Code node en JS: `$input` / `$json` / `$node`, `$helpers.httpRequest`, `DateTime`, modos del node | Escribir JS dentro de n8n |
| **n8n-code-python** | Code node en Python (beta): `_input` / `_json`, biblioteca estándar y limitaciones | Escribir Python dentro de n8n |
| **n8n-validation-expert** | Leer y resolver errores de validación, perfiles de validación, falsos positivos | Un `validate_*` reportó un error |
| **n8n-mcp-tools-expert** | Uso eficiente de las herramientas del MCP `n8n-mcp`: búsqueda de nodes, validación, gestión de workflows, biblioteca de ~2.700 templates | Operar n8n mediante MCP |

Cada carpeta incluye el `SKILL.md` (lo primero que lee Claude) y archivos de
referencia que se cargan según se necesitan — `ERROR_CATALOG.md`, `COMMON_PATTERNS.md`,
`DATA_ACCESS.md`, `FALSE_POSITIVES.md`, etc. Esto mantiene ligero el contexto: solo se
incluye el detalle necesario.

---

## Estructura

El contenido real de las skills está en `skills/` (versionado, fácil de encontrar);
`.claude/skills/` guarda solo symlinks hacia allí, que es desde donde Claude Code
las carga. Una sola fuente, sin copias duplicadas.

```
n8n-maker/
├── README.md
├── .claude/skills/              → symlinks para ../../skills/*
└── skills/
        ├── n8n-code-javascript/     SKILL.md + BUILTIN_FUNCTIONS, COMMON_PATTERNS,
        │                            DATA_ACCESS, ERROR_PATTERNS
        ├── n8n-code-python/         SKILL.md + STANDARD_LIBRARY, COMMON_PATTERNS,
        │                            DATA_ACCESS, ERROR_PATTERNS
        ├── n8n-expression-syntax/   SKILL.md + COMMON_MISTAKES, EXAMPLES
        ├── n8n-mcp-tools-expert/    SKILL.md + SEARCH_GUIDE, VALIDATION_GUIDE,
        │                            WORKFLOW_GUIDE
        ├── n8n-node-configuration/  SKILL.md + DEPENDENCIES, OPERATION_PATTERNS
        ├── n8n-validation-expert/   SKILL.md + ERROR_CATALOG, FALSE_POSITIVES
        └── n8n-workflow-patterns/   SKILL.md + webhook_processing,
                                     http_api_integration, database_operations,
                                     ai_agent_workflow, scheduled_tasks
```

---

## Cómo usar

1. Abre Claude Code **dentro de esta carpeta** (`cd ~/projetos/n8n-maker`). Las skills de
   `.claude/skills/` solo se aplican a este proyecto.
   (la carga proviene de los symlinks en `.claude/skills/`).
2. Pide lo que necesitas en portugués: *"crea un workflow que recibe un webhook,
   valida el payload y lo guarda en Postgres"*.
3. Claude activa la skill adecuada automáticamente — `n8n-workflow-patterns` para el diseño,
   `n8n-node-configuration` al configurar, `n8n-validation-expert` cuando la
   validación reporte un error.

Para usarlas en cualquier proyecto, copia (o crea symlinks de) las carpetas de nuevo en
`~/.claude/skills/`.

### Flujo típico

```
diseñar (workflow-patterns)
   → configurar nodes (node-configuration)
   → expresiones y Code nodes (expression-syntax, code-javascript)
   → validar y corregir (validation-expert)   ← 2-3 vueltas es lo normal
   → publicar/gestionar mediante MCP (mcp-tools-expert)
```

### Combinación con el MCP n8n

La skill `n8n-mcp-tools-expert` presupone que el servidor MCP **n8n-mcp** está conectado — es
lo que proporciona búsqueda de nodes, validación de configuración, biblioteca de templates y
deploy de workflows. Sin el MCP, las otras seis siguen siendo útiles: funcionan como guía de
sintaxis, patrones y depuración.

---

## Licencia / origen

Skills de uso interno de INEMA, mantenidas en este repositorio.
