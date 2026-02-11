---
name: k8s-health
description: Check health of all Kubernetes clusters
allowed-tools: mcp__plugin_kubestellar-ops_kubestellar-ops__*
---

## Your task

Use the kubestellar-ops MCP tools to check the health of all available Kubernetes clusters.

1. First, use `list_clusters` to discover all available clusters
2. Then use `get_cluster_health` on each cluster to check its health status
3. Summarize any issues found with recommended actions

Do not use any other tools besides the kubestellar-ops MCP tools.
