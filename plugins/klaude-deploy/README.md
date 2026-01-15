# klaude-deploy

App-centric multi-cluster deployment and operations for Kubernetes.

## Vision: Single-Cluster UX for Multi-Cluster Reality

Work with your **apps**, not your **clusters**. klaude-deploy automatically discovers where your apps are running and aggregates results from all clusters.

```
Traditional Multi-Cluster UX (cluster-centric):
  kubectl --context=prod-east get pods
  kubectl --context=prod-west get pods
  kubectl --context=staging get pods

klaude-deploy UX (app-centric):
  "Where is nginx running?"
  "Get logs from my api service"
  "Deploy my ML model to GPU clusters"
```

## Installation

```bash
# Install via Homebrew
brew tap kubestellar/tap
brew install klaude-deploy

# Or download from releases
# https://github.com/kubestellar/klaude/releases
```

## Features

### App Discovery & Status
- **get_app_instances** - Find all instances of an app across clusters
- **get_app_status** - Unified health view (healthy/degraded/failed)
- **get_app_logs** - Aggregated logs with cluster labels

### Smart Deployment
- **deploy_app** - Deploy to clusters matching criteria (GPU, memory, labels)
- **scale_app** - Scale across all clusters where app runs
- **patch_app** - Apply patches everywhere at once

### Cluster Resources
- **list_cluster_capabilities** - GPU, CPU, memory per cluster
- **find_clusters_for_workload** - Find clusters that can run a workload

### GitOps
- **detect_drift** - Find clusters that diverged from git
- **sync_from_git** - Apply manifests from git repository
- **reconcile** - Bring clusters back in sync
- **preview_changes** - Dry-run to see what would change

## Slash Commands

| Command | Description |
|---------|-------------|
| `/app-status` | Show status of an app across all clusters |
| `/app-logs` | Get aggregated logs from an app |
| `/deploy` | Deploy or update an app |
| `/gitops-sync` | Sync clusters from git |
| `/gitops-drift` | Check for drift from git |

## Example Workflows

### "Where is my app running?"
```
User: Where is nginx running?
→ nginx is running on 3 clusters:
  - prod-east: 3 replicas, healthy
  - prod-west: 3 replicas, healthy
  - staging: 1 replica, healthy
```

### "Deploy to GPU clusters"
```
User: Deploy my ML model to clusters with GPUs
→ Found 2 clusters with nvidia.com/gpu
→ Deployed to gpu-cluster-1, gpu-cluster-2
→ All healthy
```

### "Get logs"
```
User: Get logs from nginx
→ [prod-east/nginx-abc] GET /api/health 200
  [prod-west/nginx-xyz] GET /api/health 200
  [prod-east/nginx-abc] POST /api/data 201
```

### "Check drift"
```
User: Are my clusters in sync with git?
→ Drift detected:
  - prod-west: ConfigMap/app-config differs
  - staging: Deployment/api has extra replicas
```

## Allow Tools Without Prompts

To avoid permission prompts for each tool call:

```
/allowed-tools add mcp__plugin_klaude-deploy_klaude-deploy__*
```

Or add to `~/.claude/settings.json`:
```json
{
  "permissions": {
    "allow": [
      "mcp__plugin_klaude-deploy_klaude-deploy__*"
    ]
  }
}
```

## Related

- **klaude-ops**: Multi-cluster diagnostics, RBAC analysis, security checks
- **kubernetes-mcp-server**: Core Kubernetes operations (pods, deployments, helm)

## License

Apache-2.0
