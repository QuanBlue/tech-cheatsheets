<h1 align="center">
  <img src="./assets/Commit-Convention/commit-convention-logo.jpeg" alt="icon" height="150"></img>
  <br>
  <b>Commit Convention</b>
</h1>

<p align="center">  Concise, descriptive messages following a standard format for clear communication and effective collaboration.</p>

<!-- Badges -->
<p align="center">
  <a href="https://github.com/quanblue/tech-cheatsheets/graphs/contributors">
    <img src="https://img.shields.io/github/contributors/quanblue/tech-cheatsheets" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/quanblue/tech-cheatsheets" alt="last update" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/network/members">
    <img src="https://img.shields.io/github/forks/quanblue/tech-cheatsheets" alt="forks" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/stargazers">
    <img src="https://img.shields.io/github/stars/quanblue/tech-cheatsheets" alt="stars" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/issues/">
    <img src="https://img.shields.io/github/issues/quanblue/tech-cheatsheets" alt="open issues" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/quanblue/tech-cheatsheets.svg" alt="license" />
  </a>
</p>

<p align="center">
  <b>
      <a href="https://github.com/quanblue/tech-cheatsheets">Home page</a> •
      <a href="https://github.com/quanblue/tech-cheatsheets/tree/master/Version%20Control">Version Control page</a> •
      <a href="https://github.com/QuanBlue/Tech-Cheatsheets/tree/master/Version%20Control/Git">Git page</a>
  </b>
</p>

<br/>

<details open>
<summary><b>📖 Table of Contents</b></summary>

