# kubectl-claude

AI-powered multi-cluster Kubernetes management for Claude Code.

## Features

### Cluster Management
- **list_clusters** - Discover all Kubernetes clusters from kubeconfig
- **get_cluster_health** - Check cluster health status
- **get_nodes** - List cluster nodes with status

### Workload Tools
- **get_pods** - List pods with filtering options
- **get_deployments** - List deployments
- **get_services** - List services
- **get_events** - Get recent events for troubleshooting
- **describe_pod** - Get detailed pod information
- **get_pod_logs** - Retrieve pod logs

### RBAC Analysis
- **get_roles** - List Roles in a namespace
- **get_cluster_roles** - List ClusterRoles
- **get_role_bindings** - List RoleBindings
- **get_cluster_role_bindings** - List ClusterRoleBindings
- **can_i** - Check if you can perform an action
- **analyze_subject_permissions** - Full RBAC analysis for any subject
- **describe_role** - Detailed view of Role/ClusterRole rules

## Prerequisites

Install kubectl-claude binary:

```bash
# macOS (Homebrew)
brew install kubestellar/tap/kubectl-claude

# Or download from releases
# https://github.com/kubestellar/kubectl-claude/releases
```

## Example Usage

Once installed, you can ask Claude:

- "List all my Kubernetes clusters"
- "Show me pods that aren't running in the production namespace"
- "What permissions does the admin service account have?"
- "Can I create deployments in the default namespace?"
- "Why is my pod crashing?" (with describe_pod + get_pod_logs)
- "Analyze RBAC for user john@example.com"

## Links

- [GitHub Repository](https://github.com/kubestellar/kubectl-claude)
- [KubeStellar](https://kubestellar.io)
