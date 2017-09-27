# Problem

Identity and Access Management (IAM) at Mozilla is often implemented through various mechanisms: SSO, LDAP backend, Bugzilla authentication, GitHub, etc. some of which we control, some of which we don’t.

- Access requires multiple credentials and getting access to the right services is complicated.
- Finding out who’s eligible to grant or deny the access is hard.
- Curating accesses is simply not done and sometimes not a possibility.
- Off-boarding takes a team of people and several hours to revoke all accesses, some revocations are forgotten or missed.
- On-boarding is fully manual, and several round-trips of support tickets are necessary until a new hire is fully setup. This takes several days during which the new hire cannot function properly.

It is difficult for services owners and developers to get proper authentication, many of them thus revert to using the VPN or HTTP Basic Authentication - which do not provide fine grained control and provide a poor user experience. Many of these controls also do not allow the community to participate, in which case project owners simply function outside of Mozilla entirely.

Finally, for users logging into services, it is also painful. Sessions end quickly and it’s necessary to re-login several times a day. Many credentials have to be remembered. Asking for access takes a long time and several attempts until successful. It is unclear what accounts you have to hold as a Mozillian.

All of these problems cause our IAM to be unsafe and time consuming.

# Solution

We have created an IAM function and the IAM product to improve all of the issues. It provides a consistent user interface (mozillians.org),  lowers the amount of access management effort, and makes integration with services easy and flexible.

Additionally, our IAM use the same system for corporation employees and community alike, where employees simply have an additional flag that indicate their employment status.

This is done through a single, centralized identification system (Auth0) and a unified authentication layer (UAL, currently provided by various proxying software) supporting several mechanisms (SAML, OIDC, LDAP, REST API, etc.).

# Our quote
> “I have way too much access because it was easier that way. My account can change Firefox code and ship it to our users without anyone else's involvement. Did you know that?”

# How to get started

This is a long term project. We started by consolidating our data sources (list of employees, teams, etc.) and inventorying all authentication systems.

We have then decided, in 2016Q3, to use a central provider for assertions and tokens (Auth0) and use proxies (mod_mellon, etc.) for the different authentication mechanisms.

Switching over for service owners will be as seamless as possible. If they used SAML, it will still be SAML, just a different backend. LDAP will remain unchanged. New customers can also use OIDC. Little change is expected on their part.

# Customer quote
> “Why do I have to re-authenticate every time I close my browser or my laptop? This is madness…”
