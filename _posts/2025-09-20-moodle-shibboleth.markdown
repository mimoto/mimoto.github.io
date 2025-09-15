---
layout: post
title: "Shibboleth IdP with Moodle as a backend user store"
summary: "An unsual way of combining two popular higher education software platforms"
date: 2025-09-15 10:00:00
categories: identity infrastructure
image: /assets/images/cyber-essentials.png
author: sam_jones
published: false
---

![Cyber Essentials](/assets/images/cyber-essentials.png)

# Shibboleth IdP with Moodle as a backend user store

Shibboleth IdP and Moodle are both very common software tools used by higher education institutions. Shibboleth IdP is an excellent authentication and identity server and Moodle is a popular virtual learning environment.

Moodle already has support for SAML2 using a module, which allows the Moodle to be a SP or an IdP. So for institutions that already have Shibboleth IdP as their login service it is easy to configure single sign on access to Moodle by setting it up as a SP using the SAML2 module. Then, access to Moodle can be granted to your the users in your normal credential store; which is normally an LDAP server.

One can also use the Moodle SAML2 module to make the Moodle into an IdP, which allows you to provide access to other SAML2 resources for the users in Moodle via the Moodle login.

An LDAP credential store, with Shibboleth IdP providing login, and learning resources in Moodle is great. But for those who already have a Moodle, and merely want to add a small number of federated services to the larger offering, then adding a LDAP and associated IDAM infrastructure might be overly onerous.

On the other hand, the Moodle SAML2 module in IdP mode seems **TODO** ...

So another solution we found was to integrate Shibboleth IdP with the Moodle credential store directly allowing a more configurable SAML2 IdP whilst not requiring a full IDAM instructure and associated overhead.

## Why this is useful

If you already have a Moodle with your learning content in it, but you want to provide access to one or more federated resources then Shibboleth IdP can handle the federated and SAML2 login for those resources. Whilst it is also possible to do this with Moodle in IdP mode, doing so makes Moodle a single point of failure for your infrastructure. As it only requires read access, Shibboleth IdP can be run against a replicated copy of the Moodle DB making it easier to seperate these two piece of infrasturcture so that a failure or maintenance on one does not affect the other. Similarly, system load from logins is seperated away from the Moodle system somewhat reducing pressure on resources for that system.

User management, either by admin or self-service, can still be done using the Moodle interface as before so no extra infrasture is required for IAM tasks and no staff re-training or different student support is required for this.

This approach can also be made to work with the 2fa support in Moodle, via the TOTP module in Shibboleth IdP. Shibboleth IdP is more flexible with regards to MFA behaviours for different federated services than the native offering.
