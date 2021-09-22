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

# Components

>   * Core functionality
>     * [Access Provider](#access-provider) the glue for everything (Auth0).
>     * [SSO Dashboard Configuration and Access Control Database](#sso-dashboard-configuration-and-access-control-database) where access control is set at the IAM level (additionally to the site's own controls).
>     * [New Login Experience (NLX)](#new-login-experience-nlx) the login panel to login to websites.
>     * [OpenLDAP](#openldap) staff Identity Provider
>     * [DuoSecurity (2FA)](#duosecurity-2fa) staff 2FA
>   * Core APIs
>     * [CIS (Change Integration Service)](#cis-change-integration-service)
>     * [IAM User Profile](#iam-user-profile) the user profile specification.
>   * Websites
>     * [SSO Dashboard](#sso-dashboard) where you find the websites you can access.
>     * [People.mozilla.org / DinoPark](#people.mozilla.org) the user profile editor.
>   * [IAM Infrastructure](#iam-infrastructure) how IAM runs.


## CIS (Change Integration Service)

Backend which deals with IAM data integration from multiple sources and provides various APIs to CIS (PersonAPI, Change/Person endpoints, well-known endpoint). This includes signing, authorization, profile storage model, publishing code and drivers.

Repositories:
- https://github.com/mozilla-iam/cis
- https://github.com/mozilla-iam/cis_functions
- https://github.com/mozilla-iam/person-api
- https://github.com/mozilla-iam/gsuite-community-drive-driver
- https://github.com/mozilla-iam/slack-driver/


## IAM User Profile

The IAM user profile utilize by CIS and other modules. It also presents the schema and profile rules on the well-known endpoints.

## Access Provider

Provides OIDC, SAML, WS-FED, etc. connectivity and IdP shadowing for the purpose of providing identity and access management to relying parties. Currently utilizes Auth0 to perform this function. This includes all auth0 related CI, configuration and rule engine.

- Operator: Third party (Auth0)

Repositories:
- https://github.com/mozilla-iam/auth0-ci/
- https://github.com/mozilla-iam/auth0-deploy
- https://github.com/mozilla-iam/authzerolib

## SSO Dashboard

This is the application launcher available at https://sso.mozilla.com.

Repository:
- https://github.com/mozilla-iam/sso-dashboard

## SSO Dashboard Configuration and Access Control Database

This is the configuration and `apps.yml`.

Repository:
- https://github.com/mozilla-iam/sso-dashboard-configuration

## New Login Experience (NLX)

This is the login window for _Mozilla IAM_.

Repository:
- https://github.com/mozilla-iam/auth0-custom-lock

## people.mozilla.org

This is the new place to edit _Mozilla IAM_ profiles, manage groups, search & discover people. It will be available at https://people.mozilla.org (beta at https://people.allizom.community).
Test environment is: https://dinopark.k8s.test.sso.allizom.org/ development environment is: https://dinopark.k8s.dev.sso.allizom.org

Repositories:
The full list of repositories and what they contain can be found at https://github.com/mozilla-iam/dino-park/blob/master/Introduction.md#repositories


## vouches.mozillians.org

Site containing old mozillians.org vouches

Repository:
- https://github.com/mozilla/mozillians


## IAM Infrastructure

The AWS resources used for running many components of IAM.


## OpenLDAP

This is the Staff user database, credential storage and group system (IdP). It also contains some non-staff contributors.

## DuoSecurity (2FA)

This is the 2FA/MFA product utilized to augment OpenLDAP with a second-factor.

- Operator: Third party (Duo) 


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

## Mozilla-IAM SLA
Response time (triaging issues and PRs) varies between repositories, with the following repositories being identified as "crucial" which means we will do our best to stay on top of:
- [mozilla-aws-cli](https://github.com/mozilla-iam/mozilla-aws-cli)
- [federated-aws-rp](https://github.com/mozilla-iam/federated-aws-rp)
- [auth0-custom-lock](https://github.com/mozilla-iam/auth0-custom-lock)
- [sso-dashboard](https://github.com/mozilla-iam/sso-dashboard)
- [sso-dashboard-configuration](https://github.com/mozilla-iam/sso-dashboard-configuration)
- [auth0-ci](https://github.com/mozilla-iam/auth0-ci)
- [auth0-deploy](https://github.com/mozilla-iam/auth0-deploy)
- [cis](https://github.com/mozilla-iam/cis)

## About this repository
This repository tracks all issues that do not have a GitHub repository assigned (such as non-code, code without repo, etc.)

## Contact
For more information, please contact Mozilla Infosec (https://infosec.mozilla.org/) or the Open Innovation Team (https://wiki.mozilla.org/Innovation).
