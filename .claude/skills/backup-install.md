---
name: backup-install
description: Después de cada instalación, comprime el source y guarda en Documentos/Instalaciones + push a GitHub.
---

# Backup Install Skill

Ejecutar después de cualquier instalación nueva.

## Pasos

```powershell
# 1. Crear carpeta
New-Item -ItemType Directory -Force -Path "C:\Users\bcast\Documents\Instalaciones\<TOOL>"

# 2. Comprimir (excluir node_modules, __pycache__, .venv, dist)
$files = Get-ChildItem -Path <SOURCE> -Recurse -File |
    Where-Object { $_.FullName -notmatch '\\(node_modules|__pycache__|\.venv|dist)\\' }
Compress-Archive -Path $files.FullName -DestinationPath "...\<TOOL>-source.zip" -Force

# 3. Generar markdown de registro
# (incluir: nombre, versión, fecha, deps, cómo restaurar, uso)

# 4. Push a GitHub
cd C:\Users\bcast\claude-agents-skills
git add instalaciones/<TOOL>/
git commit -m "respaldo: agregar <TOOL> v<VERSION>"
git push
```
