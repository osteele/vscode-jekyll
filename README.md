# Jekyll extension for Visual Studio Code

A [Visual Studio Code](https://code.visualstudio.com) extension that adds
[problem
matchers](https://code.visualstudio.com/docs/editor/tasks#_processing-task-output-with-problem-matchers)
for Jekyll Liquid warnings and errors.

## Usage

Use these problem matchers in [Visual Studio Code
tasks](https://code.visualstudio.com/docs/editor/tasks) by using their names
`"$jekyll-warning"` and `"$jekyll-error"`.

For [background
tasks](https://code.visualstudio.com/docs/editor/tasks#_background-watching-tasks)
such as `jekyll serve`, use `"$jekyll-warning-watch"` and
`"$jekyll-error-watch"`.

For example, a Jekyll project might define the following tasks in
`.vscode/tasks.json`:

```json
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Serve",
      "type": "shell",
      "command": "bundle exec jekyll serve --livereload",
      "group": {
        "kind": "test",
        "isDefault": true
      },
      "isBackground": true,
      "problemMatcher": ["$jekyll-error-watch", "$jekyll-warning-watch"]
    },
    {
      "label": "Build",
      "type": "shell",
      "command": "bundle exec jekyll build",
      "group": "build",
      "problemMatcher": ["$jekyll-error", "$jekyll-warning"],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```

## Future Work

* [ ] Recognize non-Liquid Jekyll errors
* [ ] Add the tasks, if `_config.yml` is present.
* [ ] Can the matchers be combined? (Is the VSCode "severity" case-insensitive?)

## Bugs

Reported line numbers are off by the number of lines (frontmatter and blank
lines) that precede the first non-whitespace document content. See
jekyll/jekyll#7192.

## License

MIT
