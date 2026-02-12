# KubeStellar Claude Plugins

Official Claude Code plugin marketplace for [KubeStellar](https://kubestellar.io) - multi-cluster Kubernetes management tools.

## Prerequisites

Install the CLI tools via Homebrew **before** adding the plugins:

```bash
brew tap kubestellar/tap
brew install kubestellar-ops kubestellar-deploy
```

Or download binaries from [GitHub Releases](https://github.com/kubestellar/kubestellar-mcp/releases).

## Installation

### Step 1: Add the KubeStellar Marketplace

In Claude Code, run:

```
/plugin marketplace add kubestellar/claude-plugins
```

### Step 2: Install the Plugins

Go to `/plugin` → **Discover** tab → Install **kubestellar-ops** and/or **kubestellar-deploy**.

### Step 3: Verify

Run `/mcp` in Claude Code - you should see:

```
plugin:kubestellar-ops:kubestellar-ops · ✓ connected
plugin:kubestellar-deploy:kubestellar-deploy · ✓ connected
```

### Allow Tools Without Prompts

Add to `~/.claude/settings.json`:

```json
{
  "permissions": {
    "allow": [
      "mcp__plugin_kubestellar-ops_kubestellar-ops__*",
      "mcp__plugin_kubestellar-deploy_kubestellar-deploy__*"
    ]
  }
}
```

Or run in Claude Code:

```
/allowed-tools add mcp__plugin_kubestellar-ops_kubestellar-ops__*
/allowed-tools add mcp__plugin_kubestellar-deploy_kubestellar-deploy__*
```

## Updating

### Update Plugins

To update the plugins to the latest version available in the marketplace:

```
/plugin update kubestellar-ops
/plugin update kubestellar-deploy
```

Or update all installed plugins at once:

```
/plugin update --all
```

### Update CLI Tools

The plugins rely on the `kubestellar-ops` and `kubestellar-deploy` CLI tools installed via Homebrew. To upgrade them:

```bash
brew update
brew upgrade kubestellar-ops kubestellar-deploy
```

### Check Installed Versions

To see what versions you currently have installed:

```
/plugin list
```

For CLI tool versions:

```bash
kubestellar-ops --version
kubestellar-deploy --version
```

## Uninstalling

To remove a plugin from Claude Code:

```
/plugin uninstall kubestellar-ops
/plugin uninstall kubestellar-deploy
```

To remove the marketplace:

```
/plugin marketplace remove kubestellar/claude-plugins
```

To remove the CLI tools:

```bash
brew uninstall kubestellar-ops kubestellar-deploy
brew untap kubestellar/tap
```

---

## Plugins

### kubestellar-ops

Multi-cluster Kubernetes diagnostics, RBAC analysis, and security checks.

#### Example Usage

- "List my Kubernetes clusters"
- "Find pods with issues across all clusters"
- "Check for security misconfigurations"
- "What permissions does the admin service account have?"
- "Show me warning events in kube-system"

#### Skills

| Skill | Description |
|-------|-------------|
| `/k8s-health` | Check health of all Kubernetes clusters |
| `/k8s-issues` | Find issues across clusters (pods, deployments, events) |
| `/k8s-analyze` | Comprehensive namespace analysis |
| `/k8s-security` | Security audit (privileged, root, host access) |
| `/k8s-rbac` | Analyze RBAC permissions for a subject |
| `/k8s-audit-kubeconfig` | Audit kubeconfig clusters and recommend cleanup |
| `/k8s-ownership` | Set up and manage resource ownership tracking with OPA Gatekeeper |
| `/k8s-upgrade-check` | Check for available upgrades |
| `/k8s-upgrade` | Upgrade cluster (master and nodes) |

#### MCP Tools

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

**Upgrade Tools**
| Tool | Description |
|------|-------------|
| `detect_cluster_type` | Detect Kubernetes distribution type |
| `get_cluster_version_info` | Get version and available upgrades |
| `check_olm_operator_upgrades` | Check OLM operators for upgrades |
| `check_helm_release_upgrades` | List Helm releases and versions |
| `get_upgrade_prerequisites` | Validate upgrade readiness |
| `trigger_openshift_upgrade` | Initiate OpenShift upgrade |
| `get_upgrade_status` | Monitor upgrade progress |

---

### kubestellar-deploy

App-centric multi-cluster deployment and operations with GitOps support.

#### Example Usage

- "Where is nginx running?"
- "Get logs from my api service"
- "Deploy my ML model to clusters with GPUs"
- "Are my clusters in sync with git?"
- "Scale my app to 5 replicas across all clusters"

#### Skills

| Skill | Description |
|-------|-------------|
| `/app-status` | Show the status of an app across all clusters |
| `/app-logs` | Get aggregated logs from an app across all clusters |
| `/deploy` | Deploy an app to multiple clusters with smart placement |
| `/gitops-drift` | Detect drift between git manifests and cluster state |
| `/gitops-sync` | Sync manifests from a git repository to clusters |

#### MCP Tools

**App Management**
| Tool | Description |
|------|-------------|
| `get_app_instances` | Find all instances of an app across clusters |
| `get_app_status` | Get unified app status across clusters |
| `get_app_logs` | Get aggregated logs from an app |
| `deploy_app` | Deploy an app to clusters |
| `scale_app` | Scale an app across clusters |
| `patch_app` | Apply a patch to an app across clusters |

**Cluster Capabilities**
| Tool | Description |
|------|-------------|
| `list_cluster_capabilities` | List what each cluster can run |
| `find_clusters_for_workload` | Find clusters matching requirements |

**GitOps**
| Tool | Description |
|------|-------------|
| `detect_drift` | Detect configuration drift between git and clusters |
| `sync_from_git` | Sync manifests from git to clusters |
| `reconcile` | Force sync clusters with git |
| `preview_changes` | Preview what would change |

**Helm**
| Tool | Description |
|------|-------------|
| `helm_install` | Install or upgrade a Helm chart |
| `helm_uninstall` | Uninstall a Helm release |
| `helm_list` | List Helm releases |
| `helm_rollback` | Rollback a Helm release |

**Resource Management**
| Tool | Description |
|------|-------------|
| `kubectl_apply` | Apply any Kubernetes manifest |
| `delete_resource` | Delete a Kubernetes resource |
| `add_labels` | Add labels to a resource |
| `remove_labels` | Remove labels from a resource |
| `kustomize_build` | Build kustomize output |
| `kustomize_apply` | Build and apply kustomize output |
| `kustomize_delete` | Build and delete kustomize resources |

---

## Natural Language Usage

Once installed, ask questions like:
- "List my Kubernetes clusters"
- "Find pods with issues in the production namespace"
- "Check for security misconfigurations in my cluster"
- "What permissions does the admin service account have?"
- "Show me warning events in kube-system"
- "Audit my kubeconfig and show stale clusters"
- "What's the status of nginx across all clusters?"
- "Deploy this manifest to clusters with GPUs"
- "Check for drift from my git repo"
- "Install nginx-ingress with Helm across all clusters"
- "Apply kustomize overlay to production"

## About KubeStellar

KubeStellar is a flexible solution for multi-cluster Kubernetes configuration management. Learn more at [kubestellar.io](https://kubestellar.io).

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](https://github.com/kubestellar/kubestellar/blob/main/CONTRIBUTING.md).

## License

Apache License 2.0 - see [LICENSE](./LICENSE) for details.
