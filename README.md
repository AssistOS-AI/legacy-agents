# legacy-agents

Legacy Ploinky agents retained outside the default Explorer and proxies repositories. Each top-level directory is one agent (`<agent>/manifest.json`), installed by Ploinky as the `legacy-agents` repository, so agent identities are `agent:legacy-agents/<agent>` and container names start with `ploinky_legacy-agents_<agent>_`.

| Agent | Moved from | Enabled by |
| --- | --- | --- |
| `multimedia` | AssistOSExplorer | Explorer manifest |
| `soplangAgent` | AssistOSExplorer | Explorer manifest |
| `tasksAgent` | AssistOSExplorer | Explorer manifest |
| `webAssist` | AssistOSExplorer | Explorer manifest |
| `GPTResearcher` | AchillesCLI | copilot-agents `research-agents` manifest |
| `searchAgent` | proxies | Enabled on demand by the roboTeam `launch-gpt-researcher` skill |
| `opencode-free` | proxies | Optional; not enabled by default |

Consumers register this repository through their manifest `repos{}` entry `"legacy-agents": "https://github.com/AssistOS-AI/legacy-agents.git"` and enable agents as `legacy-agents/<agent>`.

There is no repository-wide licence file. `opencode-free` and `searchAgent` carry the MIT licence they had in proxies; see `AGENTS.md` and the per-agent `LICENSE` files. Documentation starts at [docs/index.html](docs/index.html) and each agent's own `docs/index.html`.
