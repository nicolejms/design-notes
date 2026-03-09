# Design Document Migration Analysis

This document provides a comprehensive analysis of design documents in the `nicolejms/design-notes` repository, comparing each against the actual codebase in the `nicolejms/radius` repository. Documents are categorized as **recommended for migration** (corresponding code exists in the radius repo) or **not recommended for migration** (no corresponding code, future/speculative features, or not code-related).

## Summary

Documents are reorganized into a new directory structure based on the functional area of the Radius system they relate to, rather than preserving the original design-notes repository layout. The "Source" column in each table shows where the document currently lives in design-notes.

| Target Directory | Recommended | Not Recommended | Total |
|------------------|-------------|-----------------|-------|
| `architecture/` | 3 | 1 | 4 |
| `security/` | 4 | 1 | 5 |
| `recipes/` | 10 | 5 | 15 |
| `resource-types/` | 1 | 9 | 10 |
| `extensibility/` | 5 | 5 | 10 |
| `control-plane/` | 4 | 1 | 5 |
| `deployment/` | 3 | 0 | 3 |
| `engineering/` | 5 | 3 | 8 |
| `templates/` | 3 | 0 | 3 |
| **Total** | **38** | **25** | **63** |

---

## Recommended for Migration

These design documents describe features, components, or architectural decisions that have corresponding implementations in the `nicolejms/radius` repository.

### architecture/ — System Architecture and Core Design

High-level system architecture, Kubernetes integration, and control plane upgrades.

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `architecture/2023-06-arch-vnext.md` | Radius Service Architecture vNext | `pkg/corerp/`, `pkg/ucp/`, `cmd/applications-rp/`, `cmd/ucpd/`, `cmd/controller/` |
| `architecture/2023-10-kubernetes-integration.md` | Kubernetes Integration | `pkg/kubernetes/`, `pkg/controller/`, `pkg/kubeutil/` |
| `architecture/2025-03-upgrade-design-doc.md` | Control Plane Upgrades | `pkg/upgrade/`, `cmd/pre-upgrade/` |

### security/ — Threat Models and Data Protection

Component threat models and sensitive data handling.

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `architecture/2024-08-controller-component-threat-model.md` | Controller Component Threat Model | `pkg/controller/`, `cmd/controller/` |
| `architecture/2024-08-dashboard-component-threat-model.md` | Dashboard Component Threat Model | Radius Dashboard component (part of overall Radius security posture) |
| `architecture/2024-11-ucp-component-threat-model.md` | UCP Component Threat Model | `pkg/ucp/`, `cmd/ucpd/` |
| `resources/2025-11-11-secrets-redactdata.md` | Redacting Sensitive Data | `pkg/crypto/encryption/` |

### recipes/ — Recipe Engine

Terraform and Bicep recipe support: module versioning, providers, registries, garbage collection, and recipe packs.

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `recipe/2023-07-terraform-template-version.md` | Terraform Module Versions | `pkg/recipes/terraform/module.go` |
| `recipe/2023-08-garbage-collection.md` | Recipe Resource Garbage Collection | `pkg/recipes/engine/` |
| `recipe/2023-08-recipes-test-plan.md` | Recipes Test Plan | `test/testrecipes/`, `test/functional-portable/` |
| `recipe/2023-09-populate-terraform-resourcs-ids.md` | Populate Terraform Resource IDs | `pkg/recipes/terraform/` |
| `recipe/2023-11-validate-template-path.md` | Validate Template Paths | `pkg/recipes/terraform/module.go` |
| `recipe/2023-11-support-insecure-registries.md` | Support Insecure Registries | `pkg/recipes/` configuration handling |
| `recipe/2024-01-support-private-terraform-repository.md` | Private Terraform Repository Support | `pkg/recipes/terraform/` |
| `recipe/2024-02-terraform-providers.md` | Multiple Terraform Providers | `pkg/recipes/terraform/config/providers/` |
| `recipe/2024-04-terraform-provider-secrets.md` | Terraform Provider Secrets | `pkg/recipes/terraform/config/` |
| `recipe/2024-06-private-bicep-registries.md` | Private Bicep Registries | `pkg/recipes/` |

