# n8n-maker — Skills de n8n para Claude Code

Conjunto de **7 skills** que ensinam o Claude Code a construir, configurar, validar e
depurar workflows do **n8n**. Ficam em `.claude/skills/` e carregam sozinhas quando o
assunto aparece na conversa — não precisa invocar nada à mão.

## 📖 Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/n8n-maker/guia/**

> Antes eram skills globais (`~/.claude/skills/`). Foram movidas para dentro deste
> projeto para ficarem versionadas junto com o trabalho de n8n.

---

## As skills

| Skill | Para que serve | Quando dispara |
|---|---|---|
| **n8n-workflow-patterns** | Os 5 padrões arquiteturais comprovados: webhook, integração HTTP/API, banco de dados, AI agent e tarefas agendadas | Desenhar/estruturar um workflow novo |
| **n8n-node-configuration** | Configuração *operation-aware*: campos obrigatórios, dependências entre propriedades, níveis de detalhe do `get_node` | Configurar um node específico |
| **n8n-expression-syntax** | Sintaxe `{{ }}`, variáveis `$json` / `$node`, dados de webhook e os erros clássicos | Escrever ou corrigir expressões |
| **n8n-code-javascript** | Code node em JS: `$input` / `$json` / `$node`, `$helpers.httpRequest`, `DateTime`, modos do node | Escrever JS dentro do n8n |
| **n8n-code-python** | Code node em Python (beta): `_input` / `_json`, biblioteca padrão e limitações | Escrever Python dentro do n8n |
| **n8n-validation-expert** | Ler e resolver erros de validação, perfis de validação, falsos positivos | Um `validate_*` reclamou |
| **n8n-mcp-tools-expert** | Uso eficiente das ferramentas do MCP `n8n-mcp`: busca de nodes, validação, gestão de workflows, biblioteca de ~2.700 templates | Operar o n8n via MCP |

Cada pasta traz o `SKILL.md` (o que o Claude lê primeiro) mais arquivos de
referência carregados sob demanda — `ERROR_CATALOG.md`, `COMMON_PATTERNS.md`,
`DATA_ACCESS.md`, `FALSE_POSITIVES.md` etc. Isso mantém o contexto leve: só o
detalhe necessário entra.

---

## Estrutura

O conteúdo real das skills mora em `skills/` (versionado, fácil de achar);
`.claude/skills/` guarda apenas symlinks para lá, que é de onde o Claude Code
carrega. Uma fonte só, sem cópia duplicada.

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

## Como usar

1. Abra o Claude Code **dentro desta pasta** (`cd ~/projetos/n8n-maker`). Skills em
   `.claude/skills/` valem só para este projeto.
   (o carregamento vem dos symlinks em `.claude/skills/`).
2. Peça o que quer em português mesmo: *"monta um workflow que recebe um webhook,
   valida o payload e grava no Postgres"*.
3. O Claude puxa a skill certa sozinho — `n8n-workflow-patterns` para o desenho,
   `n8n-node-configuration` na hora de configurar, `n8n-validation-expert` quando a
   validação reclamar.

Para usar em qualquer projeto, copie (ou faça symlink) as pastas de volta para
`~/.claude/skills/`.

### Fluxo típico

```
desenhar (workflow-patterns)
   → configurar nodes (node-configuration)
   → expressões e Code nodes (expression-syntax, code-javascript)
   → validar e corrigir (validation-expert)   ← 2-3 voltas é o normal
   → publicar/gerenciar via MCP (mcp-tools-expert)
```

### Combinando com o MCP n8n

A skill `n8n-mcp-tools-expert` pressupõe o servidor MCP **n8n-mcp** conectado — é
ele que dá busca de nodes, validação de configuração, biblioteca de templates e
deploy de workflows. Sem o MCP as outras seis continuam úteis: viram guia de
sintaxe, padrões e depuração.

---

## Licença / origem

Skills de uso interno INEMA, mantidas neste repositório.
