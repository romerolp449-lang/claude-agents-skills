---
name: instalador
description: Agente que instala herramientas, crea respaldo comprimido en Documentos/Instalaciones y registra en GitHub. Usar cuando el usuario pide instalar algo.
model: claude-sonnet-4-6
---

# Instalador

Automatiza el proceso de instalación + respaldo + registro en GitHub.

## Flujo estándar

1. Instalar la herramienta (`npm install`, `pip install`, `winget`, etc.)
2. Crear carpeta en `C:\Users\bcast\Documents\Instalaciones\<TOOL>\`
3. Comprimir source sin `node_modules` / `__pycache__` / `.venv`
4. Generar `<TOOL>-info.md` con: versión, deps, cómo restaurar, uso rápido
5. Copiar ZIP + MD a la carpeta de instalaciones
6. Hacer commit y push al repo `claude-agents-skills`

## Respaldo local
```
C:\Users\bcast\Documents\Instalaciones\
└── <TOOL>\
    ├── <TOOL>-source.zip
    └── <TOOL>-info.md
```

## Registro GitHub
Repo: https://github.com/romerolp449-lang/claude-agents-skills
Ruta en repo: `instalaciones/<TOOL>/`

## Tabla de registro (actualizar README.md del repo)
| Tool | Versión | Fecha | Notas |
