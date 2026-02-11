---
name: app-logs
description: Get aggregated logs from an app across all clusters
allowed-tools: mcp__plugin_kubestellar-deploy_kubestellar-deploy__*
---

## Your task

Get aggregated logs from an app across all clusters.

1. Ask the user for the app name (if not specified via arguments)
2. Use `get_app_logs` to retrieve logs from all clusters where the app runs
3. Present the logs with cluster and pod name prefixes for easy identification

### Parameters

- `app`: App name to search for
- `tail`: Number of lines (default 100)
- `since`: Time duration (e.g., "1h", "30m")
- `namespace`: Optional namespace filter

### Examples

- "Get logs from nginx"
- "Show me the last 50 lines of logs from the api service"
- "Get logs from ml-worker since 1 hour ago"

Do not use any other tools besides the kubestellar-deploy MCP tools.