### resource-types/ — Application Resource Types

Designs for application resource types not part of Applications.Core.

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `resources/2024-10-dapr-bindings.md` | Dapr Binding Implementation | `pkg/daprrp/` (Note: Dapr Bindings not yet in typespec; `pkg/daprrp/` handles Dapr resource types) |

### extensibility/ — User-Defined Types and Compute Extensibility

User-defined resource types, resource type registration, and compute platform extensibility (ACI, serverless).

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `architecture/2024-07-user-defined-types.md` | User-Defined Types | `pkg/dynamicrp/`, `cmd/dynamic-rp/`, `typespec/UCP/resourceproviders.tsp` |
| `architecture/2024-07-user-defned-types-schema-design.md` | User-Defined Types Schema Validation | `pkg/dynamicrp/`, `pkg/schema/` |
| `architecture/2024-08-resource-types-registration.md` | Resource Type Registration APIs | `typespec/UCP/resourceproviders.tsp`, `pkg/dynamicrp/api/` |
| `features/2024-06-resource-extensibility-feature-spec.md` | Resource Extensibility | `pkg/dynamicrp/`, `typespec/UCP/resourceproviders.tsp` |
| `features/2025-02-user-defined-resource-type-feature-spec.md` | User-Defined Resource Types | `pkg/dynamicrp/`, `typespec/UCP/resourceproviders.tsp` |

### control-plane/ — Universal Control Plane and Cloud Credentials

UCP planes APIs, AWS resource handling, and cloud provider authentication (Azure workload identity, AWS IRSA).

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `ucp/2024-03-planes-apis.md` | Planes APIs | `typespec/UCP/planes.tsp`, `typespec/UCP/aws-plane.tsp`, `typespec/UCP/azure-plane.tsp`, `typespec/UCP/radius-plane.tsp`, `pkg/ucp/frontend/` |
| `ucp/aws/handle-non-idempotent-resources/2023-09-handle-aws-non-idempotent-resources.md` | Handling Non-Idempotent AWS Resources | `pkg/ucp/aws/` |
| `cli/2024-04-azure-workload-identity.md` | Azure Workload Identity Support | `typespec/UCP/azure-credentials.tsp`, `pkg/ucp/credentials/azure.go` |
| `cli/2024-06-04-aws-irsa-support.md` | AWS IRSA Support | `typespec/UCP/aws-credentials.tsp`, `pkg/ucp/credentials/aws.go` |

### deployment/ — Deployment Controllers and GitOps

Kubernetes controllers for deployment templates and Flux-based GitOps integration.

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `architecture/2024-10-deploymenttemplate-controller.md` | DeploymentTemplate Controller | `pkg/controller/reconciler/deploymenttemplate_reconciler.go` |
| `features/2024-06-gitops-feature-spec.md` | GitOps Integration | `pkg/controller/reconciler/flux_controller.go` |
| `tools/2025-01-gitops-technical-design.md` | Radius Flux Controller Design | `pkg/controller/reconciler/flux_controller.go` |

### engineering/ — Testing, Workflows, and API Guidelines

Test strategy, CI/CD workflows, API design standards, and build system improvements.

| Source | Title | Corresponding Code in `radius` |
|--------|-------|-------------------------------|
| `tools/2023-12-test-organization.md` | Organization of Functional Tests | `test/` directory structure, `test/functional-portable/` |
| `tools/2025-03-workflow-changes.md` | GitHub Workflow Changes | `.github/` workflows |
| `guide/api-design-guidelines.md` | Radius API Guidelines | `typespec/`, `pkg/armrpc/` |
| `specs/001-lrt-current-release/` | Long-Running Tests Feature Spec | `test/` infrastructure |
| `specs/001-remove-bicep-types-submodule/` | Remove Bicep Types Submodule | Build system, `go.mod` |

