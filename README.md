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

```
/plugin install kubestellar-ops
/plugin install kubestellar-deploy
```

Or go to `/plugin` → **Discover** tab → Install **kubestellar-ops** and/or **kubestellar-deploy**.

### Step 3: Restart Claude Code

After installing (or updating) plugins, **you must restart Claude Code** for the new MCP servers to be loaded. Simply exit and relaunch the CLI:

```bash
# Exit Claude Code (Ctrl+C or type /exit), then restart it
claude
```

### Step 4: Verify

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

#### MCP Tools Reference

<details>
<summary><strong>Cluster Management</strong> (4 tools)</summary>

##### `list_clusters`
List all discovered Kubernetes clusters from kubeconfig and KubeStellar.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `source` | string | No | Discovery source: `all`, `kubeconfig`, or `kubestellar` |

##### `get_cluster_health`
Check the health status of a Kubernetes cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

##### `get_nodes`
List nodes in a cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

##### `audit_kubeconfig`
Audit all clusters in kubeconfig: check connectivity, identify stale/inaccessible clusters, and recommend cleanup.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `timeout_seconds` | integer | No | Connection timeout in seconds per cluster (default 5) |

</details>

<details>
<summary><strong>Workload Tools</strong> (6 tools)</summary>

##### `get_pods`
List pods in a cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |
| `label_selector` | string | No | Label selector to filter pods (e.g., `app=nginx`) |

##### `get_deployments`
List deployments in a cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `get_services`
List services in a cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `get_events`
Get recent events from a cluster, useful for troubleshooting.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |
| `limit` | integer | No | Maximum number of events to return (default 50) |

##### `describe_pod`
Get detailed information about a specific pod.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace of the pod |
| `name` | string | **Yes** | Name of the pod |

##### `get_pod_logs`
Get logs from a pod.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace of the pod |
| `name` | string | **Yes** | Name of the pod |
| `container` | string | No | Container name (required if pod has multiple containers) |
| `tail_lines` | integer | No | Number of lines from the end to return (default 100) |

</details>

<details>
<summary><strong>RBAC Analysis</strong> (7 tools)</summary>

##### `get_roles`
List Roles in a namespace.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `get_cluster_roles`
List ClusterRoles in a cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `include_system` | string | No | Include system ClusterRoles (`true`/`false`, default `false`) |

##### `get_role_bindings`
List RoleBindings in a namespace.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `get_cluster_role_bindings`
List ClusterRoleBindings in a cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `include_system` | string | No | Include system ClusterRoleBindings (`true`/`false`, default `false`) |

##### `can_i`
Check if a subject can perform an action on a resource (similar to `kubectl auth can-i`).
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `verb` | string | **Yes** | The action verb (`get`, `list`, `create`, `update`, `delete`, `watch`, etc.) |
| `resource` | string | **Yes** | The resource type (`pods`, `deployments`, `secrets`, etc.) |
| `namespace` | string | No | Namespace for the check (empty for cluster-scoped) |
| `subresource` | string | No | Subresource (e.g., `logs`, `status`) |
| `name` | string | No | Specific resource name to check |

##### `analyze_subject_permissions`
Analyze all RBAC permissions for a specific subject (user, group, or service account).
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `subject_kind` | string | **Yes** | Kind of subject: `User`, `Group`, or `ServiceAccount` |
| `subject_name` | string | **Yes** | Name of the subject |
| `namespace` | string | No | Namespace for ServiceAccount subjects |

##### `describe_role`
Get detailed information about a Role or ClusterRole including all rules.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `name` | string | **Yes** | Name of the Role or ClusterRole |
| `namespace` | string | No | Namespace for Role (omit for ClusterRole) |

</details>

<details>
<summary><strong>Diagnostic Tools</strong> (7 tools)</summary>

##### `find_pod_issues`
Find pods with issues like CrashLoopBackOff, ImagePullBackOff, Pending, OOMKilled, or restarts.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |
| `include_completed` | string | No | Include completed/succeeded pods (`true`/`false`, default `false`) |

