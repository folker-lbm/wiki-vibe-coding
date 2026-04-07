# Setup de Vibe Coding

## Hardware y suscripciones
- Mac Mini (Apple Silicon)
- Claude Max 5x (100€/mes)
- Google AI Pro (Gemini)
- Antigravity IDE (fork de VS Code con IA)

## Herramientas instaladas
- Homebrew, Node.js, Git, GitHub CLI (`gh`), Bun
- Claude Code (terminal + Antigravity)
- Gemini CLI, Codex CLI (disponibles para orquestar en el futuro)
- tmux (opcional, para ver agentes en paralelo)

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

### Otros
- humanizer (eliminar tono IA de textos)
- last30days (research en Reddit, X, YouTube, HN)

### Por proyecto (no global)
- ui-ux-pro-max (instalar con `uipro init --ai claude`)

## Plugins
- Superpowers (obra) — TDD, systematic-debugging, subagent-driven-development
- code-simplifier (Anthropic)
- Telegram channel (notificaciones al móvil)
