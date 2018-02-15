# mozilla-iam

# Vision
> All Mozillians (paid staff and contributors) have convenient and appropriate access to Mozilla services through a unified, authoritative, integrated identity system that empowers them to build a better Internet

# Summary
Mozilla’s Identity and Access Management (IAM) efforts improvements productivity of Mozillians (end-users and operational teams) by streamlining IAM management tasks while providing visibility.
Additionally, IAM provides an easier and significantly safer experience for the user and for services in need of authentication.

See also the [press statement](Press.md) (this is not a real press-statement, it is an exercise to kick-start projects).


![Diagram](/imgs/diagram.png?raw=true "High-level diagram")

# Concepts

## 2 Stage Access validation

Mozilla IAM validates identity using one or more factors. It also validates authorization, or access using at one or
more authorization stages.
The common case is a user account access behind verified by the access provider at a high-level using broad groups or
roles. The RP (Relying Party) will then perform the same or/and additional verification, which may allow specific access within the
application.

Ex: A reviewer may have a 'Staff' role and granted access at the first stage verification. The reviewer then gets access
to the reviewer features in the application, an access which is granted by the 2nd stage verification (i.e. RP
verification).

![2stages](/imgs/2stageaccess.png?raw=true "2 Stages Access Diagram")

# Links and information
## Internal links
- [Mozilla internal "mana" page](https://mana.mozilla.org/wiki/display/SECURITY/IAM)
- [GDrive](https://drive.google.com/drive/folders/0BxL62r-99fkxYU92VnlHRlMyYkU)
- [Decision log](https://docs.google.com/spreadsheets/d/1QqJBLg6tTMUj_8VyPMEZOdsiumSzAwdZ-J-SpJsaEqs/edit#gid=0)
- [Roadmap](https://app.productplan.com/xonua5Ar)

## Discussion
- Discourse public, main board: https://discourse.mozilla-community.org/c/iam (iam@mozilla-community.org)
- Discourse STAFF CONFIDENTIAL board: https://discourse.mozilla-community.org/c/iam/internal (iam+internal@mozilla-community.org) - only use when strictly necessary
- Slack: https://mozilla.slack.com/messages/G606LM42Y/
- Slack automated messages/bots/statuses: https://mozilla.slack.com/messages/G92LX4J3T/

## About the GitHub organization setup
This organization has been created to hold IAM-related public repositories. These repositories are public.
This organization follows https://mana.mozilla.org/wiki/display/POLICIES/Standard%3A+GitHub+repositories+and+organizations
Access control needs to be tigher than on https://www.github.com/mozilla/ (main Mozilla GitHub organization) warranting it's separation.

## About this repository
This repository tracks all issues that do not have a GitHub repository assigned (such as non-code, code without repo, etc.)

## Contact
For more information, please contact Mozilla Infosec: https://infosec.mozilla.org/
