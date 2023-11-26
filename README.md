# Tag, release & publish automation

## Summary

This project demonstrates the setup required for tag, release & publish automation.

## Development process

1. Develop on feature branches
2. Merge to `main`
3. Release PR is created automatically and updated as more commits are made on `main`
4. Manually merge the PR, which automatically creates the tag and release notes
5. New version of the package is automatically published to NPM

## Solution

- Configure a pre-commit hook to enforce commit message syntax
  - https://github.com/conventional-changelog/commitlint
  - Enforce on the `main` branch only
  - Not required if `main` is protected but good to be safe
- Configure GitHub to enforce PR title syntax
  - https://github.com/marketplace/actions/semantic-pull-request
  - Enforce for PRs on the `main` branch only
- Configure `release-please` to automatically create a release PR on push to `main`
  - https://github.com/google-github-actions/release-please-action
  - Leverages the PR title syntax described above
  - **Note:** a release PR will only be created for releasable units, which are commits pre-fixed with:
    ```sh
    feat:
    fix:
    ```
    or breaking changes, which include a `!`:
    ```bash
    refactor!:
    fix!:
    # etc.
    ```
- Configure a workflow to publish to NPM after `release-please` has created the release
  - Done in the same workflow as above

### GitHub settings

- Give GitHub Actions write access
  - Settings > Actions > General > Workflow permissions
  - Select _"Read and write permissions"_
  - Select _"Allow GitHub Actions to create and approve pull requests"_
- Enforce squashed merges
  - Settings > General > Pull Requests
  - De-select _"Allow merge commits"_
- Add branch protection to `main`
  - Require a pull request before merging
  - Require status checks to pass before merging
    - Search for and select the action associated to the required status
  - Require branches to be up to date before merging
  - Require linear history
