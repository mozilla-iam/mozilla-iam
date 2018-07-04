# Contributing to Mozilla IAM repositories

This file is maintained at https://github.com/mozilla-iam/mozilla-iam/blob/master/CONTRIBUTING.md

## Terminology
| Shortcut | Term                  | Meaning                                                                                                                            |
|----------|-----------------------|------------------------------------------------------------------------------------------------------------------------------------|
| POC      | Proof of concept      | A repository with proof of concepts, or basically anything that does not contain production code and is not yet being reviewed.    |
| PR       | Pull-Request          | A request to merge commits/code into a repository.                                                                                 |
| r+ r-    | Review granted/denied | A Mozilla shortcut to mention that a code review resulted in the acceptance or refusal of the code.                                |
| Branch   | Branch                | A branch is a view of the repository's commit history. `master` is the development branch, `production` is the production branch.  |
| Tag      | Tag                   | A tag is a known point in the repository's commit history. It's used to mark specific releases.                                    |

See also [GLOSSARY.md](GLOSSARY.md) for more definitions.

## Principles

All IAM repositories should follow these working agreements and include:

1. A master branch which is tagged for releases.
2. The settings documented in [GitHub-Security-Settings.md](GitHub-Security-Settings.md) are set for all repositories.
3. Code contains some level of unit testing.
4. Testing includes a linter or syntax analyzer such as `flake8`
5. A README which indicates the project's purpose and a diagram of functionment.
6. The code can always be tested locally without any credentials.
7. Use `makefiles` with clear targets to build, run, deploy the code.
8. No un-reviewed code may go to production.
9. Code is developed on personal forks and merged back to the repositories under <https://github.com/mozilla-iam> or
  <https://github.com/mozilla>.
10. New design or large functionality changes must go through an
  [RRA](https://infosec.mozilla.org/guidelines/risk/rapid_risk_assessment.html).
11. Pentests should be run periodically for high risk projects.

### Branches, tags, and pull-requests

* The `master` branch is used for development, and tags are created to mark point in time releases. These releases may
  be promoted to a production deploy.

* Additional branches may be created (including a `production` branch, but these should serve as a way to work on a
project with multiple people, not as personal branches. Use your own fork of the project for personal work or feature
you work on alone. If this changes, you can always push the personal branch to the upstream repository).

* Proof of concepts do not require review, unless they're promoted to production code.

Life of a commit:
```

 Personal       Pull-Req     mozilla-iam      Tag
 Fork/Repos    +--------->   master branch  +----------> version 1.0
                      ^                              ^
                      |                              |
                      |                              |
                      + Review required   +----------+
                        Except POC or configuration repos
```

This is the recommended way to setup your local fork:

#### Manually
```
# Fork the project on github first!
$ git clone git@github.com:your-name-here/mozilla-iam.git
$ cd mozilla-iam
$ git remote add upstream https://github.com/mozilla-iam/mozilla-iam
$ git branch -u master upstream/master # Tracks upstream in case it changes
```

#### Automatically
```
$ git clone https://github.com/mozilla-iam/mozilla-iam
$ cd mozilla-iam
$ hub fork
# Note that here, `origin` is upstream, and the remote with your github username is your fork
```

To update:
```
$ git pull -r upstream master
# Or
$ git pull -r your-name-here master
# Note that `-r` will rebase your local changes on top of upstream if you have any
# To avoid having to do so you can also just always work on a local branch
```

### Code reviews

* Always check the guidelines from this document are met, i.e. that principles are followed (is there any unit test? is
  there documentation? etc.)
* Look at the code flow and attempt to find any logical errors. You do not need to verify the code will run, but instead
  if there are any high level issue, or things the developer did not think of.

See also: <https://mozweb.readthedocs.io> for a longer read on good practices.