##### `find_deployment_issues`
Find deployments with issues like unavailable replicas, stuck rollouts, or misconfigurations.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `check_resource_limits`
Find pods/containers without CPU or memory limits/requests configured.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `check_security_issues`
Find security misconfigurations: privileged containers, running as root, host network/PID, missing security context.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `analyze_namespace`
Comprehensive namespace analysis: resource quotas, limit ranges, pod count, issues summary.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | **Yes** | Namespace to analyze |

##### `get_warning_events`
Get only Warning events, filtered by namespace or resource.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |
| `involved_object` | string | No | Filter by involved object name |
| `limit` | integer | No | Maximum number of events (default 50) |

##### `find_resource_owners`
Find who owns/manages resources by checking managedFields, ownership labels, and annotations.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | **Yes** | Namespace to check |
| `resource_type` | string | No | Resource type: `pods`, `deployments`, `services`, `all` (default: `all`) |

</details>

<details>
<summary><strong>OPA Gatekeeper Policy Tools</strong> (6 tools)</summary>

##### `check_gatekeeper`
Check if OPA Gatekeeper is installed and running in the cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

##### `get_ownership_policy_status`
Get the status of the ownership labels policy including violation count.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

##### `list_ownership_violations`
List resources that violate the ownership labels policy (missing owner/team labels).
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Filter violations by namespace |
| `limit` | integer | No | Maximum number of violations to return (default 50) |

##### `install_ownership_policy`
Install the ownership labels policy (ConstraintTemplate and Constraint) for OPA Gatekeeper.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `labels` | array | No | Required labels (default: `["owner", "team"]`) |
| `target_namespaces` | array | No | Namespaces to enforce (empty means all non-system namespaces) |
| `exclude_namespaces` | array | No | Namespaces to exclude (default: `kube-*`, `openshift-*`, `gatekeeper-system`) |
| `mode` | string | No | Enforcement mode: `dryrun`, `warn`, or `enforce` (default: `dryrun`) |

##### `set_ownership_policy_mode`
Change the enforcement mode of the ownership labels policy.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `mode` | string | **Yes** | Enforcement mode: `dryrun`, `warn`, or `enforce` |

##### `uninstall_ownership_policy`
Remove the ownership labels policy from the cluster.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

</details>

<details>
<summary><strong>Upgrade Tools</strong> (7 tools)</summary>

##### `detect_cluster_type`
Detect the Kubernetes distribution type (OpenShift, EKS, GKE, AKS, kubeadm, k3s, kind, etc.).
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

##### `get_cluster_version_info`
Get current Kubernetes/OpenShift version and check for available upgrades.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

##### `check_olm_operator_upgrades`
Check OLM-managed operators for available upgrades (requires OLM installed).
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `check_helm_release_upgrades`
Check Helm releases for available chart version upgrades.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `get_upgrade_prerequisites`
Check upgrade prerequisites: node health, pod issues, ClusterOperators (OpenShift), MachineConfigPools.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

##### `trigger_openshift_upgrade`
Trigger an OpenShift cluster upgrade to a specific version. **Requires explicit confirmation.**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |
| `target_version` | string | **Yes** | Target OpenShift version (e.g., `4.14.5`) |
| `confirm` | string | **Yes** | Must be `yes-upgrade-now` to proceed |

##### `get_upgrade_status`
Get the current upgrade status for a cluster (progress, ClusterOperators, MachineConfigPools).
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Cluster name (uses current context if not specified) |

</details>

<details>
<summary><strong>GitOps</strong> (1 tool)</summary>

##### `detect_drift`
Detect configuration drift between Git repository manifests and cluster state.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `repo_url` | string | **Yes** | Git repository URL (e.g., `https://github.com/org/manifests`) |
| `path` | string | No | Path within repository to YAML manifests (e.g., `production/`) |
| `branch` | string | No | Git branch to use (default: `main`) |
| `cluster` | string | No | Target cluster (uses current context if not specified) |
| `namespace` | string | No | Override namespace for all resources |

