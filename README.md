# mozilla-iam

# Vision
> All Mozillians (paid staff and contributors) have convenient and appropriate access to Mozilla services through a unified, authoritative, integrated identity system that empowers them to build a better Internet

# Summary
Mozilla’s Identity and Access Management (IAM) efforts improvements productivity of Mozillians (end-users and operational teams) by streamlining IAM management tasks while providing visibility.
Additionally, IAM provides an easier and significantly safer experience for the user and for services in need of authentication.

See also the [press statement](Press.md) (this is not a real press-statement, it is an exercise to kick-start projects).


![Diagram](/imgs/diagram.png?raw=true "High-level diagram")

# Diagrams

- [Technical Diagram of Mozilla IAM](imgs/technical_architecture_diagram.png?raw=true) High-level technical diagram of
  the different Mozilla IAM components and their interactions. It has more technical details.
- [Login flows](imgs/login_flows.png?raw=true) shows how login and account verification work from a visual, high level
  point of
  view.


# Concepts

## 2 Stage Access validation

Mozilla IAM validates identity using one or more factors. It also validates authorization, or access, using one or
more authorization stages.
The common case is a user account's access being verified by the access provider at a high-level using broad groups or
roles. The RP (Relying Party) will then perform the same or/and additional verification, which may allow specific access within the
application.

Ex: A reviewer may have a 'Staff' role and is granted access at the first stage verification. The reviewer then gets access
to the reviewer features in the application, access which is granted by the 2nd stage verification (i.e. RP
verification).

![2stages](/imgs/2stageaccess.png?raw=true "2 Stages Access Diagram")

## Automatic expiration of access

Mozilla IAM records a timestamp of the last successful login to any RP (Relying Party) during the user's login. The
timestamp is tied to the RP.
With this, Mozilla IAM is able to tell the date at which an RP was last accessed by a user.
Automatic expiration of access is the method by which Mozilla IAM use the timestamp to decide if the user should
retain access, regardless of any other access control mechanism. If the timestamp is older than a certain amount of time
(such as 6 month), then the access will be denied and the user will have to ask for the access to be re-enabled.

This method is useful in environments where group-based or role-based access cannot always be well managed, and where
keeping track of which group gives access where, what user should have access is difficult. In other word, this method
implements a logic of "use it or lose it" automatically.

Note: The access validation occurs as part of the "2 Stage Access validation" concept and is not meant as a replacement for group-based and role-based access control.

![expirationofaccess](/imgs/expirationofaccess.png?raw=true "Expiration of access diagram")

# Links and information
## Internal links
- [Mozilla internal "mana" page](https://mana.mozilla.org/wiki/display/SECURITY/IAM)
- [GDrive (Team Drive)](https://drive.google.com/drive/folders/0ALdo9L7TEaCgUk9PVA)
- [Decision log](https://docs.google.com/spreadsheets/d/1QqJBLg6tTMUj_8VyPMEZOdsiumSzAwdZ-J-SpJsaEqs/edit#gid=0)
- [Roadmap](https://app.productplan.com/p/WZ5WEuTxpjVjxuPQ2IvlCys0WnXZVSJ2)

## Discussion
- Discourse public, main board: https://discourse.mozilla-community.org/c/iam (iam@mozilla-community.org)
- Discourse MOZILLA CONFIDENTIAL board: https://discourse.mozilla-community.org/c/iam/internal (iam+internal@mozilla-community.org) - only use when strictly necessary
- Slack: https://mozilla.slack.com/messages/G606LM42Y/
- Slack automated messages/bots/statuses: https://mozilla.slack.com/messages/G92LX4J3T/

## About the GitHub organization setup
This organization has been created to hold IAM-related public repositories. These repositories are public.
This organization follows https://mana.mozilla.org/wiki/display/POLICIES/Standard%3A+GitHub+repositories+and+organizations
Access control needs to be tigher than on https://www.github.com/mozilla/ (main Mozilla GitHub organization) warranting it's separation.

## About this repository
This repository tracks all issues that do not have a GitHub repository assigned (such as non-code, code without repo, etc.)

## Contact
For more information, please contact Mozilla Infosec (https://infosec.mozilla.org/) or the Open Innovation Team (https://wiki.mozilla.org/Innovation).
