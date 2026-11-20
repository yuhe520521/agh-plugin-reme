# AGH ReMe Memory

Connects to a [ReMe](https://github.com/agentscope-ai/ReMe) HTTP service to provide long-term memory search and management for AGH.

## Tools

| Tool | Description |
|------|-------------|
| `agh_reme_search` | Search ReMe long-term memory for relevant historical context |
| `agh_reme_auto_memory` | Capture conversation messages into ReMe memory (explicit call) |
| `agh_reme_auto_dream` | Run ReMe memory consolidation/dream (explicit call) |
| `agh_reme_health_check` | Check ReMe service health |
| `agh_reme_status` | Get ReMe service status |
| `agh_reme_list_files` | List memory files in the ReMe workspace |
| `agh_reme_load_file` | Load a specific memory file from ReMe |

## Configuration

Set the ReMe HTTP service endpoint via environment variables:

- `REME_URL` — Full URL (e.g., `http://127.0.0.1:2333`)
- `REME_HOST` — Host (defaults to `127.0.0.1`)
- `REME_PORT` — Port (defaults to `2333`)

ReMe's HTTP service does not use API-key authentication.

## Degradations from the Upstream Original

- **Auto memory capture**: Originally triggered automatically on session events via upstream hooks. In AGH, this is an explicit `agh_reme_auto_memory` tool call.
- **Auto dream schedule**: Originally ran on a daily cron schedule in the upstream host. In AGH, this is an explicit `agh_reme_auto_dream` tool call.
- **Memory guidance injection**: Originally injected into agent sessions on startup. In AGH, guidance is included in the `agh_reme_search` tool description.
- **Status gateway**: Originally an upstream TypertRemoteService for the status page. In AGH, replaced by the `agh_reme_status` tool.

## Requirements

- A running ReMe HTTP service (start with `reme start workspace_dir=/path/to/workspace`)
- Node.js >= 24.10