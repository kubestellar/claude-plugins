---
name: app-status
description: Show the status of an app across all clusters
allowed-tools: mcp__plugin_kubestellar-deploy_kubestellar-deploy__*
---

## Your task

Show the status of an app across all clusters.

1. Ask the user for the app name (if not specified via arguments)
2. Use `get_app_status` to get unified status across all clusters
3. Use `get_app_instances` to find all instances of the app
4. Present a summary showing:
   - Which clusters the app is running on
   - Replica counts and health status per cluster
   - Overall health (healthy, degraded, failed)
   - Any issues detected

### Examples

- "What's the status of nginx?"
- "Is my api service healthy?"
- "Show me the status of the ml-pipeline app"

Do not use any other tools besides the kubestellar-deploy MCP tools.
