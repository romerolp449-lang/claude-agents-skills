# graphiti — Registro de Instalación
**Fecha:** 2026-06-25
**Repo:** https://github.com/getzep/graphiti (27,969 estrellas)
**Versión:** graphiti-core 0.29.2
**Tipo:** Librería Python

## Qué hace
Construye grafos de conocimiento en tiempo real para agentes de IA.
Actualiza el grafo de forma incremental sin recomputar todo el batch.

## Dependencias instaladas
- graphiti-core 0.29.2
- neo4j 6.2.0 (driver Python)
- openai 2.44.0
- tenacity, tqdm, backoff, posthog

## Requisitos para usar
- Base de datos Neo4j corriendo (local o cloud)
- API key de OpenAI, Anthropic u otro LLM compatible

## Uso básico
```python
from graphiti_core import Graphiti

client = Graphiti("bolt://localhost:7687", "neo4j", "password")
await client.build_indices_and_constraints()
await client.add_episode(name="episodio", episode_body="texto a recordar")
results = await client.search("qué recuerdas sobre X")
```

## Restaurar
```powershell
pip install graphiti-core
```
