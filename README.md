# skill-mcp-cli

```bash
npx skills add yigitkonur/skill-mcp-cli
```

> [mcp server tester](https://github.com/yigitkonur/skill-mcp-server-tester) · [mcp-use code review](https://github.com/yigitkonur/skill-mcp-use) · [copilot review setup](https://github.com/yigitkonur/skill-copilot-review) · [devin review setup](https://github.com/yigitkonur/skill-devin-review-init)

A Codex/Claude Code skill for rigorous MCP server testing with `mcp-cli`.
It teaches agents to run direct CLI checks end-to-end (no helper scripts), validate both happy/error paths, and avoid false positives from daemon caching.

## what it does

When an agent builds or changes an MCP server, this skill enforces a strict verification workflow before it can report completion.

It provides:

- setup patterns for stdio/http servers
- command-by-command test flow (connect → inventory → inspect → call → break)
- JSON argument handling patterns (inline/stdin/heredoc/file/jq)
- output + stream handling guidance
- troubleshooting for ambiguous commands, missing tools, retries, and stale daemon connections
- a definition-of-done checklist

## what makes this useful

**built for real agent execution.**
The skill is optimized for terminal-first use: direct commands, sequential checks, and explicit pass/fail expectations.

**guards against stale confidence.**
It explicitly requires `MCP_NO_DAEMON=1` after rebuilds so agents verify the current server implementation, not cached daemon state.

**progressive disclosure.**
`SKILL.md` stays lean while detailed operational guidance lives in `references/*`.

## requirements

- `mcp-cli` (installed globally or runnable from source)
- `curl` (for installer flow)
- `jq` (recommended for downstream parsing patterns)

## file overview

| file | lines | what it covers |
|---|---:|---|
| `SKILL.md` | 77 | skill entrypoint, execution rules, reference routing |
| `references/testing-flow.md` | 117 | strict setup + connect/inventory/inspect/call/break + checklist |
| `references/configuration-and-arguments.md` | 83 | config templates, filtering, JSON argument patterns |
| `references/output-debugging-and-chaining.md` | 79 | output model, stream separation, chaining, env vars |
| `references/errors-and-recovery.md` | 68 | common failures, structured errors, retry and recovery |

## usage examples

```text
test my mcp server with mcp-cli before I mark this task done
```

```text
validate schema + happy path + bad input behavior for my MCP tool changes
```

```text
retest this MCP server after rebuild using MCP_NO_DAEMON=1
```

## scope

**built for:** testing MCP servers through `mcp-cli` with deterministic verification steps.

**not for:** building MCP servers from scratch, testing non-MCP systems, or replacing deeper protocol fuzz tools.

## license

mit
