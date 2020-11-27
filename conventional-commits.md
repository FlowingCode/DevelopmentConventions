## Flowing Code Commit Message Guidelines / 1.0.0-SNAPSHOT

The following rules are based on the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/), which provides an easy set of rules for creating an explicit commit history.
This convention dovetails with [SemVer](https://semver.org/spec/v2.0.0.html) by describing the features, fixes, and breaking changes made in commit messages.
Some elements and definitions were taken from the [Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines) and (see [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/).


### Commit Message Format
Each commit message consists of a **header**, a **body** and a **footer**. The **header** has a special format that includes a **type**, a **scope** and a **subject**. The **type** and **subject** are required, all the other parts are optional.

```
<type>[optional scope][!]: <subject>

[optional body]

[optional footer(s)]
```

(Commits by the maven-release-plugin are excluded from these guidelines.)

### 1. Type
Required. Must be one of the following: 
  - `build:` Changes that affect the build system or external dependencies (e.g.: configure plugins and dependencies in pom.xml)
  - `ci:` Changes to our CI configuration files and scripts, with no impact in the released artifact (e.g.: set metadata and profiles in pom.xml, edit DockerFile)
  - `chore:` Maintenance changes not covered by other types.
  - `docs:` Documentation only changes
  - `feat:` A new feature (correlates with MINOR in semantic versioning)
  - `fix:` A bug fix (correlates with PATCH in semantic versioning)
  - `perf:` A code change that improves performance
  - `refactor:` A code change that neither fixes a bug nor adds a feature
  - `revert:` Reverts a previous commit
  - `style:` Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
  - `test:` Adding missing tests or correcting existing tests

Type values are lowercase.

An **exclamation mark** `!` following the **type** (and **scope**, if present) indicates a breaking change (correlating with MAJOR in semantic versioning). A breaking change can be part of commits of any type. Additional details on the breaking change, if needed, can be provided in the footer section.

### 2. Scope
Optional. Provides additional contextual info. The scope (if any) is written surrounded by parenthesis. A scope name consists of a noun describing a section of the codebase.
The granularity of scopes and their allowed values are defined on a per-project basis. 

Addons projects define the scope `demo` for those changes affecting the demo source code; other changes use the unnamed scope. 

### 3. Subject
Required. A succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize the first letter
* no dot (.) at the end
* the length of the header line (including type and scope) must be less than 72 characters.

A properly formed Git commit subject line should always be able to complete the following sentence:<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;If applied, this commit will _subject_

#### Examples
✔️ "implement cool feature" → If applied, this commit will _implement cool feature_<br>
❌ "if applied, this commit will implement cool feature" → If applied, this commit will _if applied, this commit will implement cool feature_<br>
❌ "implemented cool feature" → If applied, this commit will _implemented cool feature_<br>
❌ "implements cool feature" → If applied, this commit will _implements cool feature_<br>
❌ "cool feature" → If applied, this commit will _cool feature_<br>


### 4. Body
Optional. Should include the motivation for the change and contrast this with previous behavior.

If possible, use the imperative, present tense, just as in the **subject**. (This restriction can be relaxed.)

### 5. Footer
Optional. Contains additional information about breaking changes (`BREAKING CHANGE:` footer), and it is also the place to reference GitHub issues that this commit Closes (`Closes` footer). Other footers may be provided following a convention similar to [git trailer format](https://git-scm.com/docs/git-interpret-trailers).

One or more footers may be provided one blank line after the body. Each footer must consist of a word token, followed by either a `:<space>` or `<space>#` separator, followed by a string value. Footer tokens are case-insensitive, with the exception of of `BREAKING CHANGE` (which must be uppercase).

```
BREAKING CHANGE: <description>
Closes #42
```

When the `BREAKING CHANGE:` footer is used, the breaking change indicator `!` must be added in the header line.
