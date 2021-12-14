# Issue Comment GitHub Action

Comment on a GitHub Issue using a Handlebars template.

Features:

- Create comment
- Update comment
- Delete & Create comment

## Getting Started

```yml
name: 'Comment On Pull Request'

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  deploy:
    name: 'Render'
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2

      - uses: badsyntax/github-action-issue-comment@v0.0.1
        name: Comment on Pull Request
        if: github.event_name == 'pull_request'
        with:
          action: 'create-clean', # one of "create", "update", or "create-clean"
          template: '.github/pr-comment-template.hbs'
          templateInputs: |
            {
              "firstName": "Bob",
              "lastName": "Marley"
            }
```

## Action Inputs

| Name             | Description                                                                                                                                                                                                                                                     | Example                             |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `action`         | Action, one of "update", "create", or "create-clean'. The "update" action will first create a comment if it doesn't exist, else update it. "create" will create a new comment. "create-clean" will first delete the existing comment, then create a new comment | `update`                            |
| `template`       | The path to the handlebars template file                                                                                                                                                                                                                        | `./.github/pr-comment-template.hbs` |
| `templateInputs` | A JSON string object of key value pairs (can include newlines)                                                                                                                                                                                                  | `{"key":"value"}`                   |

## License

See [LICENSE.md](./LICENSE.md).
