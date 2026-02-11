---
name: k8s-upgrade-check
description: Check for available upgrades
allowed-tools: mcp__plugin_kubestellar-ops_kubestellar-ops__*
---

## Your task

Use the kubestellar-ops MCP tools to check for available upgrades across Kubernetes clusters, including cluster version, OLM operators, and Helm releases.

### Workflow

1. **Discover Clusters**
   - Use `list_clusters` to get all available clusters
   - Ask the user which cluster(s) to check, or check all if they don't specify

2. **For each cluster:**

   a. **Detect Cluster Type**
      - Use `detect_cluster_type` to identify the distribution (OpenShift, EKS, GKE, AKS, kubeadm, etc.)
      - This determines what upgrade mechanisms are available

   b. **Check Cluster Version**
      - Use `get_cluster_version_info` to get current version and available upgrades
      - For OpenShift: Show available upgrade paths from ClusterVersion
      - For managed clusters: Show current version and guide to cloud console
      - For kubeadm: Show current version and upgrade guidance

   c. **Check OLM Operators** (if applicable)
      - Use `check_olm_operator_upgrades` to find operators with pending upgrades
      - Show current vs available versions
      - Note which operators have auto-update enabled vs manual

   d. **Check Helm Releases**
      - Use `check_helm_release_upgrades` to list Helm releases and their versions
      - Note: Cannot check for newer chart versions without helm CLI configured

3. **Generate Summary Report**

   Structure the output as:

   ```
   # Upgrade Check Report

   ## Cluster: <name>
   Type: <OpenShift 4.x | EKS | GKE | AKS | kubeadm | k3s | kind>
   Current Version: <version>

   ### Cluster Upgrade
   [Available upgrades or guidance based on cluster type]

   ### OLM Operators (if installed)
   | Operator | Current | Channel | Auto-Update | Status |
   |----------|---------|---------|-------------|--------|

   ### Helm Releases
   | Release | Namespace | Chart | Version |
   |---------|-----------|-------|---------|
   ```

### Available Tools

| Tool | Purpose |
|------|---------|
| `list_clusters` | Discover available clusters |
| `detect_cluster_type` | Identify cluster distribution |
| `get_cluster_version_info` | Get version and upgrade paths |
| `check_olm_operator_upgrades` | Check OLM operators for upgrades |
| `check_helm_release_upgrades` | List Helm releases and versions |

Do not use any other tools besides the kubestellar-ops MCP tools.
