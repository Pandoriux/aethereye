# Project Conventions

These are my personal conventions, based on established standards and extended with my own preferences.

## Git

### Commits

These are conventions for writing git commit messages, based on [Conventional Commits](https://www.conventionalcommits.org/), and extended with my own preferences.

```text
<type>(<scope>/<optional sub-scope(s)>): <description>

<optional body>

<optional footer(s)>
```

Commit header (`type`, `scope`, `description`) are **mandatory**.

`sub-scope`, `body` and `footer` are **optional**.

Commits should be **atomic**, if one file change touches different sub-scopes, only commit the part of the file that fits with one sub-scope.

Yes

```text
feat(ui/item-card): add item card component
```

```text
feat(ui): update global styles
```

```text
feat(readme): update project readme
```

No

```text
feat(ui/item, ui/collection): add item card and collection card
```

#### Types

- `release`: commits tagged as releases
- `feat`
- `fix`
- `refactor`
- `perf`
- `style`
- `docs`
- `build`
- `chore`
- `...`

For `BREAKING CHANGE`, appends a `!` after the scope:

```text
<type>(<scope>/<optional sub-scope(s)>)!: <description>
```

include `BREAKING CHANGE: <description>` in footer.

There is also a `wip-<optional type>` type, which prefixes the above types, signaling that the commit is still a work in progress. Such commits should only exist on **development branches** and must be **squashed** before merging into **main**.

- `wip`: generic work in progress. Use when the changes are too noisy or unorganized. Prefer a more explicit wip-* type below when possible
- `wip-feat`
- `wip-fix`
- `...`

#### Scopes and Sub-scopes

List of standard scopes and common sub-scopes. This is for reference only, not a full list.

- `project`: project
- `app`: app (ui + core)
- `ui`: web
- `core-ts`: typescript core
- `core-rs`: rust core
- `core-db`: database core
- `...`

#### Body (optional)

Commit body is free-form and may consist of any number of newline separated paragraphs.

#### Footers (optional)

- `Token: value`

```text
Signed-off-by: Pandoriux
Reviewed-by: Phong
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

#### Exceptions: Auto-Generated Commits

Some commits are created automatically by **Git**, **GitHub**, or other **automation tools**. These do **not** need to follow the convention and should be left as-is:

```text
Initial commit
```

```text
Merge branch 'dev' into 'main'
```

```text
Merge pull request #1 from owner/dev
```

```text
Revert "fix: correct logic"
```

```text
...
```

<br>

### Pull Requests

#### Title

The pull request `title` should follow the [Commit Convention Header](#commits), with some adjustments:

- **Scopes are optional:** you may omit scope and sub-scopes.
- **Pull requests do not have to be atomic:** unlike commits, a pull request may span multiple scopes, since the nature of a PR can be broader. That said, being atomic is still recommended.

```text
<type>(<optional scope>/<optional sub-scope(s)>): <description>
```

#### Description

For the `description body`, provide details if necessary. When relevant, cover:

- **What** was changed
- **Why** it was necessary
- **How** it was implemented

For trivial changes (e.g., dependency bumps), the description can be omitted or simplified.

> [!IMPORTANT]
> **Pull requests must be merged using a squash merge.**  
> When merging a pull request into `main`, use **squash merge**, and ensure the resulting commit still strictly adheres to the [Commit Convention](#commits).

<br>

### Branches

Use `/` to divide segments and `-` to separate words.

```text
release/v1.x.x
```

```text
feat/google-oauth2
```
