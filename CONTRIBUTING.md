# Contributing

Thank you for your interest in contributing to Xzcolp-AGI-Core.

## License
This repository is licensed under the MIT License. By contributing, you agree that your contributions will be licensed under the same MIT License.

## Branching & Commits
- Use feature branches named `feat/<short-description>` or `fix/<short-description>`.
- Commit messages should follow Conventional Commits: `type(scope): short summary`.

## Pull Requests
- Open a Pull Request against `main` for all non-trivial changes.
- PRs must include:
  - A clear description of the change and rationale
  - Related issue number (if any)
  - Tests added or updated
  - Security considerations (if applicable)
  - Migration notes (if applicable)

## Review & CI
- All PRs must pass CI: unit tests, linting (ruff), security scans (bandit/trivy), and code style checks.
- At least one approval is required before merging.

## Contributor License Agreement (CLA)
We use the Developer Certificate of Origin (DCO). Please sign-off your commits with `--signoff` or add `Signed-off-by: Your Name <you@example.com>` in the PR description.

## Security
- Do not commit secrets or credentials. Use Google Secret Manager for runtime secrets.
- Report security issues via the repository's Security Advisory process.

## Thanks
Thank you for improving Xzcolp-AGI-Core!