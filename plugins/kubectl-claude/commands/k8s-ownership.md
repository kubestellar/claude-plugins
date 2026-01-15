---
allowed-tools: mcp__plugin_kubectl-claude_kubectl-claude__*
description: Set up and manage resource ownership tracking with OPA Gatekeeper
---

## Your task

Help the user set up and manage resource ownership tracking using OPA Gatekeeper policies.

### Workflow

1. **Check Gatekeeper Status**
   - Use `check_gatekeeper` to verify OPA Gatekeeper is installed
   - If not installed, provide installation instructions

2. **Check/Install Ownership Policy**
   - Use `get_ownership_policy_status` to see if the ownership policy exists
   - If not installed, ask the user if they want to install it using `install_ownership_policy`
   - Default to `dryrun` mode for safety

3. **Show Violations**
   - Use `list_ownership_violations` to show resources missing ownership labels
   - Group by namespace and highlight the most problematic areas

4. **Recommend Next Steps**
   - If in dryrun mode with many violations, help users fix them before enforcing
   - Suggest switching to `warn` mode first, then `enforce`

### Available Tools

| Tool | Purpose |
|------|---------|
| `check_gatekeeper` | Check if Gatekeeper is installed |
| `get_ownership_policy_status` | Get current policy configuration |
| `list_ownership_violations` | List resources missing labels |
| `install_ownership_policy` | Install the policy (dryrun/warn/enforce) |
| `set_ownership_policy_mode` | Change enforcement mode |
| `uninstall_ownership_policy` | Remove the policy |
| `find_resource_owners` | Check who owns existing resources |

### Key Parameters

**install_ownership_policy:**
- `labels`: Required labels (default: ["owner", "team"])
- `mode`: dryrun (default), warn, or enforce
- `exclude_namespaces`: Namespaces to skip (auto-excludes system namespaces)

### Example Outputs

**Policy not installed:**
```
Gatekeeper is installed and healthy.
Ownership policy is not configured.

Would you like to install it? I recommend starting with dryrun mode
to see which resources would be affected before enforcing.
```

**Showing violations:**
```
Found 47 resources missing ownership labels:

By Namespace:
- default: 12 violations
- app-prod: 23 violations
- app-staging: 12 violations

Top violations:
| Namespace | Kind | Name | Missing |
|-----------|------|------|---------|
| app-prod | Deployment | api-server | owner, team |
...
```

### Safety Notes

- Always start with `dryrun` mode
- Show violation count before suggesting `enforce` mode
- Warn users that `enforce` mode will block deployments