### templates/ — Design Document Templates

Templates for authoring future design documents, feature specifications, and threat models.

| Source | Title | Rationale |
|--------|-------|-----------|
| `template/YYYY-MM-design-template.md` | Design Document Template | Supports future design work in radius repo |
| `template/YYYY-MM-feature-spec-template.md` | Feature Specification Template | Supports future design work in radius repo |
| `template/YYYY-MM-threat-model-template.md` | Threat Model Template | Supports future design work in radius repo |

---

## Not Recommended for Migration

These design documents describe features that are not yet implemented, are speculative/future proposals, or represent process documentation without corresponding code.

| Source | Title | Would-be Directory | Reason |
|--------|-------|-------------------|--------|
| `architecture/2024-05-radius-on-dapr.md` | Radius on Dapr | `architecture/` | Proposes replacing internal service infrastructure with Dapr. No evidence this was implemented; the service architecture still uses its own patterns. |
| `architecture/2025-10-terraform-bicep-settings.md` | Terraform & Bicep Settings Lifecycle | `recipes/` | Future feature for externalizing Terraform/Bicep recipe configuration into dedicated settings resources. No corresponding settings resource types exist in `typespec/`. |
| `recipe/2025-09-container.md` | Container Resource Recipe Migration | `recipes/` | Proposes replacing the imperative Go renderer for containers with a Bicep recipe. Container still uses the Go renderer chain (`pkg/corerp/renderers/container/`). |
| `features/2024-11-authz-feature-spec.md` | Authorization Feature | `control-plane/` | Granular access control and permissions for multi-tenant environments. No authorization/RBAC code exists in the radius repo. |
| `features/2025-07-10-offline-install-feature-spec.md` | Offline Installation | `engineering/` | Support for air-gapped environments. No specific offline installation code or mechanisms exist. |
| `features/2025-07-23-radius-configuration-ux.md` | Configuration UX | `engineering/` | User experience design recommendations for control plane configuration. UX guidance document without direct code implementation. |
| `features/2025-07-radius-resource-types-contribution.md` | Contributing Resource Types | `engineering/` | Community contribution process and pathways document. Not a code feature specification. |
| `features/2025-08-14-terraform-bicep-settings.md` | Terraform & Bicep Settings | `recipes/` | Feature spec for externalizing settings (same future feature as architecture doc above). No corresponding settings resources in `typespec/`. |
| `features/2025-08-29-container-resource-type.md` | Container Resource Type | `extensibility/` | Redesigned container resource type as part of compute extensibility. Represents future schema redesign, not current implementation. |
| `features/2025-09-02-routes-resource-type.md` | Routes Resource Type | `resource-types/` | New routes resource type replacing legacy gateways. No `routes.tsp` or routes implementation exists; `gateways.tsp` remains the current implementation. |
| `architecture/2024-08-applications-rp-component-threat-model.md` | Applications RP Threat Model | `security/` | Related to Applications.Core (`pkg/corerp/`, `cmd/applications-rp/`) — excluded from migration. |
| `recipe/2024-01-global-scope-secret-store.md` | Global Scope Secret Store | `recipes/` | Related to Applications.Core (`pkg/corerp/frontend/controller/secretstores/`) — excluded from migration. |
| `recipe/2025-08-recipe-packs.md` | Recipe Packs | `recipes/` | Related to Applications.Core (`pkg/corerp/frontend/controller/recipepacks/`) — excluded from migration. |
| `resources/2023-04-tls-termination.md` | TLS Termination | `resource-types/` | Related to Applications.Core (`typespec/Applications.Core/gateways.tsp`, `pkg/corerp/renderers/gateway/`) — excluded from migration. |
| `resources/2023-07-fail-deployments.md` | Classify Deployment Failures | `resource-types/` | Related to Applications.Core (`pkg/corerp/backend/`) — excluded from migration. |
| `resources/2023-10-app-graph.md` | Application Graph API | `resource-types/` | Related to Applications.Core (`pkg/corerp/frontend/controller/applications/`) — excluded from migration. |
| `resources/2023-10-recipe-details.md` | Recipe Information in Resources | `resource-types/` | Related to Applications.Core (`pkg/corerp/datamodel/`) — excluded from migration. |
| `resources/2023-10-simulated-environment.md` | Simulated Environment | `resource-types/` | Related to Applications.Core (`typespec/Applications.Core/environments.tsp`) — excluded from migration. |
| `resources/2024-06-support-secretstores-env.md` | Secret Stores in Environment Variables | `resource-types/` | Related to Applications.Core (`typespec/Applications.Core/secretStores.tsp`) — excluded from migration. |
| `resources/2025-01-gateway-timeouts.md` | Gateway Timeouts | `resource-types/` | Related to Applications.Core (`typespec/Applications.Core/gateways.tsp`) — excluded from migration. |
| `features/2024-07-secretstore-feature-spec.md` | Secret Stores Extension | `resource-types/` | Related to Applications.Core (`typespec/Applications.Core/secretStores.tsp`) — excluded from migration. |
| `architecture/2025-04-aci-support.md` | ACI Integration | `extensibility/` | Related to Applications.Core (`pkg/corerp/renderers/aci/`) — excluded from migration. |
| `architecture/2025-04-compute-extensibility.md` | Compute Platform Extensibility | `extensibility/` | Related to Applications.Core (`pkg/corerp/renderers/aci/`, `pkg/corerp/renderers/container/`) — excluded from migration. |
| `features/2025-01-serverless-feature-spec.md` | Serverless Container Platforms | `extensibility/` | Related to Applications.Core (`pkg/corerp/renderers/aci/`) — excluded from migration. |
| `features/2025-06-compute-extensibility-feature-spec.md` | Compute Platform Extensibility | `extensibility/` | Related to Applications.Core (`pkg/corerp/renderers/aci/`, `pkg/corerp/renderers/container/`) — excluded from migration. |

