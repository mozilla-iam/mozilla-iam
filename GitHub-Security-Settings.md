# GitHub Organization and Repository Settings

This documents which settings are used for Mozilla IAM repositories, and why.
All repositories created should follow the rules established here unless otherwise stated.

See also (CONTRIBUTING.md)[CONTRIBUTING.md] for more information about contributing code to Mozilla IAM repositories. 

## mozilla-iam GitHub organization owners

The GitHub "org owners" for https://github.com/mozilla-iam/ are required to:

- Use a separate GitHub account from their main GitHub account, dedicated to org management. This account may not be used to commit code and must have 2FA enabled.
- Follow rules documented in this document.

### Teams and access control
URL: https://github.com/orgs/mozilla-iam/teams

An "org owner" may add users to teams. The teams should have a description which indicates their intended purpose.

- No user may be added to teams that will be given universal `write` access to all repository by default.
- Teams **must** be created in order to give **granular** access to repositories. In particular:
  - If a user does not merge code in a repository, the user should be in a team that is not able to merge code for that repository.

### Organization Settings
URL: https://github.com/organizations/mozilla-iam/settings

#### Security: 2FA

2FA **must** be required for all users.

#### 3rd party access, OAuth apps and GitHub Apps

All apps and 3rd party access **must** be reviewed and only allowed if all "org owners" agree. Do not add them without complete concensus from all owners, or without notification.

## mozilla-iam repository settings

NOTE: GitHub repository settings are subject to change at GitHub's discretion without warning and this file may be updated in the future as things change or evolve over time.

All settings discussed below can be viewed at: `https://github.com/mozilla-iam/REPOS_NAME_HERE/settings/` where `REPOS_NAME_HERE` is the name of the repository.
Each subsequent paragraph represents one settings section.

### Collaborators and teams

- There should be **no** "Collaborators" added to any repository. These are single users, as opposed to teams.
- Teams **must** be used to add permissions for users. Teams may have `read` or `write` permissions, but **may not** have the `admin` permissions.
- Teams such as issue managers, bots, etc. that need no write access to code may still have `write` permissions in this section, as long as the push protection is setup in the next section.

### Branches

- There should be a `master` and `production` branch setup at the minimum (see also (CONTRIBUTING.md)[CONTRIBUTING.md]).
- Branch Protection Rules **must** be set as follow (settings that are not indicated here are up to you):
  - [x] Protect this branch
  - [x] Require pull request reviews before merging
  - [x] Require signed commits
  - [x] Include administrators
  - [x] Restrict who can push to this branch
    - Include the teams which should be able to affect code (i.e. write, commit, push code)
    - Do **NOT** include the teams that may not (such as issue managers, bots, etc.)
    
  NOTE: "Restrict who can push to this branch" is effectively the control by which you may allow specific teams to write issues without being able to change code. This does not prevent these teams from contributing through pull-requests. It prevents these teams to merge code.
 
