# checkout-repo-with-matching-branch

A GitHub Action to checkout a different repo with a branch that matches the branch in the current repo

In Bullet Train we use this to be able to properly test across repo boundaries when there are "join PRs" that require changes to be made in more than one repo.

## Usage

```yaml
- name: Checkout Starter Repo
  uses: bullet-train-co/checkout-repo-with-matching-branch@v1
  with:
    target_dir: tmp/starter
    repository: bullet-train-co/bullet_train
```

## Action Inputs

| Name | Description | Default |
| --- | --- | --- |
| `target_dir` | The directory where you want the other repo to be placed. | N/A |
| `repository` | The name of the other repo to be checked out. | N/A |
| `target_branch` | The branch that you want to try to match. Leave blank to match against the current branch. | `{{ github.head_ref }}` |
| `default_branch` | The branch to use if no matching branch is found. | `main` |

## Action Outputs

None

TODO: Maybe we should output some things?

## Reference Example

Here is an example workflow. In this example we're checking out the `bullet-train-co/bullet_train` repository at `tmp/starter`:

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  check_out_starter_repo:
    runs-on: ubuntu-latest
    name: Bullet Train Minitest

    steps:
      - name: Checkout This Repo
        uses: actions/checkout@v4

      - name: Checkout Bullet Train Starter Repo
        uses: bullet-train-co/checkout-repo-with-matching-branch@v1
        with:
          target_dir: tmp/starter
          repository: bullet-train-co/bullet_train
```
