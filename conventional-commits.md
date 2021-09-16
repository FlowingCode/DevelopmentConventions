## Flowing Code Commit Message Guidelines / 1.0.0-rc.4

The following guidelines are an extension of the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/), which provides an easy set of rules for creating an explicit commit history and dovetails with [SemVer](https://semver.org/spec/v2.0.0.html) by describing the features, fixes, and breaking changes made in commit messages. 

These guidelines encourage [logically atomic commits](https://benmatselby.dev/post/logical-commits/), i.e. commits that are big enough to add value to the project, and small enough to read, review and revert. There is no hard and fast rule for determining what adds value to the project, or what is small enough: use common sense.

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
  - Commits that contribute to the application source code:
    - `feat:` A new feature (correlates with MINOR in semantic versioning)
    - `fix:` A bug fix (correlates with PATCH in semantic versioning)
    - `perf:` A code change that improves performance
    - `refactor:` A code change that neither fixes a bug, nor adds a feature, nor implement a performance improvement
  
  - Commits that contribute to unit tests:
    - `test:` Adding missing tests or refactoring/fixing existing tests  

  - Commits that contribute to the build process and external dependencies:  
    - `build:` Changes to the build process or external dependencies affecting the exported artifacts (i.e. those artifacts that are created as a result of such process, and are utilized as final deliverables or included in other external projects). Correlates with a PATCH, MINOR or MAJOR increment in semantic versioning, depending on the nature of the change
    - `ci:` Changes to the CI configuration, and other changes to the build process or external dependencies with no impact in the exported artifacts (e.g.: configure code quality metrics, add dependencies that are only needed for running unit tests). Does not correlate with an increment in semantic versioning, because the versioned artifacts are not modified

 - Trivial commits:
    - `docs:` Documentation only changes 
    - `style:` Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)    

 - Other commits:
    - `revert:` Reverts a previous commit
    - `chore:` Changes, not covered by other types
    - `WIP:` Incomplete changes ("work in progress")

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

The commit body is free-form text and may consist of any number of newline separated paragraphs. It may contain URIs and links to other issues.

If possible, use the imperative present tense ("change" not "changed" nor "changes") and follow basic grammar rules: capitalize the first letter, end each sentence with a period, etc. This restriction can be relaxed.

### 5. Footer
Optional. One or more footers may be provided one blank line after the body. Footers contains additional information about the commit, such as a description of the breaking changes, the list of issues that the commit will close, and other metadata. 

Each footer consists of a word *token*, followed by either a `:<space>` or `<space>#` separator, followed by a string *value*.

```
Token: value
Token #value
```

The following footers are defined: 
* `BREAKING CHANGE:` describes the breaking changes introduced by the commit. When this footer is used, the breaking change indicator `!` must be added in the header line.

* `Close #` provides a link to a single issue that is closed by the commit.

* [`Co-authored-by: `](https://docs.github.com/en/free-pro-team@latest/github/committing-changes-to-your-project/creating-a-commit-with-multiple-authors) collects the name and email address for each co-author.

The tokens are case-insensitive, with the exception of `BREAKING CHANGE: ` (which must be uppercase).
Other footers may be included following the syntax given above.

#### Examples
```
BREAKING CHANGE: description
Close #42
Close #43
Co-authored-by: name <name@example.com>
Co-authored-by: another-name <another-name@example.com>
```

### Revert commits

If the commit reverts a previous commit:
- The commit *type* must be `revert:`
- The commit *subject* must begin with the *type* of the reverted commit, followed by the *subject* of the reverted commit.
- The commit message should contain the SHA of the commit(s) being reverted.

#### Example
```
revert: chore: update README.md

Revert commit b3befad91a6e39288ea53d540a4a483b0898fb49.
```

### WIP commits

WIP commits are temporary in nature and expected to be replaced by a final logically atomic commit.

In order to mark a commit as work-in-progress:
- The commit *type* must be `WIP:` (uppercase)
- The commit *subject* must begin with the *type* of the in-progress commit, followed by the *subject* of the in-progress commit.
- The commit message body may describe the current status of the implementation, in addition to other information that is intended for the final commit message.

#### Example

An initial commit was added with a partial fix:
```
WIP: fix: prevent orders with negative amount of items

Validation was added in the creation form. 
Need to consider the case of editing an existing orders.
```

After the changes are complete, the commit message will be rewritten as:
```
fix: prevent orders with negative amount of items

Add validation in the creation and edition forms.
```

### FAQ

#### What type to use for visual content changes?

Use the appropriate type, depending on the nature of the change. For instance: changes to Cascading Style Sheets contribute to the application source code (`fix`, `refactor`, etc.) and changes to static resources do not contribute to the application code, and are not covered by other types (`chore`). Note that the `style` type addresses changes that do not affect the meaning of the code (such as formatting).
  
```
fix: fix overlapping problem in divs
refactor: use css variables instead of hardcoded values
chore: replace the landing page banner
style: format CSS style rules
```


#### What type to use when removing a class or method?

A commit that only removes a class or method is a `refactor` (i.e. a code change that neither fixes a bug, nor adds a feature). 
If the class or method is part of the public API, the commit introduces a BREAKING CHANGE.

```
refactor!: delete class Foo 
```

### References
  - [Conventional Commits specification 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/)
  - [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html)
  - Ben Selby. [Logically atomic commits](https://benmatselby.dev/post/logical-commits/)
  - Clarice Bouwer. [Why I Create Atomic Commits In Git](https://dev.to/cbillowes/why-i-create-atomic-commits-in-git-kfi)
    
### Bibliography
  - [Angular convention](https://github.com/angular/angular/blob/88fbc06/CONTRIBUTING.md#-commit-message-guidelines) (88fbc06)
  - Chris Beams. [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
