`Last update: 2021-01`

> **Modules**
>   * Core functionality
>     * [Access Provider](#access-provider) the glue for everything (Auth0).
>     * [SSO Dashboard Configuration and Access Control Database](#sso-dashboard-configuration-and-access-control-database) where access control is set at the IAM level (additionally to the site's own controls).
>     * [New Login Experience (NLX)](#new-login-experience-nlx) the login panel to login to websites.
>     * [OpenLDAP](#openldap) staff Identity Provider
>     * [DuoSecurity (2FA)](#duosecurity-2fa) staff 2FA
>   * Core APIs
>     * [CIS (Change Integration Service)](#cis-change-integration-service)
>     * [IAM User Profile](#iam-user-profile) the user profile specification.
>   * Website integration
>     * [Django OIDC](#django-oidc) to integrate your Django website with IAM.
>   * Websites
>     * [SSO Dashboard](#sso-dashboard) where you find the websites you can access.
>     * [DinoPark](#dinopark) the user profile editor.
>     * [Legacy Mozillians.org (to be replaced by DinoPark and CIS)](#legacy-mozilliansorg-to-be-replaced-by-dinopark-and-cis)
>   * [IAM Infrastructure](#iam-infrastructure) how IAM runs.
>   * [UX (User Experience)](#ux-user-experience) how everything works together from a user point of view.


# _Mozilla DRI_
Mozilla also leverage the DRI model (Directely Responsible Individual) similarly to [GitLab](https://about.gitlab.com/handbook/people-operations/directly-responsible-individuals/)
The IAM DRI is responsible for maintaining this file (module owners) and is the ultimate decision maker. The DRI is also responsible for the project's success or failure.
DRIs are responsible for drafting the high-level miletones, roadmap and resolving issues or problems.

- IAM DRI: Brian Pitts
- DinoPark DRI: Brian Pitts


# _Mozilla IAM_ Modules Owners

This document list which team or people are **responsible for making decisions** by service or component (module) of _Mozilla IAM_. This is inspired by [Mozilla's Module System](https://wiki.mozilla.org/Modules). This list is useful to expedite decisions. It does not mean that a module owner is the sole authority for the module, but it is the "go-to" person. In the module owner absence, module peers may also make decisions on behalf of the module owner.

All decisions are taken by consulting various parties of different teams in and outside of Mozilla.

**Module owners are responsible for:**

- Aligning module-level miletones and issues with the IAM roadmap milestones and objectives. The IAM roadmap milestones are set together with the module owners, the DRI and stakeholders.
- Breaking down tasks associated with miletones into sub tasks that can be worked on in a sprint.
- Making decisions about the module that align with Mozilla OKRs and technical considerations.
- Raising issues associated with OKRs, milestones, tech stack etc. to the IAM DRI.


# Default Owner

For all components below if no owner is listed, then the owner is Brian Pitts and the Web SRE / IAM team.

## UX (User Experience)

User flow, design, etc.

## Django OIDC

A Python Django module providing OpenID Connect (OIDC) support for relying parties, used by multiple sites.

- Module Owner: @johngian
- Peers: @akatsoulas

Repositories:
- https://github.com/mozilla/mozilla-django-oidc/

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

## people.mozilla.org (PMO)

This is the new place to edit _Mozilla IAM_ profiles, manage groups, search & discover people. It will be available at https://people.mozilla.org (beta at https://people.allizom.community).
Test environment is: https://dinopark.k8s.test.sso.allizom.org/ development environment is: https://dinopark.k8s.dev.sso.allizom.org

Repositories:
- https://github.com/mozilla-iam/dino-park-front-end
- https://github.com/mozilla-iam/dino-park-search
- https://github.com/mozilla-iam/dino-park-fence
- https://github.com/mozilla-iam/dino-park-fossil
- https://github.com/mozilla-iam/dino-park-lookout
- https://github.com/mozilla-iam/dino-park-tree

## vouches.mozillians.org

Site containing old mozillians.org vouches

- Owner: @HerminaC
- Operator: OI

Repository:
- https://github.com/mozilla/mozillians


## IAM Infrastructure


## OpenLDAP

This is the Staff user database, credential storage and group system (IdP). It also contains some non-staff contributors.

- Owner: @rtucker
- Peers: @gcox
- Operator: CoreServices

## DuoSecurity (2FA)

This is the 2FA/MFA product utilized to augment OpenLDAP with a second-factor.
