# Commit Spec

The following specification describes the commit message format for cis-oss projects.

Conforming to this specification helps us to automate the generation of changelogs and releases as well as ensure that our commit messages are consistent and easy to read.

## Spec

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

1. Commits MUST be prefixed with a type, which consists of a noun, feat, fix, etc., followed by the OPTIONAL scope, OPTIONAL !, and REQUIRED terminal colon and space.
2. The type MUST be one of the following:
    - ```feat```: A new feature
    - ```fix```: A bug fix
    - ```docs```: Documentation only changes
    - ```style```: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
    - ```refactor```: A code change that neither fixes a bug nor adds a feature
    - ```perf```: A code change that improves performance
    - ```test```: Adding missing tests
    - ```chore```: Changes to the auxiliary tools such as release scripts
    - ```build```: Changes to the dependencies, devDependencies, or build tooling
    - ```ci```: Changes to our Continuous Integration configuration
    - ```release```: SHALL be used ONLY by release tooling or lead maintainers making final changes for a release (e.g. bumping version number)
    - ```revert```: Used when reverting changes made in a commit. Commit MUST include Refs-footer when used. Refs-Footer MUST point to reverted commit.
3. A scope MAY be provided after a type. A scope MUST consist of a noun describing a section of the codebase surrounded by parenthesis, e.g., ```fix(parser):```.
4. A description MUST immediately follow the colon and space after the type/scope prefix.The description is a short summary of the code changes.
5. The description MUST use the imperative, present tense.
6. A longer commit body MAY be provided after the short description, providing additional contextual information about the code changes. The body MUST begin one blank line after the description.
7. The commit body MUST be written in the imperative, present tense.
8. A commit body is free-form and MAY consist of any number of newline separated paragraphs.
9. One or more footers MAY be provided one blank line after the body. Each footer MUST consist of a word token, followed by `:<space>` separator, followed by a string value.
10. Permitted Tokens are:
    - ```Closes```: References bug issues this commit closes upon merging
        - Can only be used with ```fix``` type
    - ```Implements```: References feature issues this commit closes upon merging
        - Can only be used with ```feat``` type
    - ```Refs```: Related issues and PRs, SHOULD NOT be used alongside ```Closes``` or ```Implements```
    - ```BREAKING-CHANGE```: Describes the breaking change, including previous and new behavior
    - ```Co-authored-by```: Lists collaborators for that commit
    - ```Format```: Format of the commit body. Can be either name or MIME-type (e.g. ```text/markdown```).
    - ```Milestone```: What type of milestone change this commit would entail. Can be either of: ```epoch```, ```major```, ```minor```, ```patch```, ```none``` (none SHALL be used for ci changes only)
    - ```Signed-off-by```: A way to signify acceptance of the Developer Certificate of Origin (DCO).
11. A footer’s token MUST use ```-``` (dashes) in place of whitespace characters, e.g., ```Co-authored-by``` (this helps differentiate the footer section from a multi-paragraph body).
12. A footer’s value MAY contain spaces and newlines, and parsing MUST terminate when the next valid footer token/separator pair is observed.
13. Breaking changes MUST be indicated in the type/scope prefix of a commit, and as an entry in the footer.
14. When included as a footer, a breaking change MUST consist of the uppercase text ```BREAKING-CHANGE```, followed by a colon, space, and description, e.g., ```BREAKING-CHANGE: environment variables now take precedence over config files```.
16. For inclusion in the type/scope prefix, breaking changes MUST be indicated by a ```!``` immediately before the ```:```.
17. Commits not conforming to this spec MAY be merged. If the commit contains a BREAKING CHANGE it MUST NOT be merged.
18. A commit MUST only have changes of one type.
19. The units of information that make up Conventional Commits MUST NOT be treated as case sensitive by implementors, with the exception of ```BREAKING-CHANGE``` which MUST be uppercase.

## Reasoning
We use automated tooling to create changelogs as well as create our releases. For that our commit messages MUST be parsable by machines. This spec is supposed to make sure they are.
As long as there is no breaking change it is not as big of a big deal if spec is not followed. Just keep in mind that your contribution will most likely not be contained in the changelog.

## Examples
### Minimal commit message
```fix: Last character of message is no longer cut off```

### Minimal commit message with scope
```fix(chat): Last character of message is no longer cut off```

### Commit message with body, issue ref and Contributor
```
fix(chat): Last character of message is no longer cut off

This is the explanation of the previous error. Also I explain what the changes do to fix the error.
- Change 1
- Change 2

Closes: #13
Co-authored-by: Max Mustermann <max.mustermann@example.com>
Milestone: patch
Format: text/markdown
```

### Commit message with breaking change
```
feat(sending)!: Messages now support more data to be sent

Messages can now be sent with all parameters allowed by the provider.

Implements: #72
BREAKING-CHANGE: Messages now no longer take json payloads as a param.
Instead the message object now exposes methods to set every parameter.
Format: text/plain
Milestone: Major
```

## Version
This is version 1.0.0 of the cis-oss commit spec.

## Attribution
This commit spec is adapted from the [Conventional Commits v1.0.0](https://www.conventionalcommits.org/en/v1.0.0) specification, licensed under [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/).

## License
This document is licensed under [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/).
