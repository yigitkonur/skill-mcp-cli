# skill-mcp-cli workspace

This workspace contains:

1. **mcp-cli source repo** (`./mcp-cli`) — the Bun CLI implementation.
2. **Documentation set** (`./docs`) — practical guidance for configuration, commands, testing, troubleshooting, and internals.

## Workspace map

- `docs/getting-started.md` — install + first commands
- `docs/configuration.md` — stdio/http config, filtering, env substitution
- `docs/commands.md` — `info`, `call`, `grep`, flags, stream behavior
- `docs/testing-guide.md` — mandatory MCP verification flow
- `docs/troubleshooting.md` — error codes + recovery patterns
- `docs/advanced-usage.md` — chaining, stream separation, env variables
- `docs/internals.md` — daemon and retry internals
- `mcp-cli/SKILL.md` — Codex skill entry point (lean orchestrator)
- `mcp-cli/references/*.md` — detailed skill playbooks loaded on demand

## Skill layout (inside `mcp-cli/`)

```text
mcp-cli/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── testing-flow.md
    ├── configuration-and-arguments.md
    ├── output-debugging-and-chaining.md
    └── errors-and-recovery.md
```

## Validation commands

Run from `mcp-cli/`:

```bash
python3 /Users/yigitkonur/.codex/skills/.system/skill-creator/scripts/quick_validate.py ./
bun run src/index.ts -c ./mcp_servers.json info filesystem
bun run src/index.ts -c ./mcp_servers.json call filesystem read_file '{"path":"./README.md","head":2}'
```

## Notes

- The top-level workspace folder is not the git repository.
- Git operations (commit/push) run in `./mcp-cli`.
