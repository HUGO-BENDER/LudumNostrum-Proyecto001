@AGENTS.md

## Estándares comunes (importados del framework)

@../IA/standards/coding.md
@../IA/standards/git.md
@../IA/standards/definition-of-done.md

## Claude Code

- La sesión principal arranca como el agente `orquestador` (`.claude/settings.json`).
- Subagentes en `.claude/agents/`, skills en `.claude/skills/`.
- No edites `.claude/agents` ni `.claude/skills` aquí: se sincronizan desde `../IA/template` con `Sync-Agents.ps1`.
