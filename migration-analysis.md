# Design Document Migration Analysis

This document provides a comprehensive analysis of design documents in the `nicolejms/design-notes` repository, comparing each against the actual codebase in the `nicolejms/radius` repository. Documents are categorized as **recommended for migration** (corresponding code exists in the radius repo) or **not recommended for migration** (no corresponding code, future/speculative features, or not code-related).

## Summary

| Category | Recommended | Not Recommended | Total |
|----------|-------------|-----------------|-------|
| Architecture | 13 | 2 | 15 |
| Recipe | 12 | 1 | 13 |
| Resources | 9 | 0 | 9 |
| CLI | 2 | 0 | 2 |
| UCP | 2 | 0 | 2 |
| Tools | 3 | 0 | 3 |
| Features | 6 | 7 | 13 |
| Guide | 1 | 0 | 1 |
| Specs | 2 | 0 | 2 |
| Templates | 3 | 0 | 3 |
| **Total** | **53** | **10** | **63** |

---

## Recommended for Migration

These design documents describe features, components, or architectural decisions that have corresponding implementations in the `nicolejms/radius` repository.

### Architecture

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `architecture/2023-06-arch-vnext.md` | Radius Service Architecture vNext | Overall architecture: `pkg/corerp/`, `pkg/ucp/`, `cmd/applications-rp/`, `cmd/ucpd/`, `cmd/controller/` |
| `architecture/2023-10-kubernetes-integration.md` | Kubernetes Integration | `pkg/kubernetes/`, `pkg/controller/`, `pkg/kubeutil/` |
| `architecture/2024-07-user-defined-types.md` | User-Defined Types | `pkg/dynamicrp/`, `cmd/dynamic-rp/`, `typespec/UCP/resourceproviders.tsp` |
| `architecture/2024-07-user-defned-types-schema-design.md` | User-Defined Types Schema Validation | `pkg/dynamicrp/`, `pkg/schema/` |
| `architecture/2024-08-resource-types-registration.md` | Resource Type Registration APIs | `typespec/UCP/resourceproviders.tsp`, `pkg/dynamicrp/api/` |
| `architecture/2024-08-applications-rp-component-threat-model.md` | Applications RP Threat Model | `pkg/corerp/`, `cmd/applications-rp/` |
| `architecture/2024-08-controller-component-threat-model.md` | Controller Component Threat Model | `pkg/controller/`, `cmd/controller/` |
| `architecture/2024-08-dashboard-component-threat-model.md` | Dashboard Component Threat Model | Radius Dashboard component (part of overall Radius security posture) |
| `architecture/2024-10-deploymenttemplate-controller.md` | DeploymentTemplate Controller | `pkg/controller/reconciler/deploymenttemplate_reconciler.go` |
| `architecture/2024-11-ucp-component-threat-model.md` | UCP Component Threat Model | `pkg/ucp/`, `cmd/ucpd/` |
| `architecture/2025-03-upgrade-design-doc.md` | Control Plane Upgrades | `pkg/upgrade/`, `cmd/pre-upgrade/` |
| `architecture/2025-04-aci-support.md` | ACI Integration | `pkg/corerp/renderers/aci/` |
| `architecture/2025-04-compute-extensibility.md` | Compute Platform Extensibility | `pkg/corerp/renderers/aci/`, `pkg/corerp/renderers/container/` |

### Recipe

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `recipe/2023-07-terraform-template-version.md` | Terraform Module Versions | `pkg/recipes/terraform/module.go` |
| `recipe/2023-08-garbage-collection.md` | Recipe Resource Garbage Collection | `pkg/recipes/engine/` |
| `recipe/2023-08-recipes-test-plan.md` | Recipes Test Plan | `test/testrecipes/`, `test/functional-portable/` |
| `recipe/2023-09-populate-terraform-resourcs-ids.md` | Populate Terraform Resource IDs | `pkg/recipes/terraform/` |
| `recipe/2023-11-validate-template-path.md` | Validate Template Paths | `pkg/recipes/terraform/module.go` |
| `recipe/2023-11-support-insecure-registries.md` | Support Insecure Registries | `pkg/recipes/` configuration handling |
| `recipe/2024-01-global-scope-secret-store.md` | Global Scope Secret Store | `pkg/corerp/frontend/controller/secretstores/` |
| `recipe/2024-01-support-private-terraform-repository.md` | Private Terraform Repository Support | `pkg/recipes/terraform/` |
| `recipe/2024-02-terraform-providers.md` | Multiple Terraform Providers | `pkg/recipes/terraform/config/providers/` |
| `recipe/2024-04-terraform-provider-secrets.md` | Terraform Provider Secrets | `pkg/recipes/terraform/config/` |
| `recipe/2024-06-private-bicep-registries.md` | Private Bicep Registries | `pkg/recipes/` |
| `recipe/2025-08-recipe-packs.md` | Recipe Packs | `pkg/corerp/frontend/controller/recipepacks/` |

