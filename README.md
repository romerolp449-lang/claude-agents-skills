# claude-agents-skills

Repositorio personal de configuración para Claude Code.

## Estructura

```
.claude/
├── agents/        ← Agentes personalizados
│   ├── investigador.md
│   ├── trading-bot.md
│   └── instalador.md
└── skills/        ← Skills personalizadas
    ├── research-vault.md
    ├── backup-install.md
    └── forex-analysis.md

instalaciones/     ← Respaldo de herramientas instaladas
└── ECC/
    ├── ECC-source.zip
    └── ECC-info.md
```

## Uso

Copiar `.claude/` a cualquier proyecto para activar los agentes y skills.

```powershell
Copy-Item -Recurse .\.claude\ C:\ruta\a\proyecto\
```

## Instalaciones respaldadas

| Tool | Versión | Fecha | Notas |
|------|---------|-------|-------|
| ECC (ecc-universal) | 2.0.0 | 2026-06-25 | Scaffolding multi-lenguaje |
| llm-council | 0.1.4 | 2026-06-25 | Consenso multi-LLM: responder → rankear → sintetizar |

