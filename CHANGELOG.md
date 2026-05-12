# Changelog

## [2.0.0] - 2026-05-12

### ⚠️ Breaking Changes

- Upgraded `hashicorp/azurerm` provider from `~> 3.116` to `~> 4.20`.
- Minimum Terraform CLI version raised from `>= 1.9` to `>= 1.10`.

### Behavior Notes

- The `azurerm_cognitive_account` resources (`cog`,
  `cog_cmk` via `azurerm_cognitive_account_customer_managed_key`)
  retain their `identity { type, identity_ids }` blocks unchanged —
  azurerm 4.x did not alter that block's schema. CMK input
  `cmk_user_assigned_identity_id` continues to feed
  `identity_ids = [var.cmk_user_assigned_identity_id]`.
- This overlay does not yet declare an `azurerm_synapse_workspace`
  resource. The 4.x rename matrix for Synapse Workspace
  (`managed_virtual_network_enabled`, `data_exfiltration_protection_enabled`,
  identity block) will be applied when the resource block is added in
  a subsequent feature PR.

### Migration Notes for Consumers

- Bump your root `azurerm` provider constraint to `~> 4.20`.
- Ensure Terraform CLI `>= 1.10`.
- Set `ARM_SUBSCRIPTION_ID` env var or `subscription_id` in your
  `provider "azurerm"` block — azurerm 4.x requires it.
- Module public input/output surface is unchanged.

### Added

- `azapi ~> 2.0` provider declaration in `versions.tf`.
- New `examples/basic/versions.tf` declaring the full fleet provider
  set (azurerm, azapi, popsrox, random). Previously the example
  embedded `provider "azurerm" {}` in `main.tf` with no pinned
  provider versions, leaving the example floating on whatever
  azurerm the consumer happened to have cached.

### Internal

- Standardized `versions.tf` format and bumped `required_version`
  to `>= 1.10` everywhere.

### Cross-module dependency

This module sources two sibling overlays from GitHub
(`tf-az-overlays-azregionslookup`, `tf-az-overlays-resourcegroup`)
which are still pinned to `azurerm ~> 3.116`. Production consumers
must wait for those overlays' Phase 1 PRs to merge before this
`2.0.0` can be cleanly initialized. Local validation was performed by
patching the cached `versions.tf` of those submodules during
`terraform init -get=false`.

# v1.0.0 - <date>

Added
- Add Something you added
