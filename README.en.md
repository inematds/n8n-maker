# n8n-maker — n8n Skills for Claude Code

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

A set of **7 skills** that teach Claude Code to build, configure, validate, and
debug **n8n** workflows. They live in `.claude/skills/` and load automatically when
the topic comes up in conversation—you don't need to invoke anything manually.

## 📖 User guide

Complete guide (landing page + step-by-step instructions): **https://inematds.github.io/n8n-maker/guia/en/**

> They used to be global skills (`~/.claude/skills/`). They were moved into this
> project so they're versioned alongside the n8n work.

---

## The skills

| Skill | What it does | When it activates |
|---|---|---|
| **n8n-workflow-patterns** | The 5 proven architectural patterns: webhook, HTTP/API integration, database, AI agent, and scheduled tasks | Designing/structuring a new workflow |
| **n8n-node-configuration** | *Operation-aware* configuration: required fields, dependencies between properties, detail levels for `get_node` | Configuring a specific node |
| **n8n-expression-syntax** | `{{ }}` syntax, `$json` / `$node` variables, webhook data, and common errors | Writing or fixing expressions |
| **n8n-code-javascript** | Code node in JS: `$input` / `$json` / `$node`, `$helpers.httpRequest`, `DateTime`, node modes | Writing JS inside n8n |
| **n8n-code-python** | Code node in Python (beta): `_input` / `_json`, standard library, and limitations | Writing Python inside n8n |
| **n8n-validation-expert** | Reading and resolving validation errors, validation profiles, false positives | A `validate_*` call reported an issue |
| **n8n-mcp-tools-expert** | Efficient use of the `n8n-mcp` MCP tools: node search, validation, workflow management, library of ~2,700 templates | Operating n8n via MCP |

Each folder includes the `SKILL.md` (what Claude reads first) plus reference files
loaded on demand—`ERROR_CATALOG.md`, `COMMON_PATTERNS.md`, `DATA_ACCESS.md`,
`FALSE_POSITIVES.md`, etc. This keeps the context lightweight: only the necessary
details are included.

---

## Structure

The actual skill content lives in `skills/` (versioned and easy to find);
`.claude/skills/` contains only symlinks to them, which is where Claude Code
loads them from. One source, no duplicate copies.

```
n8n-maker/
├── README.md
├── .claude/skills/              → symlinks to ../../skills/*
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

## How to use

1. Open Claude Code **inside this folder** (`cd ~/projetos/n8n-maker`). Skills in
   `.claude/skills/` apply only to this project.
   (they load through the symlinks in `.claude/skills/`).
2. Ask for what you want in Portuguese: *"build a workflow that receives a webhook,
   validates the payload, and writes it to Postgres"*.
3. Claude loads the right skill automatically—`n8n-workflow-patterns` for the design,
   `n8n-node-configuration` when configuring, and `n8n-validation-expert` when
   validation reports an issue.

To use them in any project, copy (or symlink) the folders back to
`~/.claude/skills/`.

### Typical workflow

```
design (workflow-patterns)
   → configure nodes (node-configuration)
   → expressions and Code nodes (expression-syntax, code-javascript)
   → validate and fix (validation-expert)   ← 2-3 rounds is normal
   → publish/manage via MCP (mcp-tools-expert)
```

### Combining with the n8n MCP

The `n8n-mcp-tools-expert` skill assumes the **n8n-mcp** MCP server is connected—it
provides node search, configuration validation, a template library, and workflow
deployment. Without the MCP, the other six are still useful: they serve as guides to
syntax, patterns, and debugging.

---

## License / origin

INEMA internal-use skills, maintained in this repository.