### Resources

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `resources/2023-04-tls-termination.md` | TLS Termination | `typespec/Applications.Core/gateways.tsp`, `pkg/corerp/renderers/gateway/` |
| `resources/2023-07-fail-deployments.md` | Classify Deployment Failures | `pkg/corerp/backend/` |
| `resources/2023-10-app-graph.md` | Application Graph API | `pkg/corerp/frontend/controller/applications/` |
| `resources/2023-10-recipe-details.md` | Recipe Information in Resources | `pkg/corerp/datamodel/` |
| `resources/2023-10-simulated-environment.md` | Simulated Environment | `typespec/Applications.Core/environments.tsp` |
| `resources/2024-06-support-secretstores-env.md` | Secret Stores in Environment Variables | `typespec/Applications.Core/secretStores.tsp`, `pkg/corerp/frontend/controller/secretstores/` |
| `resources/2024-10-dapr-bindings.md` | Dapr Binding Implementation | `pkg/daprrp/` (Note: Dapr Bindings not yet in typespec; `pkg/daprrp/` handles Dapr resource types) |
| `resources/2025-01-gateway-timeouts.md` | Gateway Timeouts | `typespec/Applications.Core/gateways.tsp`, `pkg/corerp/renderers/gateway/` |
| `resources/2025-11-11-secrets-redactdata.md` | Redacting Sensitive Data | `pkg/crypto/encryption/` |

### CLI

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `cli/2024-04-azure-workload-identity.md` | Azure Workload Identity Support | `typespec/UCP/azure-credentials.tsp`, `pkg/ucp/credentials/azure.go` |
| `cli/2024-06-04-aws-irsa-support.md` | AWS IRSA Support | `typespec/UCP/aws-credentials.tsp`, `pkg/ucp/credentials/aws.go` |

### UCP

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `ucp/2024-03-planes-apis.md` | Planes APIs | `typespec/UCP/planes.tsp`, `typespec/UCP/aws-plane.tsp`, `typespec/UCP/azure-plane.tsp`, `typespec/UCP/radius-plane.tsp`, `pkg/ucp/frontend/` |
| `ucp/aws/handle-non-idempotent-resources/2023-09-handle-aws-non-idempotent-resources.md` | Handling Non-Idempotent AWS Resources | `pkg/ucp/aws/` |

### Tools

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `tools/2023-12-test-organization.md` | Organization of Functional Tests | `test/` directory structure, `test/functional-portable/` |
| `tools/2025-01-gitops-technical-design.md` | Radius Flux Controller Design | `pkg/controller/reconciler/flux_controller.go` |
| `tools/2025-03-workflow-changes.md` | GitHub Workflow Changes | `.github/` workflows |

### Features

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `features/2024-06-resource-extensibility-feature-spec.md` | Resource Extensibility | `pkg/dynamicrp/`, `typespec/UCP/resourceproviders.tsp` |
| `features/2024-06-gitops-feature-spec.md` | GitOps Integration | `pkg/controller/reconciler/flux_controller.go` |
| `features/2024-07-secretstore-feature-spec.md` | Secret Stores Extension | `typespec/Applications.Core/secretStores.tsp`, `pkg/corerp/frontend/controller/secretstores/` |
| `features/2025-01-serverless-feature-spec.md` | Serverless Container Platforms | `pkg/corerp/renderers/aci/` |
| `features/2025-02-user-defined-resource-type-feature-spec.md` | User-Defined Resource Types | `pkg/dynamicrp/`, `typespec/UCP/resourceproviders.tsp` |
| `features/2025-06-compute-extensibility-feature-spec.md` | Compute Platform Extensibility | `pkg/corerp/renderers/aci/`, `pkg/corerp/renderers/container/` |