</details>

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

#### MCP Tools Reference

<details>
<summary><strong>App Management</strong> (6 tools)</summary>

##### `get_app_instances`
Find all instances of an app across all clusters. Returns where the app is running, replica counts, and health status.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `app` | string | **Yes** | App name (matches label `app=<name>` or name contains `<name>`) |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `get_app_status`
Get unified status of an app across all clusters. Shows health (healthy/degraded/failed), replica counts, and any issues.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `app` | string | **Yes** | App name |
| `namespace` | string | No | Namespace (all namespaces if not specified) |

##### `get_app_logs`
Get aggregated logs from an app across all clusters. Logs are labeled with cluster name for easy identification.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `app` | string | **Yes** | App name |
| `namespace` | string | No | Namespace (all namespaces if not specified) |
| `tail` | integer | No | Number of lines from end (default 100) |
| `since` | string | No | Only return logs newer than duration (e.g., `1h`, `30m`) |

##### `deploy_app`
Deploy an app to clusters. Can specify clusters explicitly or let kubestellar find matching clusters based on requirements.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `manifest` | string | **Yes** | Kubernetes manifest (YAML) |
| `clusters` | array | No | Target clusters (all matching clusters if not specified) |
| `gpu_type` | string | No | Deploy to clusters with this GPU type |
| `min_gpu` | integer | No | Deploy to clusters with at least this many GPUs |
| `dry_run` | boolean | No | Preview changes without applying |

##### `scale_app`
Scale an app across clusters. Can target specific clusters or all clusters where app runs.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `app` | string | **Yes** | App name |
| `replicas` | integer | **Yes** | Target replica count |
| `namespace` | string | No | Namespace |
| `clusters` | array | No | Target clusters (all clusters where app runs if not specified) |

##### `patch_app`
Apply a patch to an app across clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `app` | string | **Yes** | App name |
| `patch` | string | **Yes** | JSON or strategic merge patch |
| `namespace` | string | No | Namespace |
| `patch_type` | string | No | Patch type: `strategic`, `merge`, or `json` (default: `strategic`) |
| `clusters` | array | No | Target clusters |

</details>

<details>
<summary><strong>Cluster Capabilities</strong> (2 tools)</summary>

##### `list_cluster_capabilities`
List what each cluster can run: GPU availability, CPU/memory capacity, node labels.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cluster` | string | No | Specific cluster (all clusters if not specified) |

##### `find_clusters_for_workload`
Find clusters that can run a workload with specific requirements (GPU, memory, CPU, labels).
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `gpu_type` | string | No | GPU type required (e.g., `nvidia.com/gpu`) |
| `min_gpu` | integer | No | Minimum number of GPUs required |
| `min_memory` | string | No | Minimum memory required (e.g., `16Gi`) |
| `min_cpu` | string | No | Minimum CPU required (e.g., `4`) |
| `labels` | object | No | Required node labels |

</details>

<details>
<summary><strong>GitOps</strong> (4 tools)</summary>

##### `detect_drift`
Detect drift between git manifests and cluster state. Shows which resources differ between git and what's deployed.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `repo` | string | **Yes** | Git repository URL (e.g., `https://github.com/org/manifests`) |
| `path` | string | No | Path within repo to manifests (e.g., `production/`) |
| `branch` | string | No | Git branch (default: `main`) |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `sync_from_git`
Sync manifests from a git repository to clusters. Applies all manifests found in the specified path.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `repo` | string | **Yes** | Git repository URL |
| `path` | string | No | Path within repo to manifests |
| `branch` | string | No | Git branch (default: `main`) |
| `clusters` | array | No | Target clusters (all clusters if not specified) |
| `dry_run` | boolean | No | Preview changes without applying |
| `namespace` | string | No | Override namespace for all resources |

