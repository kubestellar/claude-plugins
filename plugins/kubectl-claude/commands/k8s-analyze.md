---
allowed-tools: mcp__plugin_kubectl-claude_kubectl-claude__*
description: Analyze a Kubernetes namespace
---

## Your task

Use the kubectl-claude MCP tools to perform a comprehensive analysis of a Kubernetes namespace.

1. Ask the user which cluster and namespace to analyze (if not specified, use the default context and default namespace)
2. Use `analyze_namespace` to get a comprehensive overview
3. Provide insights on:
   - Workload health (pods, deployments)
   - Resource usage and limits
   - Potential issues and recommendations

Do not use any other tools besides the kubectl-claude MCP tools.
