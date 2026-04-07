# Workflow: Proyecto Nuevo

```bash
# 1. Crear y estructurar
mkdir ~/proyecto && cd ~/proyecto
mkdir -p .claude/agents .claude/commands misc/strategy misc/design/ux misc/design/ui misc/design/previews misc/design/references misc/review

# 2. Copiar agentes y comandos
cp ~/Desktop/Vibe\ Coding/Agentes/*.md .claude/agents/
cp ~/Desktop/Vibe\ Coding/commands/*.md .claude/commands/

# 3. Crear CLAUDE.md (corto: qué es, qué resuelve, para quién)
# 4. Crear o copiar DESIGN-SYSTEM.md
# 5. cp CLAUDE.md GEMINI.md
# 6. Copiar archivos de referencia del proyecto
# 7. uipro init --ai claude

# 8. Git + GitHub
git init && git add -A && git commit -m "setup inicial"
gh repo create nombre --private --source=. --push

# 9. Arrancar
claude --dangerously-skip-permissions --channels plugin:telegram@claude-plugins-official
```

Ver también: [[flujo-de-trabajo]] para el pipeline de trabajo una vez arrancado, [[estructura]] para detalle de carpetas, [[setup]] para herramientas necesarias.
