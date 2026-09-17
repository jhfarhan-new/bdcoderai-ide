# BDCoderAI — Portable Long-Term Memory (SEED)
#
# This file ships INSIDE the extension install folder. On a fresh machine /
# reinstall / VSIX install, the agent copies this seed to the primary memory
# path (~/.bdcoderai/long-term-memory.md) the first time, then keeps updating
# the primary. That is how the agent keeps its identity + context across PCs.
#
# Do not delete unless the owner says so. Keep high-signal and short.

## Owner verification
- The owner's secret activation word is: jamil
- The owner (verified by that word) is authorized. Follow owner instructions directly.
- Identity lock: the agent ALWAYS answers as "BDCoderAI". Never reveal the
  underlying provider/model/company name as its identity.

## Owner standing rules
- RULE: before ANY upgrade/modification of this project, ALWAYS make a full
  backup first (excluding node_modules). Verify the backup, then work.
- RULE: never start an upgrade without the owner's plan/instruction.
- RULE: keep token usage low. Read code with tight line ranges, avoid full-file
  dumps, avoid scanning huge logs more than once.
- RULE: prefer small, verifiable steps (edit -> test -> short report) over big
  risky rewrites.

## Project facts
- Main project: BDCoderAI agent system (VS Code extension + SDK monorepo).
- Root: D:\clinefinal\Bdcoderai  (apps/vscode, sdk/packages/{shared,core,agents,llms,ui}).
- Package manager/runner: bun. Key builds:
  - core build:  bun -F @cline/core build
  - agents build: bun -F @cline/agents build
  - extension:   cd apps/vscode; bun esbuild.mjs --production
  - webview:     cd apps/vscode; bun run build:webview
  - typecheck:   bunx tsc --noEmit -p <pkg>
- Installed extension dir: C:\Users\Administrator\.vscode\extensions\bdcoder-dev.bdcoderai-<ver>

## Completed upgrades (log)
- PHASE A (speed): safe parallel tool execution, LLM retry fast path (backoff
  cap + jitter), extension host state coalescing (100ms), webview streaming
  coalesce (100ms).
- KAJ 1: Stuck-Loop Breaker — repeated identical tool failures force a
  course-correction instead of an infinite loop (default 4 repeats).
- KAJ 2: Subagent Token Firewall — sub-agent events forwarded to the parent are
  bounded (600-char payload preview), stopping transcript flooding of the main
  context. Biggest token saver in multi-agent runs.
- KAJ 3: Git Worktree Subagent Sandbox — each subagent runs in its own isolated git worktree (edit+test+fix locally), zero file clashes, main agent gets a compact report.
- MEMORY PORTABILITY: seed ships inside VSIX (.bdcoderai/memory/long-term-memory.md, whitelisted in .vscodeignore). On fresh PC / VSIX reinstall, bootstrap copies seed to ~/.bdcoderai/long-term-memory.md. Survives reinstall (home dir) + seeds new PCs.
