---
name: k8s-rbac
description: Analyze RBAC permissions for a subject
allowed-tools: mcp__plugin_kubestellar-ops_kubestellar-ops__*
---

## Your task

Use the kubestellar-ops MCP tools to analyze RBAC permissions.

1. Ask the user for:
   - The subject type (user, group, or serviceaccount)
   - The subject name
   - The cluster (optional, defaults to current context)
   - The namespace (for serviceaccounts)

2. Use `analyze_subject_permissions` to get all roles, bindings, and effective permissions

3. Provide a report showing:
   - All RoleBindings and ClusterRoleBindings for the subject
   - Effective permissions (what actions they can perform)
   - Any overly permissive access (cluster-admin, wildcards, etc.)
   - Security recommendations

Do not use any other tools besides the kubestellar-ops MCP tools.
