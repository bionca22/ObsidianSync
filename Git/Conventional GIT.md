

#### Convencional Branch
- **`main`**: The main development branch (e.g., `main`, `master`, or `develop`)
- **`feature/`** (or **`feat/`**): For new features (e.g., `feature/add-login-page`, `feat/add-login-page`)
- **`bugfix/`** (or **`fix/`**): For bug fixes (e.g., `bugfix/fix-header-bug`, `fix/header-bug`)
- **`hotfix/`**: For urgent fixes (e.g., `hotfix/security-patch`)
- **`release/`**: For branches preparing a release (e.g., `release/v1.2.0`)
- **`chore/`**: For non-code tasks like dependency, docs updates (e.g., `chore/update-dependencies`)

##### Basic Rules

1. **Use Lowercase Alphanumerics, Hyphens, and Dots**: Always use lowercase letters (`a-z`), numbers (`0-9`), and hyphens(`-`) to separate words. Avoid special characters, underscores, or spaces. For release branches, dots (`.`) may be used in the description to represent version numbers (e.g., `release/v1.2.0`).
2. **No Consecutive, Leading, or Trailing Hyphens or Dots**: Ensure that hyphens and dots do not appear consecutively (e.g., `feature/new--login`, `release/v1.-2.0`), nor at the start or end of the description (e.g., `feature/-new-login`, `release/v1.2.0.`).
3. **Keep It Clear and Concise**: The branch name should be descriptive yet concise, clearly indicating the purpose of the work.
4. **Include Ticket Numbers**: If applicable, include the ticket number from your project management tool to make tracking easier. For example, for a ticket `issue-123`, the branch name could be `feature/issue-123-new-login`.


----

#### Convencional Commit

1. **fix:** a commit of the _type_ `fix` patches a bug in your codebase (this correlates with [`PATCH`](http://semver.org/#summary) in Semantic Versioning).
2. **feat:** a commit of the _type_ `feat` introduces a new feature to the codebase (this correlates with [`MINOR`](http://semver.org/#summary) in Semantic Versioning).
3. **BREAKING CHANGE:** a commit that has a footer `BREAKING CHANGE:`, or appends a `!` after the type/scope, introduces a breaking API change (correlating with [`MAJOR`](http://semver.org/#summary) in Semantic Versioning). A BREAKING CHANGE can be part of commits of any _type_.
4. _types_ other than `fix:` and `feat:` are allowed, for example [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional) (based on the [Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)) recommends `build:`, `chore:`, `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, and others.
5. _footers_ other than `BREAKING CHANGE: <description>` may be provided and follow a convention similar to [git trailer format](https://git-scm.com/docs/git-interpret-trailers).