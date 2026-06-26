---
name: llm-council
description: Usa múltiples LLMs para responder una pregunta: cada modelo responde, se rankean entre sí anónimamente, y un "chairman" sintetiza la respuesta final. Activar cuando el usuario quiera consenso multi-modelo, segunda opinión de varios LLMs, o validación cruzada de una respuesta.
---

# LLM Council Skill

Implementación del patrón LLM Council (Karpathy): 3 etapas — responder, rankear, sintetizar.

## Cuándo usar
- El usuario quiere comparar qué dicen varios LLMs sobre algo
- Necesita una respuesta validada por múltiples modelos
- Quiere saber qué modelo da mejores respuestas en un tema

## Instalado como
```powershell
npm install -g llm-council   # v0.1.4
```

## Setup rápido en un proyecto

```powershell
# En la carpeta del proyecto
npm init -y
npm install llm-council
```

Crear `council.mjs`:

```javascript
import { LLMCouncil } from 'llm-council';

const council = new LLMCouncil({
  provider: 'openrouter',
  apiKey: process.env.OPENROUTER_API_KEY,
  models: [
    'openai/gpt-4o',
    'anthropic/claude-sonnet-4-6',
    'google/gemini-2.0-flash-001',
  ],
  chairmanModel: 'anthropic/claude-sonnet-4-6',
  verbose: true,
});

const result = await council.run(process.argv[2]);
console.log('\n=== RESPUESTA FINAL ===');
console.log(result.stage3.response);
console.log('\n=== RANKINGS ===');
result.stage2.aggregate_rankings.forEach(r =>
  console.log(`  ${r.model}: rank promedio ${r.average_rank}`)
);
```

Ejecutar:
```powershell
$env:OPENROUTER_API_KEY="sk-or-..."
node council.mjs "¿Cuál es la mejor estrategia para trading de bajo riesgo?"
```

## Con Ollama (sin API key, modelos locales)

```javascript
const council = new LLMCouncil({
  provider: 'ollama',
  models: ['llama3', 'mistral', 'gemma2'],
  chairmanModel: 'llama3',
  timeout: 300_000,
  verbose: true,
});
```

## Flujo de 3 etapas

| Etapa | Qué pasa |
|-------|----------|
| Stage 1 | Todos los modelos responden en paralelo |
| Stage 2 | Cada modelo rankea las respuestas de los demás (anónimas: A, B, C) |
| Stage 3 | El chairman sintetiza respuesta final con todo el contexto |

## Referencia
- npm: https://npm.im/llm-council
- Patrón original: https://github.com/karpathy/llm-council
