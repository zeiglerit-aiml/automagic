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
