# Autosquash

_Based on the `rebase` action by `cirrus-actions`. Thanks for making an awesome action!_

After installation simply comment `/autosquash` to trigger the action:
# Installation

To configure the action simply add the following lines to your `.github/workflows/autosqaush.yml` workflow file:

```yml
on:
  issue_comment:
    types: [created]
name: Autosquash
jobs:
  autosquash:
    name: Autosquash
    if: github.event.issue.pull_request != '' && contains(github.event.comment.body, '/autosquash')
    runs-on: ubuntu-latest
    steps:
    - name: Checkout the latest code
      uses: actions/checkout@v2
      with:
        fetch-depth: 0
    - name: Autosquash
      uses: StarryInternet/autosquash@main
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Restricting who can call the action

It's possible to use `author_association` field of a comment to restrict who can call the action and skip the rebase for others. Simply add the following expression to the `if` statement in your workflow file: `github.event.comment.author_association == 'MEMBER'`. See [documentation](https://developer.github.com/v4/enum/commentauthorassociation/) for a list of all available values of `author_association`.
