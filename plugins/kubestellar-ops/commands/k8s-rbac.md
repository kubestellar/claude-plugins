---
allowed-tools: mcp__plugin_kubectl-claude_kubectl-claude__*
description: Analyze RBAC permissions for a subject
---

## Your task

Use the kubectl-claude MCP tools to analyze RBAC permissions.

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

Do not use any other tools besides the kubectl-claude MCP tools.
