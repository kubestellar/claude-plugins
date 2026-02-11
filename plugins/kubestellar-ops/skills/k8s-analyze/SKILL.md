---
name: k8s-analyze
description: Analyze a Kubernetes namespace
allowed-tools: mcp__plugin_kubestellar-ops_kubestellar-ops__*
---

## Your task

Use the kubestellar-ops MCP tools to perform a comprehensive analysis of a Kubernetes namespace.

1. Ask the user which cluster and namespace to analyze (if not specified, use the default context and default namespace)
2. Use `analyze_namespace` to get a comprehensive overview
3. Provide insights on:
   - Workload health (pods, deployments)
   - Resource usage and limits
   - Potential issues and recommendations

Do not use any other tools besides the kubestellar-ops MCP tools.