---

## Migration Notes

### Suggested Target Location

Design documents should be migrated to the `docs/design-notes/` directory in the radius repository using the following structure, organized by functional area:

```
radius/docs/design-notes/
├── architecture/      # System architecture, Kubernetes integration, upgrades
├── security/          # Threat models and data protection
├── recipes/           # Recipe engine: Terraform, Bicep, registries, packs
├── resource-types/    # Core resource type designs (gateways, secrets, Dapr, etc.)
├── extensibility/     # User-defined types, resource extensibility, compute platforms
├── control-plane/     # UCP, planes APIs, cloud credentials (Azure, AWS)
├── deployment/        # Deployment controllers, GitOps, Flux
├── engineering/       # Testing, CI/CD workflows, API guidelines
└── templates/         # Design document templates
```

This structure groups documents by the functional area of the Radius system they relate to, making it easier for developers to find relevant design context for the code they are working on:

- **architecture/** maps to the overall service structure (`cmd/`, `pkg/corerp/`, `pkg/ucp/`)
- **security/** maps to threat models for each component plus data protection (`pkg/crypto/`)
- **recipes/** maps to `pkg/recipes/` (Terraform and Bicep recipe engine)
- **resource-types/** maps to `pkg/daprrp/` (non-Applications.Core resource types)
- **extensibility/** maps to `pkg/dynamicrp/`, `typespec/UCP/resourceproviders.tsp`
- **control-plane/** maps to `pkg/ucp/`, `typespec/UCP/`
- **deployment/** maps to `pkg/controller/reconciler/`
- **engineering/** maps to `test/`, `.github/`, build configuration

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