-  [Introduction](#rainbow-introduction)
-  [Rule](#construction-rule)
-  [Structure](#building_construction-structure)
   -  [Type](#type)
   -  [Scope](#scope)
   -  [Specification](#specification)
-  [Examples](#page_facing_up-examples)
-  [Benefits of Commit Convention](#mechanical_arm-benefits-of-commit-convention)
-  [Integration with Automation Tools](#toolbox-integration-with-automation-tools)
-  [Credits](#sparkles-credits)

</details>

# :rainbow: Introduction

Using a `commit convention` helps maintain a consistent and informative commit history. It allows team members to quickly understand the purpose and impact of each commit, making collaboration and code maintenance more efficient.

# :construction: Rule

-  Use the **Imperative**, **Present tense**:
   _Example:_ "change" not "changed" nor "changes"
-  Don't capitalize the first letter
-  No dot (.) at the end

# :building_construction: Structure

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Type

**`revert`**: Revert commit

**`build`**: Changes that affect the build system or external dependencies
_Example scopes: gulp, broccoli, npm,…_

**`ci`**: Changes to our CI configuration files and scripts
_Example scopes: Travis, Circle, BrowserStack, SauceLabs_

**`docs`**: Documentation only changes

**`feat`**: A new feature

**`fix`**: A bug fix

**`perf`**: A code change that improves performance

**`refactor`**: A code change that neither fixes a bug nor adds a feature

**`style`**: Changes that do not affect the meaning of the code
_Example scopes_: white-space, formatting, missing semi-colons, etc

**`test`**: Adding missing tests or correcting existing tests

## Scope

> `The scope` should be the name of the **npm package affected**

<details>
<summary>List of supported scopes</summary>

`core`

`animations`

`language-service`

`service-worker`

`platform-server`

`platform-browser`

`platform-browser-dynamic`

`platform-webworker`

`platform-webworker-dynamic`

`http`

`forms`

`common`

`router`

`upgrade`

`elements`

`compiler`

`compiler-cli`

</details>

There are currently a few exceptions to the **use package name** rule:

-  **`packaging`**: used for changes that change the _npm package_ layout in all of our packages (e.g. public path changes, _package.json_ changes done to all packages, _d.ts_ file/format changes, changes to bundles,…)
-  **`changelog`**: used for updating the release notes in _CHANGELOG.md_
-  **`aio`**: used for docs-app (_angular.io_) related changes within the `/aio` directory of the repo
-  `none/empty string`: useful for `style`, `test` and `refactor` changes that are done across all packages (e.g. `style: add missing semicolons`)

## Specification

The key words `MUST`, `MUST NOT`, `REQUIRED`, `SHALL`, `SHALL NOT`, `SHOULD`, `SHOULD NOT`, `RECOMMENDED`, `MAY`, and `OPTIONAL` in this document are to be interpreted as described in [**RFC 2119**](https://www.ietf.org/rfc/rfc2119.txt).

-  **Commits** MUST be prefixed with a type, which consists of a noun, `feat`, `fix`, etc., followed by the OPTIONAL scope, OPTIONAL `!`, and REQUIRED terminal colon and space.
-  **A scope** MAY be provided after a type.

   > A scope MUST consist of a noun describing a section of the code base surrounded by parenthesis, e.g: `fix(parser):`

-  **A description** MUST immediately follow the colon and space after the type/scope prefix.

   > The description is a short summary of the code changes,
   > e.g., `fix: array parsing issue when multiple spaces were contained in string`

-  **A longer commit body** MAY be provided after the short description, providing additional contextual information about the code changes.

   > The commit body MUST begin one blank line after the description.

   > The commit body is free-form and MAY consist of any number of newline separated paragraphs.

-  **One or more footers** MAY be provided one blank line after the body.

   > Each footer MUST consist of a word token, followed by either a `:<space>` or `<space>#` separator, followed by a string value (this is inspired by the **[git trailer convention](https://git-scm.com/docs/git-interpret-trailers)**).

   > A footer’s token MUST use `` in place of whitespace characters, e.g., `Acked-by` (this helps differentiate the footer section from a multi-paragraph body. An exception is made for `BREAKING CHANGE`, which MAY also be used as a token.

   > A footer’s value MAY contain spaces and newlines, and parsing MUST terminate when the next valid footer token/separator pair is observed.

-  **Breaking changes** MUST be indicated in the type/scope prefix of a commit, or as an entry in the footer.

   > -  If included as a footer, a breaking change MUST consist of the uppercase text `BREAKING CHANGE`, followed by a colon, space, and description,
   >    e.g., `BREAKING CHANGE: environment variables now take precedence over config files`

   -  If included in the type/scope prefix, breaking changes MUST be indicated by a `!` immediately before the `:`. If `!` is used, `BREAKING CHANGE:` MAY be omitted from the footer section, and the commit description SHALL be used to describe the breaking change.
      >

   > `BREAKING-CHANGE` MUST be synonymous with `BREAKING CHANGE`, when used as a token in a footer.

-  The units of information that make up Conventional Commits MUST NOT be treated as case sensitive by implementors, with the exception of BREAKING CHANGE which MUST be uppercase.

---

# :page_facing_up: Examples

**Commit message with description and breaking change footer**

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

**Commit message with `!` to draw attention to breaking change**

```
feat!: send an email to the customer when a product is shipped
```

**Commit message with scope and `!` to draw attention to breaking change**

```
feat(api)!: send an email to the customer when a product is shipped
```

**Commit message with both `!` and BREAKING CHANGE footer**

```
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

**Commit message with no body**

```
docs: correct spelling of CHANGELOG
```

**Commit message with scope**

```
feat(lang): add Polish language
```

**Commit message with multi-paragraph body and multiple footers**

```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```

# :mechanical_arm: Benefits of Commit Convention

Adhering to a commit convention offers several advantages:

-  **Clear communication:** Understand the purpose and impact of a commit at a glance.
-  **Ease of navigation:** Quickly find relevant commits using search and filtering tools.
-  **Effective collaboration:** Facilitate code reviews and provide valuable feedback.
-  **Maintenance and debugging:** Simplify tracking changes and identifying bug fixes.

# :toolbox: Integration with Automation Tools

Commit conventions can be integrated with automation tools, such as Continuous Integration (CI) systems or changelog generators. These tools can automatically generate release notes or trigger specific actions based on commit messages following the convention.

-  [**Better-commits**](https://github.com/Everduin94/better-commits) - A CLI tool that helps you write better commit messages.

# :sparkles: Credits

-  [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/#commit-message-with-multi-paragraph-body-and-multiple-footers)

---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
