---
name: graphiti
description: Usa grafos de conocimiento para dar memoria persistente a agentes de IA. Activar cuando el usuario quiera que un agente recuerde contexto entre sesiones, construya una base de conocimiento incremental, o conecte información relacionada en un grafo.
---

# Graphiti Skill

Repo: https://github.com/getzep/graphiti (27,969 estrellas)
Instalado: graphiti-core 0.29.2

## Qué hace
Grafo de conocimiento en tiempo real — el agente recuerda hechos, personas, eventos y sus relaciones. Se actualiza de forma incremental sin recomputar todo.

## Requisitos
- Neo4j corriendo en bolt://localhost:7687
- API key de un LLM (OpenAI, Anthropic, Groq)

## Setup rápido
```python
from graphiti_core import Graphiti

g = Graphiti("bolt://localhost:7687", "neo4j", "password")
await g.build_indices_and_constraints()

# Agregar conocimiento
await g.add_episode(name="sesion_1", episode_body="El usuario opera un bot Forex en MT4 con Groq")

# Buscar en el grafo
results = await g.search("bot forex")
for r in results:
    print(r.fact)
```

## Cuándo usar
- Agente que necesita recordar entre conversaciones
- Base de conocimiento que crece con el tiempo
- Conectar entidades relacionadas (personas, eventos, conceptos)
