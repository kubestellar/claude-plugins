---
allowed-tools: mcp__plugin_kubectl-claude_kubectl-claude__*
description: Find issues across Kubernetes clusters
---

## Your task

Use the kubectl-claude MCP tools to find all issues across Kubernetes clusters.

1. Use `list_clusters` to get all available clusters
2. For each cluster, check for:
   - Pod issues using `find_pod_issues` (CrashLoopBackOff, ImagePullBackOff, OOMKilled, pending pods)
   - Deployment issues using `find_deployment_issues` (stuck rollouts, unavailable replicas)
   - Warning events using `get_warning_events`

3. Provide a summary of all problems found organized by cluster, with severity and recommended actions.

Do not use any other tools besides the kubectl-claude MCP tools.
