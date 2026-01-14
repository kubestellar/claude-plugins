---
allowed-tools: mcp__plugin_kubectl-claude_kubectl-claude__*
description: Check for security issues in Kubernetes
---

## Your task

Use the kubectl-claude MCP tools to perform a security audit across Kubernetes clusters.

1. Use `list_clusters` to get all available clusters
2. For each cluster, use `check_security_issues` to find:
   - Privileged containers
   - Containers running as root
   - Host network/PID/IPC usage
   - Other security misconfigurations

3. Also use `check_resource_limits` to find pods without CPU/memory limits (resource exhaustion risk)

4. Provide a security report with:
   - Issues organized by severity (Critical, High, Medium, Low)
   - Affected workloads
   - Remediation recommendations

Do not use any other tools besides the kubectl-claude MCP tools.
