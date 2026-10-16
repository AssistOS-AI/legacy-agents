# legacy-agents

Ploinky agents moved out of AssistOSExplorer, AchillesCLI and proxies. Origin: `https://github.com/AssistOS-AI/legacy-agents.git`. Agent identities are `agent:legacy-agents/<agent>`; container names start with `ploinky_legacy-agents_<agent>_`.

`AGENTS.md` is the single instruction file in this repository, at the root and in each agent folder. Do not add `CLAUDE.md` files.

## Mandatory Reading Order

1. The workspace root `AGENTS.md` for workspace conventions, then this file and the `AGENTS.md` of the agent you are editing.
2. The agent's `docs/index.html`, `docs/wiki.html` and `docs/specs/matrix.md`, plus its coding-style spec (`DS001-coding-style.md`) where it has one.
3. Where an agent's `AGENTS.md` says "read `../AGENTS.md`" for coding style, this file defers to the agent's own coding-style spec and to the AssistOSExplorer conventions (`../AssistOSExplorer/docs/specs/DS001-coding-style.md`).

## Agents, tests and enablement

Run each command from the agent directory. Node.js 20 or later.

| Agent | Test command | Who enables it |
| --- | --- | --- |
| `multimedia` | none (no automated tests) | Explorer: `legacy-agents/multimedia global no-wait` |
| `soplangAgent` | `npm install --no-package-lock && npm test` (needs the `soplang` and `flexsearch` packages) | Explorer: `legacy-agents/soplangAgent global no-wait`; Explorer also calls it by name at runtime |
| `tasksAgent` | `node --test tests/unit/*.test.mjs` | Explorer: `legacy-agents/tasksAgent global` |
| `webAssist` | `node tests/runAll.mjs` (needs the sibling `../ploinky` checkout and `achillesAgentLib` resolvable from `webAssist/node_modules`) | Explorer: `legacy-agents/webAssist no-wait` |
| `GPTResearcher` | `node --test test/*.test.mjs` | copilot-agents `research-agents` manifest: `legacy-agents/GPTResearcher global no-wait` |
| `searchAgent` | `node --test test/*.test.mjs` | The roboTeam `launch-gpt-researcher` skill (in AssistOSExplorer `roboTeamAgent/`) references `legacy-agents/searchAgent`; the manifest declares `startup: manual` |
| `opencode-free` | `node --test test/*.test.mjs` (`chain-soul.test.mjs` runs only when `OPENCODE_FREE_PLOINKY_DIR` names a Ploinky checkout; `SOUL_SRC` or `EXPLORER_ROOT` locate Soul Gateway sources) | Optional; no default enabler |

## Cross-repository rules

- The browser-served `soplangAgent/IDE-plugins/scripta-variants/scripta-variants.js` imports Explorer code through the absolute URL `/explorer/shared/document/scripta-state.js`. Do not reintroduce relative `../../../explorer/...` imports.
- `searchAgent` DPU secret grants are keyed by the principal `agent:legacy-agents/searchAgent`. It must match `dpuAgent` `default-agent-policies.mjs` in AssistOSExplorer.
- Test fixtures that mint grants use the sibling `../ploinky` checkout and fail when it is missing. Do not replace them with hand-written identities.
- Each agent's `docs/partials-loader.js` imports `../../docs/documentation-breadcrumb.js`; keep `docs/documentation-breadcrumb.js` at the repository root.
- `opencode-free` and `searchAgent` keep their own MIT `LICENSE`. Add no repository-wide licence without the owner's decision.
