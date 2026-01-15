# KubeStellar Claude Plugins

Official Claude Code plugin marketplace for [KubeStellar](https://kubestellar.io) - multi-cluster Kubernetes management tools.

## Installation

Add the KubeStellar marketplace to Claude Code:

```
/plugin marketplace add kubestellar/claude-plugins
```

Then go to `/plugin` → **Discover** tab → Install **kubectl-claude**.

## kubectl-claude Plugin

AI-powered multi-cluster Kubernetes management with 30 MCP tools and 7 slash commands.

### Slash Commands

| Command | Description |
|---------|-------------|
| `/k8s-health` | Check health of all Kubernetes clusters |
| `/k8s-issues` | Find issues across clusters (pods, deployments, events) |
| `/k8s-analyze` | Comprehensive namespace analysis |
| `/k8s-security` | Security audit (privileged, root, host access) |
| `/k8s-rbac` | Analyze RBAC permissions for a subject |
| `/k8s-audit-kubeconfig` | Audit kubeconfig clusters and recommend cleanup |
| `/k8s-ownership` | Set up and manage resource ownership tracking with OPA Gatekeeper |

### MCP Tools

**Cluster Management**
| Tool | Description |
|------|-------------|
| `list_clusters` | Discover clusters from kubeconfig |
| `get_cluster_health` | Check cluster health status |
| `get_nodes` | List cluster nodes with status |
| `audit_kubeconfig` | Audit all clusters for connectivity and recommend cleanup |

**Workload Tools**
| Tool | Description |
|------|-------------|
| `get_pods` | List pods with filtering options |
| `get_deployments` | List deployments |
| `get_services` | List services |
| `get_events` | Get recent events |
| `describe_pod` | Get detailed pod information |
| `get_pod_logs` | Retrieve pod logs |

**RBAC Analysis**
| Tool | Description |
|------|-------------|
| `get_roles` | List Roles in a namespace |
| `get_cluster_roles` | List ClusterRoles |
| `get_role_bindings` | List RoleBindings |
| `get_cluster_role_bindings` | List ClusterRoleBindings |
| `can_i` | Check if you can perform an action |
| `analyze_subject_permissions` | Full RBAC analysis for any subject |
| `describe_role` | Detailed view of Role/ClusterRole rules |

**Diagnostic Tools**
| Tool | Description |
|------|-------------|
| `find_pod_issues` | Find CrashLoopBackOff, ImagePullBackOff, OOMKilled, pending pods |
| `find_deployment_issues` | Find stuck rollouts, unavailable replicas, ReplicaSet errors |
| `check_resource_limits` | Find pods without CPU/memory limits |
| `check_security_issues` | Find privileged containers, root users, host network |
| `analyze_namespace` | Comprehensive namespace analysis |
| `get_warning_events` | Get only Warning events |
| `find_resource_owners` | Find who owns/manages resources via managedFields, labels, annotations |

**OPA Gatekeeper Policy Tools**
| Tool | Description |
|------|-------------|
| `check_gatekeeper` | Check if OPA Gatekeeper is installed and healthy |
| `get_ownership_policy_status` | Get ownership policy configuration and violation count |
| `list_ownership_violations` | List resources missing required ownership labels |
| `install_ownership_policy` | Install ownership labels policy (dryrun/warn/enforce) |
| `set_ownership_policy_mode` | Change policy enforcement mode |
| `uninstall_ownership_policy` | Remove the ownership policy |

### Natural Language Usage

Once installed, ask questions like:
- "List my Kubernetes clusters"
- "Find pods with issues in the production namespace"
- "Check for security misconfigurations in my cluster"
- "What permissions does the admin service account have?"
- "Show me warning events in kube-system"
- "Audit my kubeconfig and show stale clusters"

### Allow Tools Without Prompts

Add to `~/.claude/settings.json`:
```json
{
  "permissions": {
    "allow": [
      "mcp__plugin_kubectl-claude_kubectl-claude__*"
    ]
  }
}
```

### Prerequisites

Install kubectl-claude via Homebrew:
```bash
brew tap kubestellar/tap
brew install kubectl-claude
```

## About KubeStellar

KubeStellar is a flexible solution for multi-cluster Kubernetes configuration management. Learn more at [kubestellar.io](https://kubestellar.io).

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](https://github.com/kubestellar/kubestellar/blob/main/CONTRIBUTING.md).

## License

Apache License 2.0 - see [LICENSE](./LICENSE) for details.
