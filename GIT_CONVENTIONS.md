# Git Conventions

These are my personal Git conventions, based on established standards and extended with my own preferences.

## Commits

These are conventions for wirtting git commit message, based on [Conventional Commits](https://www.conventionalcommits.org/), and extended with my own preferences.

```text
<type>(<layer>.<module>.<optional nested module(s)>): <description>

<optional body>

<optional footer(s)>
```

Commit header (`type`, `layer`, `module`, `description`) are all **mandatory**.

`nested module`, `body` and `footer` are **optional**.

Commit should be **atomic**, if one file change contains different modules, only commit the part of the file that fits with one module.

Yes

```text
feat(fe.item): add item card
```

```text
feat(fe.rte.lexical): add bold to lexical editor
```

No

```text
feat(fe): add item detail page
```

```text
feat(fe.item, fe.collection): add item card and collection card
```

### Types

- `release`: commits tagged as releases
- `feat`
- `fix`
- `refactor`
- `perf`
- `style`
- `docs`
- `build`
- `chore`

For `BREAKING CHANGE`, appends a `!` after the scope:

```text
<type>(<layer>.<module>)!: <description>
```

include `BREAKING CHANGE: <description>` in footer.

There is also a `wip-<optional type>` type, which prefixes the above types, signaling that the commit is still a work in progress. Such commits should only exist on **development branches** and must be **squashed** before merging into **main**.

- `wip`: generic work in progress. Use when the changes are too noisy or unorganized. Prefer a more explicit wip-* type below when possible
- `wip-feat`
- `wip-fix`
- `...`

### Scopes (Layers and Modules)

- `project`: project-wide
  - `.ci`
  - `.cd`
- `fe`: frontend (js)
- `be`: backend (rust)
- `bridge`: ipc between fe and be (commands, events)
- `db`: database (sqlite)

### Body (optional)

Commit body is free-form and may consist of any number of newline separated paragraphs.

### Footers (optional)

- `Token: value`

```text
Signed-off-by: pan
Reviewed-by: phong
```

- `Verb #issue`

```text
Closes #123
Fixes #456
Resolves #789
```

- `BREAKING CHANGE`

```text
BREAKING CHANGE: <description>
```

### Exceptions: Auto-Generated Commits

Some commits are created automatically by **Git**, **GitHub**, or other **automation tools**. These do **not** need to follow the convention and should be left as-is:

```text
Initial commit
```

```text
Merge branch 'main' into 'develop'
```

```text
Merge pull request #1 from phong/develop
```

```text
Revert "fix: correct typo"
```

```text
...
```

<br>

## Pull Requests

### Title

The pull request `title` should follow the [Commit Convention Header](#commits), with some adjustments:

- **Scopes are optional**: you may omit layers and/or modules.  
- **Pull requests do not have to be atomic**: unlike commits, a pull request may span multiple scopes or modules, since the nature of a PR can be broader.  

```text
<type>(<optional layer>.<optional module>): <description>
```

However, when merging a pull request into `main` (always using **squash merge**), the **resulting** commit **must still strictly adhere** to the [Commit Convention](#commits).

In the case of merging a broad pull request, since releases are automated by [release-please](https://github.com/googleapis/release-please), use its [commit override](https://github.com/googleapis/release-please?tab=readme-ov-file#how-can-i-fix-release-notes) feature to  consolidate multiple changes into a single, well-formatted commit.

Example (add override block to commit body):

```text
BEGIN_COMMIT_OVERRIDE
feat: add ability to override merged commit message

fix: another message
chore: a third message
END_COMMIT_OVERRIDE
```

### Description

For the `description body`, provide details if necessary. When relevant, cover:

- **What** was changed
- **Why** it was necessary
- **How** it was implemented

For trivial changes (e.g., version bumps), a description may be omitted or simplified.

<br>

## Branchs

Use `/` to divide segments and `-` to separate words.

```text
release/v1.x.x
```

```text
feature/google-oauth2
```
