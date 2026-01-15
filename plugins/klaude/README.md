# klaude

AI-powered multi-cluster Kubernetes management for Claude Code.

## Features

### Cluster Management
- **list_clusters** - Discover all Kubernetes clusters from kubeconfig
- **get_cluster_health** - Check cluster health status
- **get_nodes** - List cluster nodes with status
- **audit_kubeconfig** - Audit clusters for connectivity and recommend cleanup

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

### Diagnostic Tools
- **find_pod_issues** - Find CrashLoopBackOff, ImagePullBackOff, OOMKilled pods
- **find_deployment_issues** - Find stuck rollouts, unavailable replicas
- **check_resource_limits** - Find pods without CPU/memory limits
- **check_security_issues** - Find privileged containers, root users
- **analyze_namespace** - Comprehensive namespace analysis
- **get_warning_events** - Get only Warning events
- **find_resource_owners** - Find who owns/manages resources

### OPA Gatekeeper Policy Tools
- **check_gatekeeper** - Check if OPA Gatekeeper is installed
- **install_ownership_policy** - Install ownership labels policy
- **list_ownership_violations** - List resources missing ownership labels
- **set_ownership_policy_mode** - Change enforcement mode (dryrun/warn/enforce)

### Upgrade Tools
- **detect_cluster_type** - Detect distribution (OpenShift, EKS, GKE, AKS, kubeadm)
- **get_cluster_version_info** - Get current version and available upgrades
- **check_olm_operator_upgrades** - Check OLM operators for pending upgrades
- **check_helm_release_upgrades** - List Helm releases and versions
- **get_upgrade_prerequisites** - Validate upgrade readiness
- **trigger_openshift_upgrade** - Trigger OpenShift upgrade (with safety checks)
- **get_upgrade_status** - Monitor upgrade progress

## Slash Commands

| Command | Description |
|---------|-------------|
| `/k8s-health` | Check health of all clusters |
| `/k8s-issues` | Find pod and deployment issues |
| `/k8s-security` | Check for security misconfigurations |
| `/k8s-rbac` | Analyze RBAC permissions |
| `/k8s-analyze` | Comprehensive namespace analysis |
| `/k8s-audit-kubeconfig` | Audit and cleanup kubeconfig |
| `/k8s-ownership` | Manage ownership tracking with OPA Gatekeeper |
| `/k8s-upgrade-check` | Check for available upgrades |
| `/k8s-upgrade` | Interactive cluster upgrade workflow |

## Prerequisites

Install klaude binary:

```bash
# macOS (Homebrew)
brew install kubestellar/tap/klaude

# Or download from releases
# https://github.com/kubestellar/klaude/releases
```

## Example Usage

Once installed, you can ask Claude:

- "List all my Kubernetes clusters"
- "Show me pods that aren't running in the production namespace"
- "What permissions does the admin service account have?"
- "Check for available cluster upgrades"
- "What operators need updating?"
- "Upgrade my OpenShift cluster to 4.14.5"

Or use slash commands:
- `/k8s-upgrade-check` - Check all upgrade sources
- `/k8s-upgrade` - Start an interactive upgrade workflow

## Links

- [GitHub Repository](https://github.com/kubestellar/klaude)
- [KubeStellar](https://kubestellar.io)
