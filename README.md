# Tag & release automation

## Summary

This project demonstrates a GitHub Actions workflow that automates the tag & release process for a NPM package.

## Target development process

1. Develop on feature branches
2. Merge to `main` using a commit message syntax, e.g. [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
3. Manually trigger the workflow from the GitHub Actions UI

## Solution

- Configure a pre-commit hook to enforce commit message syntax
  - https://github.com/conventional-changelog/commitlint
  - Enforce on the `main` branch only
- Configure GitHub to enforce PR title syntax
  - Enforce for PRs on the `main` branch only

### GitHub settings

- Enable "Read and write permissions" for GitHub Actions
  - Settings > Actions > General > Workflow permissions
