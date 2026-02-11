---
name: k8s-audit-kubeconfig
description: Audit kubeconfig clusters and recommend cleanup
allowed-tools: mcp__plugin_kubestellar-ops_kubestellar-ops__*
---

## Your task

Use the kubestellar-ops MCP tools to audit all clusters in the user's kubeconfig.

1. Use `audit_kubeconfig` to check connectivity to all configured clusters
2. Present the results showing:
   - Which clusters are accessible (with their Kubernetes versions)
   - Which clusters are inaccessible (with error reasons)
3. If there are inaccessible clusters, provide the cleanup commands to remove stale contexts, clusters, and users

This helps users maintain a clean kubeconfig by identifying and removing stale cluster configurations.

Do not use any other tools besides the kubestellar-ops MCP tools.
