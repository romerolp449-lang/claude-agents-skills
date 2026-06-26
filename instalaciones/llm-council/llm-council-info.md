# llm-council — Registro de Instalación
**Fecha:** 2026-06-25
**Fuente:** https://npm.im/llm-council
**Versión:** 0.1.4
**Tipo:** Librería TypeScript (no CLI)
**Instalado:** global (`npm install -g llm-council`)

## Qué hace
Implementa el patrón LLM Council de Karpathy:
1. **Stage 1:** N modelos responden la query en paralelo
2. **Stage 2:** Cada modelo rankea las respuestas de los demás (anónimas)
3. **Stage 3:** Un modelo "chairman" sintetiza la respuesta final

## Proveedores soportados
- **OpenRouter** — requiere `OPENROUTER_API_KEY`
- **Ollama** — modelos locales, sin API key

## Uso básico (OpenRouter)
```typescript
import { LLMCouncil } from 'llm-council';

const council = new LLMCouncil({
  provider: 'openrouter',
  apiKey: process.env.OPENROUTER_API_KEY!,
  models: [
    'openai/gpt-4o',
    'anthropic/claude-sonnet-4-6',
    'google/gemini-2.0-flash-001',
  ],
  chairmanModel: 'anthropic/claude-sonnet-4-6',
  verbose: true,
});

const result = await council.run('Tu pregunta aquí');
console.log(result.stage3.response); // respuesta final sintetizada
```

## Uso básico (Ollama — local)
```typescript
const council = new LLMCouncil({
  provider: 'ollama',
  models: ['llama3', 'mistral', 'gemma2'],
  chairmanModel: 'llama3',
  timeout: 300_000,
  verbose: true,
});
```

## Output
```json
{
  "query": "...",
  "stage1": [{ "model": "...", "response": "..." }],
  "stage2": { "aggregate_rankings": [...] },
  "stage3": { "model": "...", "response": "respuesta final" },
  "error": null
}
```

## Restaurar
```powershell
npm install -g llm-council
```
