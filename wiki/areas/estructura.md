# Estructura de Carpetas

## Reutilizables (escritorio)
```
~/Desktop/Vibe Coding/
├── Agentes/           ← 6 .md maestros
├── commands/          ← 3 slash commands
├── design-systems/    ← Un design system por marca/proyecto
├── workflows/         ← Documentos de proceso
└── prompts/           ← Prompts reutilizables
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