##### `reconcile`
Bring clusters back in sync with git. Same as sync_from_git but always applies changes.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `repo` | string | **Yes** | Git repository URL |
| `path` | string | No | Path within repo to manifests |
| `branch` | string | No | Git branch (default: `main`) |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `preview_changes`
Preview what would change if manifests were synced from git. Dry-run mode.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `repo` | string | **Yes** | Git repository URL |
| `path` | string | No | Path within repo to manifests |
| `branch` | string | No | Git branch (default: `main`) |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

</details>

<details>
<summary><strong>Helm</strong> (4 tools)</summary>

##### `helm_install`
Install or upgrade a Helm chart to clusters. Supports values overrides and targeting specific clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `release_name` | string | **Yes** | Name for the Helm release |
| `chart` | string | **Yes** | Chart name or path (e.g., `nginx`, `./mychart`, `oci://registry/chart`) |
| `namespace` | string | No | Target namespace (default: `default`) |
| `values` | object | No | Values to set (key-value pairs for `--set`) |
| `values_yaml` | string | No | Values in YAML format (equivalent to `-f values.yaml`) |
| `version` | string | No | Chart version to install |
| `repo` | string | No | Chart repository URL |
| `wait` | boolean | No | Wait for resources to be ready |
| `timeout` | string | No | Timeout for wait (e.g., `5m`, `300s`) |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `helm_uninstall`
Uninstall a Helm release from clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `release_name` | string | **Yes** | Name of the Helm release to uninstall |
| `namespace` | string | No | Namespace of the release (default: `default`) |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (clusters where release exists if not specified) |

##### `helm_list`
List Helm releases across clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `namespace` | string | No | Filter by namespace |
| `all_namespaces` | boolean | No | List releases in all namespaces |
| `filter` | string | No | Filter releases by name regex |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `helm_rollback`
Rollback a Helm release to a previous revision.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `release_name` | string | **Yes** | Name of the Helm release |
| `namespace` | string | No | Namespace of the release (default: `default`) |
| `revision` | integer | No | Revision to rollback to (previous if not specified) |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (clusters where release exists if not specified) |

</details>

<details>
<summary><strong>Resource Management</strong> (7 tools)</summary>

##### `kubectl_apply`
Apply any Kubernetes manifest to clusters. Supports all resource types using dynamic client.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `manifest` | string | **Yes** | Kubernetes manifest (YAML or JSON) |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `delete_resource`
Delete a Kubernetes resource from clusters. Supports all common resource types.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `kind` | string | **Yes** | Resource kind (e.g., `Deployment`, `Service`, `Pod`, `ConfigMap`, `Secret`) |
| `name` | string | **Yes** | Resource name |
| `namespace` | string | No | Namespace (default: `default`, ignored for cluster-scoped resources) |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `add_labels`
Add labels to a Kubernetes resource across clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `kind` | string | **Yes** | Resource kind (e.g., `Deployment`, `Service`, `Pod`, `Node`) |
| `name` | string | **Yes** | Resource name |
| `labels` | object | **Yes** | Labels to add (key-value pairs) |
| `namespace` | string | No | Namespace (default: `default`, ignored for cluster-scoped) |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `remove_labels`
Remove labels from a Kubernetes resource across clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `kind` | string | **Yes** | Resource kind (e.g., `Deployment`, `Service`, `Pod`, `Node`) |
| `name` | string | **Yes** | Resource name |
| `labels` | array | **Yes** | Label keys to remove |
| `namespace` | string | No | Namespace (default: `default`, ignored for cluster-scoped) |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `kustomize_build`
Build kustomize output from a directory containing kustomization.yaml. Returns the rendered manifests.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | string | **Yes** | Path to directory containing kustomization.yaml |

##### `kustomize_apply`
Build and apply kustomize output to clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | string | **Yes** | Path to directory containing kustomization.yaml |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

##### `kustomize_delete`
Build kustomize output and delete those resources from clusters.
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | string | **Yes** | Path to directory containing kustomization.yaml |
| `dry_run` | boolean | No | Preview changes without applying |
| `clusters` | array | No | Target clusters (all clusters if not specified) |

</details>

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
