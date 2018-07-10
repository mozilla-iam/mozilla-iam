`Last update: 2018-07`

# _Mozilla IAM_ Program Strategy

* @jeffbryner (IT, InfoSec)
* @hmitsch (Open Innovation, ParSys)

# Mozilla IT Operating Model

* IT Capability Owner: @jeffbryner
  * IT Product Owner: @gdestuynder
    * Auth0 & Auth0 Lock & Auth0 Dashboard: @jdow @akrug @gdestuynder
       * <Question: Is `Auth0 Lock` the same as `NLX`>
    * Service Integration (CIS): @akrug
    * LDAP: @jdow
    * DuoSecurity: @gdestuynder
    
* IT Enterprise Architecture
   * @mvk-mozilla
   
* Outside-IT Capability Ownership
    * User Experience (UX): @mbranson
    * Mozillians.org: ParSys
    * WorkDay (HRIS): People Team

# Modules Owners

This document list which team or people are responsible for which component (module) of the _IAM Stack_. This is mainly useful for decision making and is inspired by [Mozilla's Module System](https://wiki.mozilla.org/Modules).

_Note:_ We don't yet know what a conflict resolution process would look like if there was a diverging opinion between the Module Owner and the IT Capability Owner for that module.

Extensions to the Mozilla Module System:
- **IT Capability Owner**: The person which is capability owner for a particular module.
- **Operator**: A person or team which is responsible for keeping the system running, generally also the
  developer in a devops model.

## CIS (Change Integration Service)

Backend which deals with IAM data integration from multiple sources.

- IT Capability Owner: @jeffbryner
- Module Owner: @akrug
- Peers: @gdestuynder
- Operator: EIS

Repositories:
- https://github.com/mozilla-iam/cis
- https://github.com/mozilla-iam/cis_functions

## Person API

API which presents and allows manipulation of CIS data. This includes a publicly available endpoint to the _IAM Stack_ (replacing the Mozillians.org API).

- IT Capability Owner: @jeffbryner
- Owner: @akrug
- Peers: @gdestuynder <can we add a ParSys Peer?>
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/person-api

## SSO Dashboard

This is the application launcher available at https://sso.mozilla.com.

- IT Capability Owner: @jeffbryner
- Owner: @akrug
- Peers: @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard

## SSO Dashboard Configuration and Access Control Database

This is the configuration and `apps.yml`.

- IT Capability Owner: @jeffbryner
- Owner: @jdow
- Peers: @akrug @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/sso-dashboard-configuration

## GSuite Community Driver

This is the G Suite Team Drive integration.

- IT Capability Owner: @jeffbryner
- Owner: @akrug
- Peers: @gdestuynder
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/gsuite-community-drive-driver

## Slack Driver

This is the driver for Slack user deprovisioning.

- IT Capability Owner: @jeffbryner
- Owner: @gdestuynder
- Peers: @akrug
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/slack-driver/

## New Login Experience (NLX)

This is the login window for _Mozilla IAM_.

- IT Capability Owner: @jeffbryner
- Owner: @hidde
- Peers: @akrug @gdestuynder <can we add a full staff member from ParSys here?>
- Operator: EIS

Repository:
- https://github.com/mozilla-iam/auth0-custom-lock

## Mozillians.org Profile and Group Management

This is the place to edit _Mozilla IAM_ profiles, manage groups, search & discover people. It is available at https://mozillians.org.

- Owner: @hmitsch
- Peers: @johngian @akatsoulas @fiji-flo <suggesting to add a InfoSec person?>
- Operator: ParSys

Repository:
- https://github.com/mozilla/mozillians

## Phonebook

This is the Staff-only accessible system to access Mozilla's org chart and Staff profiles, available at https://phonebook.mozilla.org.

- IT Capability Owner: @jeffbryner
- Owner: @akrug
- Peers: @atoll
- Operator: IT (MOC?)

Repository:
- https://github.com/mozilla/phonebook

## IAM Infrastructure

- IT Capability Owner: TBD
- Owner (accountable, decision maker): TBD
- Peers: danielh (infra) adelbarrio (monitoring&alerting) @akrug @johngian
- Operator (responsible, developer): IT (MOC?)

Repository:
- TBD (infrastructure)
- TBD (monitoring&alerting)
