# Automagic — legacy multi-cloud automation workspace

## Important branch status

The repository has two unrelated histories:

- `main` is a new placeholder branch containing this README.
- `master` contains the substantial legacy project tree. A GitHub comparison reports no common ancestor between `main` and `master`; this is not a simple fast-forward or safe branch rename.

The `master` tree currently contains approximately 10,340 tracked entries, including:

- `aws/` — about 8,561 entries, including a large vendored Python Lambda runtime/dependency tree
- `observ/` — about 956 entries
- `gcp/` — about 605 entries
- `IAC/` — Terraform and infrastructure modules
- `AI_ML/` — AI/ML and inference prototypes
- `tools/` and `poc/` — utilities and proof-of-concept projects

The tree includes thousands of Python files and native/binary dependencies. This repository is therefore **not empty and is not a deletion/archive candidate** until its legacy branch has been inventoried.

## Safe consolidation plan

1. Keep both refs intact while inventorying the `master` tree and its deployment entry points.
2. Identify unique applications, infrastructure modules, vendored dependencies, generated packages, and obsolete experiments.
3. Scan the legacy tree for secrets, dependency vulnerabilities, licenses, executable artifacts, and unsafe deployment/teardown behavior.
4. Assign each unique component to its canonical repository (for example, Argo CD helpers to `argo`, shared Terraform modules to `terraform`, and AI/ML application source to the relevant application repository).
5. Migrate only reviewed source and required history. Do not copy the vendored Python runtime wholesale unless a reproducible packaging requirement justifies it.
6. After migration and validation, decide whether `main` should become the consolidated canonical branch and whether `master` can be retired.

## Current usage

Do not treat the current `main` branch as a deployable automation application. Do not delete, archive, force-reset, or merge `master` until the migration inventory is complete.

## Portfolio ownership

Legacy multi-cloud automation archive. Preserve main and master until the large legacy master tree is inventoried, scanned, and any unique source is migrated.

Account-wide ownership, consolidation decisions, and repository status are maintained in the [WSP portfolio repository catalog](https://github.com/zeiglerit-aiml/WSP_Integrated_AI_SDLC_GVC_pl/blob/main/REPOSITORY_CATALOG.md).

## Legacy branch inventory (2026-11-08)

The `master` branch was inspected through its recursive Git tree. It contains 10,340 tracked entries and is a substantial legacy workspace, not a disposable placeholder.

| Top-level area | Tracked entries | Initial interpretation |
|---|---:|---|
| `aws/` | 8,561 | Lambda/runtime packages and AWS automation; includes vendored Python dependencies |
| `observ/` | 956 | Observability tooling; includes a tracked Python virtual environment |
| `gcp/` | 605 | GCP scripts and Terraform; includes a tracked Python virtual environment and Terraform working files |
| `IAC/` | 69 | Terraform modules, policies, provider configuration and variables |
| `AI_ML/` | 61 | Inference, RAG, MCP, Helm and security proof-of-concepts |
| `poc/` | 36 | Application, Kubernetes and IaC prototypes |
| `tools/` | 37 | Cloud administration, deployment and teardown utilities |
| Other (`PAC/`, `azure/`, `cont/`, `tests/`, root) | 15 | Small supporting examples and metadata |

### Review findings and migration safeguards

- `gcp/activate/` and `observ/venv/` contain tracked virtual-environment content. These are generated environment artifacts, not maintainable source dependencies; identify required package pins before removing them.
- `aws/python_lambda/python/` and `aws/python_layer/python/` contain vendored Python dependency trees. Do not migrate these wholesale; recover their build manifests and reproduce packages from pinned dependencies.
- `IAC/terraform.tfvars` is tracked and contains AWS account/role identifiers and deployment parameters. The inspected values are not credentials, but the file should be replaced by a sanitized example and excluded from Git after confirming no secret values exist in the full history.
- The current `.gitignore` does not broadly exclude all `*.tfvars` files. Correct this only alongside a safe example-file convention and migration plan.
- `tools/` contains cloud deletion and teardown utilities (including AWS, Azure and GCP helpers). Do not execute these during inventory or CI; review target checks and confirmation safeguards individually.
- The recursive tree inspection did not constitute a secret scan, dependency vulnerability scan, license review, Terraform validation, or runtime test. Treat all legacy code as untrusted until those checks are completed.
- `IAC/` contains candidate reusable infrastructure modules, but provider/version consistency, state strategy, tests and module boundaries must be assessed before moving any code into the shared `terraform` repository.

### Recommended migration sequence

1. Preserve `master` and its history; do not merge it into the unrelated `main` history.
2. Scan the full branch for credentials, private keys, tokens, state files and sensitive configuration. Rotate any exposed credential; removing a file from the current tree does not erase Git history.
3. Inventory and test source independently of vendored environments and generated artifacts.
4. Migrate reviewed, uniquely owned modules to their canonical destinations: IaC modules to the shared Terraform repository only after module tests; Argo/Kubernetes material to `argo`; AI/ML pipeline components to `mapcf` or the owning application; security examples to `security`.
5. Preserve provenance and original commit references in the migration record. Do not delete duplicate-looking files until content and usage have been compared.
6. Only after migration and CI validation, decide whether to archive `automagic` or retire `master`.
