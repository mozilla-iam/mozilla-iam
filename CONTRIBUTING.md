# Contributing to Mozilla IAM repositories

## Terminology
| Shortcut | Term                  | Meaning                                                                                                                            |
|----------|-----------------------|------------------------------------------------------------------------------------------------------------------------------------|
| POC      | Proof of concept      | A repository with proof of concepts, or basically anything that does not contain production code and is not yet being reviewed.    |
| PR       | Pull-Request          | A request to merge commits/code into a repository.                                                                                 |
| r+ r-    | Review granted/denied | A Mozilla shortcut to mention that a code review resulted in the acceptance or refusal of the code.                                |
| Branch   | Branch                |  A branch is a view of the repository's commit history. `master` is the development branch, `production` is the production branch. |
   
## Code quality
Code quality/review is really deep in our culture here in Mozilla and should **not** be treated as a nice to have.

### Branches
Each repository should have:
* A `master` branch that is used for development, setup in such as way that pull-requests are required to add commits. Reviews are optional for proof of concepts, but required on any repository that also has a production branch.

* An optional `staging` branch. This branch is used to test deployments only.

* A `production` branch. This branch is optional for proof of concept repositories, but otherwise required. Pull-requests and reviews are required to commit to this branch, and must be enforced by GitHub settings. PRs to the `production` branch must come from the same repository's branches (usually, from `master`).

Life of a commit:
```

 Personal       Pull-Req     mozilla-iam      Pull-Req        mozilla-iam        Pull-Req        mozilla-iam
 Fork/Repos    +--------->   master branch  +------------->   staging branch   +-------------->  production branch
                                                               (optional)
                      ^                              ^                                ^
                      |                              |                                |
                      |                              |                                |
                      + Review required   +-------------------------------------------+
                        Except POC repos
```

### Code reviews
The purpose of doing reviews is not to check if code changes work (this should be ensured by the dev before opening the PR) but rather deep dive on the implementation and to ensure that code standards/policies are met.

Here are some guidelines that we recommend to also follow:
* https://mozweb.readthedocs.io/en/latest/1


### Pull-requests (PR)

* PRs should deal with one specific issue. Several PRs should be opened when dealing with multiple issues.
* PRs should reference the issue(s) that required this PR.
* If commits for the same change are spread over several commits due to development, reviews, etc. it is acceptable to squash the commits on merge during a PR.
* An attempt to make commits reasonably atomic (one type of change per commit) should be made.
* Commit messages should be reasonably clear, for example: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
        
        
### Push

Push is only allowed for POC repos. Any repos with a `production` branch should therefore disable push to branches in the GitHub settings.
`push -f` is strongly discouraged unless absolutely necessary (even on POC repos) - and if so, forks and authors should be consulted to ensure this is the best solution.
