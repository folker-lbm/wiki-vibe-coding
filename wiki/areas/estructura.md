# Estructura de Carpetas

## Reutilizables (escritorio)
```
~/Desktop/Vibe Coding/
├── Agentes/           ← 6 .md maestros
├── commands/          ← 3 slash commands
├── design-systems/    ← Un design system por marca/proyecto
├── workflows/         ← Documentos de proceso
├── prompts/           ← Prompts reutilizables
└── archivo-obsoleto/  ← Versiones antiguas archivadas
```

## Global (una vez por ordenador)
```
~/.claude/
├── settings.json      ← Permisos, Agent Teams
├── skills/            ← Skills (react-best-practices, humanizer, etc.)
├── plugins/           ← Superpowers, code-simplifier
└── channels/telegram/ ← Token del bot
```

## Por proyecto
```
~/proyecto/
├── .claude/
│   ├── agents/        ← 6 agentes (copiados de Vibe Coding)
│   └── commands/      ← 3 comandos (copiados de Vibe Coding)
├── CLAUDE.md          ← Contexto del proyecto (corto, ~1K tokens)
├── DESIGN-SYSTEM.md   ← Identidad visual del proyecto
├── GEMINI.md          ← Copia de CLAUDE.md
├── misc/
│   ├── strategy/      ← Strategy briefs
│   ├── design/
│   │   ├── ux/        ← Specs de flujos
│   │   ├── ui/        ← Specs visuales
│   │   ├── previews/  ← HTML interactivos para aprobar
│   │   └── references/← Screenshots de inspiración
│   ├── review/        ← Audits, QA reports, evaluaciones
│   └── coding-team/   ← Task briefs
└── src/               ← Código
```

## Wikis personales

Basadas en el patrón [[second-brain|LLM Wiki de Karpathy]]. Cada wiki es un repo público en GitHub. Ver [[wikis-personales]] para detalle.

```
wiki-nombre/
├── CLAUDE.md          ← Instrucciones del agente mantenedor
├── raw/               ← Fuentes originales (NUNCA modificar)
│   └── assets/
└── wiki/              ← Conocimiento compilado (el LLM escribe esto)
    ├── areas/
    ├── ideas/
    ├── referencias/
    ├── workflows/
    ├── diario/        ← Solo en wiki-personal
    ├── index.md
    └── log.md
```
