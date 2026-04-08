# Setup de Vibe Coding

## Hardware y suscripciones
- Mac Mini (Apple Silicon)
- Claude Max 5x (100€/mes)
- Google AI Pro (Gemini)
- Antigravity IDE (fork de VS Code con IA)

## Herramientas instaladas
- Homebrew, Node.js, Git, GitHub CLI (`gh`), Bun, NVM
- Claude Code (terminal + Antigravity)
- Gemini CLI, Codex CLI
- tmux (opcional, para ver agentes en paralelo)
- Obsidian (visor de [[wikis-personales]])
- Obsidian Web Clipper (extensión Chrome para clipear artículos a raw/)

## Configuración de Claude Code (~/.claude/settings.json)
```json
{
  "env": { "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1" },
  "permissions": {
    "allow": ["Bash(*)", "Read(*)", "Write(*)", "Edit(*)", "WebFetch(*)", "mcp__*"]
  }
}
```

## Skills instalados (~/.claude/skills/)

### Desarrollo
- react-best-practices, composition-patterns, web-design-guidelines (Vercel)
- deploy-to-vercel (Vercel)

### Diseño
- frontend-design (Anthropic oficial)
- bencium-innovative-ux-designer
- creative-director (20+ metodologías de diseño)

### Wiki / Second Brain
- second-brain (NicholasSpisak) — incluye 4 comandos:
  - /second-brain — scaffolding de nueva wiki
  - /second-brain-ingest — ingesta de fuentes
  - /second-brain-query — consultas contra la wiki
  - /second-brain-lint — health check mensual

### Otros
- humanizer (eliminar tono IA de textos)
- last30days (research en Reddit, X, YouTube, HN)

### Por proyecto (no global)
- ui-ux-pro-max (instalar con `uipro init --ai claude`)

## Plugins
- Superpowers (obra) — TDD, systematic-debugging, subagent-driven-development
- code-simplifier (Anthropic)
- Telegram channel (notificaciones al móvil)
- Caveman (JuliusBrussee) — reduce output tokens 65-87%. Ver [[optimizacion-tokens]]

## Channels

```bash
claude --channels plugin:telegram@claude-plugins-official
```

Claude accesible vía Telegram/Discord/iMessage dentro de la sesión activa. Eventos llegan con contexto completo. Ver [[claude-code-features-avanzadas]].

## Hooks configurables

Además de PreToolUse/PostToolUse, hay hooks avanzados poco conocidos:
- **TaskCompleted** — vetar que Claude marque tarea como completada (exit 2)
- **CwdChanged** — auto-reload env (direnv) en monorepo
- **FileChanged** — reaccionar a cambios en archivos específicos (ej: security audit en package-lock.json)

Ver [[claude-code-features-avanzadas]] para detalles y ejemplos.
