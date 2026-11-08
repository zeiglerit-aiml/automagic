# Automagic — automation workspace

## Repository status

The current `main` branch contains no runnable application or automation source. It is a placeholder/workspace, not an installable tool or production automation service. The repository's historical Git storage may contain prior objects, but those are not part of the current tracked source tree.

## Intended boundary

Use this repository only when a distinct automation product or reusable automation library is ready to be maintained here. Argo CD deployment examples and cluster lifecycle helpers belong in [argo](https://github.com/zeiglerit-aiml/argo). AI/ML application and MLOps assistant code belongs in the relevant application repositories.

## Before adding code

- Define one supported automation use case and its owner.
- Add source, tests, dependency declarations, and a runnable quickstart.
- Document required credentials and use environment/secret stores rather than committed secrets.
- Add CI for linting, tests, dependency checks, and artifact integrity.
- Keep deployment permissions least-privilege and make destructive actions explicit.

Until those items exist, do not treat this repository as a deployable artifact.