### Guide

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `guide/api-design-guidelines.md` | Radius API Guidelines | `typespec/`, `pkg/armrpc/` |

### Specs

| Document | Title | Corresponding Code in `radius` |
|----------|-------|-------------------------------|
| `specs/001-lrt-current-release/` | Long-Running Tests Feature Spec | `test/` infrastructure |
| `specs/001-remove-bicep-types-submodule/` | Remove Bicep Types Submodule | Build system, `go.mod` |

### Templates

| Document | Title | Rationale |
|----------|-------|-----------|
| `template/YYYY-MM-design-template.md` | Design Document Template | Supports future design work in radius repo |
| `template/YYYY-MM-feature-spec-template.md` | Feature Specification Template | Supports future design work in radius repo |
| `template/YYYY-MM-threat-model-template.md` | Threat Model Template | Supports future design work in radius repo |

---

## Not Recommended for Migration

These design documents describe features that are not yet implemented, are speculative/future proposals, or represent process documentation without corresponding code.

| Document | Title | Reason |
|----------|-------|--------|
| `architecture/2024-05-radius-on-dapr.md` | Radius on Dapr | Proposes replacing internal service infrastructure with Dapr. No evidence this was implemented; the service architecture still uses its own patterns. |
| `architecture/2025-10-terraform-bicep-settings.md` | Terraform & Bicep Settings Lifecycle | Future feature for externalizing Terraform/Bicep recipe configuration into dedicated settings resources. No corresponding settings resource types exist in `typespec/`. |
| `recipe/2025-09-container.md` | Container Resource Recipe Migration | Proposes replacing the imperative Go renderer for containers with a Bicep recipe. Container still uses the Go renderer chain (`pkg/corerp/renderers/container/`). |
| `features/2024-11-authz-feature-spec.md` | Authorization Feature | Granular access control and permissions for multi-tenant environments. No authorization/RBAC code exists in the radius repo. |
| `features/2025-07-10-offline-install-feature-spec.md` | Offline Installation | Support for air-gapped environments. No specific offline installation code or mechanisms exist. |
| `features/2025-07-23-radius-configuration-ux.md` | Configuration UX | User experience design recommendations for control plane configuration. UX guidance document without direct code implementation. |
| `features/2025-07-radius-resource-types-contribution.md` | Contributing Resource Types | Community contribution process and pathways document. Not a code feature specification. |
| `features/2025-08-14-terraform-bicep-settings.md` | Terraform & Bicep Settings | Feature spec for externalizing settings (same future feature as architecture doc above). No corresponding settings resources in `typespec/`. |
| `features/2025-08-29-container-resource-type.md` | Container Resource Type | Redesigned container resource type as part of compute extensibility. Represents future schema redesign, not current implementation. |
| `features/2025-09-02-routes-resource-type.md` | Routes Resource Type | New routes resource type replacing legacy gateways. No `routes.tsp` or routes implementation exists; `gateways.tsp` remains the current implementation. |

---

## Migration Notes

### Suggested Target Location

Design documents should be migrated to the `docs/design-notes/` directory in the radius repository, preserving the current directory structure:

```
radius/docs/design-notes/
├── architecture/
├── cli/
├── features/
├── guide/
├── recipe/
├── resources/
├── specs/
├── template/
├── tools/
└── ucp/
```

### Documents Already in Radius

The radius repository already contains architecture documentation in `docs/architecture/`:
- `docs/architecture/deployment-engine.md`
- `docs/architecture/state-persistence.md`

Migrated design documents should be placed in a separate `docs/design-notes/` directory to avoid conflicts.

### Exclusions

The following items from the design-notes repository should **not** be migrated as they are repository-specific tooling:
- `.specify/` - Spec Kit configuration specific to the design-notes repo
- `.github/agents/` and `.github/prompts/` - Spec Kit agents/prompts for the design-notes repo
- `.github/config/` - Spell-checking dictionary (may be merged into the radius repo's existing config)
- `.vscode/` - Workspace settings
- `design-notes.code-workspace` - VS Code workspace file
