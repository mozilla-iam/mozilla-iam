# mozilla-iam

# Vision
> All Mozillians (paid staff and contributors) have convenient and appropriate access to Mozilla services through a unified, authoritative, integrated identity system that empowers them to build a better Internet

# Summary
Mozilla’s Identity and Access Management (IAM) aim to improve the productivity of Mozillians (end-users and operational teams) by streamlining IAM management tasks while providing visibility.
Additionally, IAM provides an easier and significantly safer experience for the user and for services in need of authentication.

See also the [press statement](Press.md) (this is not a real press-statement, it is an exercise to kick-start projects).


![Diagram](/imgs/diagram.png?raw=true "High-level diagram")

# Technical and detailed diagrams

![Diagram](/imgs/tech_diagram.png?raw=true "Technical diagram")

- [Technical Diagram 2017 (old)](imgs/technical_architecture_diagram.png?raw=true) High-level technical diagram of
  the different Mozilla IAM components and their interactions from 2017's IAM implementation.
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

## Authentication Assurance

Mozilla IAM uses various indicators in order to figure out if a user should have access to a relying party. AAI
(Authentication Assurance Indicators) are generated for the user who's authenticating. These could be indicators that a
user has used a 2FA device (with different strength of authentication), that their geo-location changed, that their
identity provider performed additional authentication checks, that they've logged in before with the same machine, that
their machine's software is up to date, etc.

These AAIs are ranked and used to determine an AAL (Authentication Assurance Level) for that iteration of the
authencation of the user. The AAL is re-calculated each time a user authenticates as the indicators may have
changed. A map of AAI to AAL can be found in our [well-known endpoint](https://auth.mozilla.com/.well-known/mozilla-iam).

The AALs are ranked using the [Mozilla Standard Levels](https://infosec.mozilla.org/guidelines/risk/standard_levels),
i.e. `LOW/MEDIUM/HIGH/MAXIMUM`. The AAL is used to determine if a user should be granted access per relying party.

For example, if `AAL=LOW`, the user may be able to chat on Discourse, but have no administrative capabilities (which may
require `AAL=HIGH`). See also the diagram below illustrating this use case.

NOTE: The default for all relying parties is to require `AAL=MEDIUM`. An example of a relying party allowing `AAL=LOW` would
be https://discourse.mozilla-community.org/ or https://voice.mozilla.org/

![authenticationassurance](/imgs/aal_diagram.png?raw=true "Authentication Assurance diagram")

# Links and information
## Internal links
- [Mozilla internal "mana" page](https://mana.mozilla.org/wiki/display/SECURITY/IAM) This contains some internal processes and some legacy documentation.
- [GDrive (Team Drive)](https://drive.google.com/drive/folders/0ALdo9L7TEaCgUk9PVA) This contains internal research docs and meeting notes.
- [Roadmap](https://app.productplan.com/p/qrTbDMF8xQq2GdunpfIc0oc317UrR8K9)
- [Decision making](DECISION-MAKING.md) Who's responsible for ultimately making decisions and who's accountable for these.
- [Decision log](https://docs.google.com/spreadsheets/d/1QqJBLg6tTMUj_8VyPMEZOdsiumSzAwdZ-J-SpJsaEqs/edit#gid=0) A log of past decisions that seemed important.
- [CONTRIBUTING](CONTRIBUTING.md) A list of principles that we go by when participating to the Mozilla IAM project.
  - [GitHub Security Settings](GitHub-Security-Settings.md) How our repositories are setup in GitHub, and why.
- [GLOSSARY](GLOSSARY.md) A list of terms that are commonly used in this project, with their definition or explanation.
- [Auth0 and IAM metrics dashboard](https://biff-5adb6e55.influxcloud.net/d/HuRNN_1Zk/iam-engagement?orgId=1) A dashboard with statistics about Auth0 usage and people.mozilla.org engagement. Note that the access is limited to Mozilla employees.

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
