---
layout: post
title:  "Security hardening Shibboleth SP"
summary: Increase your identity infrastructure's security with these tips.
date:   2023-05-09 09:34:00
categories: sp security identity infrastructure
image: /assets/images/armidillo.jpg
author: sam_jones
published: true
---

![an Armidillo](/assets/images/armidillo.jpg)
###### Photo by [Victor Miyata](https://www.pexels.com/@miyatavictor/)

## Introduction

Shibboleth Service Provider (SP) is a widely used SAML-based Single Sign-On (SSO) solution for controlling access to web applications.

Out of the box, Shibboleth SP is secure enough for most installation scenarios, thanks to the sensible defaults the developers have chosen. Security is after-all absolutely key in a login system.

However, like any other software system, some configurations of Shibboleth SP can be vulnerable to security threats, and taking the time to ensure unauthorised access is prevented is essential.

In this blog post, we will discuss some security hardening measures for your installation of Shibboleth SP.

## Cookies

Aside from any cookies your web site may use, Shibboleth SP uses one or more cookies during the authentication process, a list of which can be found [here](https://shibboleth.atlassian.net/wiki/spaces/SP3/pages/2065335663/CookieUsage).

The Shibboleth 'session' cookie is the key one to consider in most installations. It contains a pseudo-random number that uniquely identifies the authenticated session. Its behaviour is controlled by the ```<Sessions>``` stanza in the configuration file, in particular by the ```cookieProps``` property. By default the cookie is not restricted to SSL, so in many cases one can improve security by enabling "secure" cookies at this point, as described in the [documentation](https://shibboleth.atlassian.net/wiki/spaces/SP3/pages/2065334342/Sessions).

By default, Shibboleth SP checks the IP address of browsers using a particular session to reduce the chance of session hi-jacking. This behaviour is by the ```consistentAddress``` property on the ```<Sessions>``` stanza. It may be explicitly set to ```false``` in some scenarios. If it has been set, review the reason why and re-enable it if possible. Be aware that mobile devices can change their IP addresses more frequently that desktop PCs, and that with ```consistentAddress``` set to true, users of mobile devices may have to re-authenticate.

Also disabled by default is the Session Recovery cookie.

The Session Recovery cookie may be enabled in some clustering scenarios. It stores personally identifiable information within the cookie, encrypted using a key known to all the SPs in the cluster. This allows the session to move between servers without error. With regular rotation and an appropriate key length there is no security issue with this, but if it's enabled whilst not being used in a cluster it would be better to disable it.

## Data Sealer keys

If the Session Recovery cookie mentioned above is enabled, you should also have a ```DataSealer```. There are two types. If you are using the ```Static``` kind you should change to the ```Versioned``` type because the static one is only acceptable in non-production scenarios.

If you are using the ```Versioned``` type, check how frequently you are updating the Sealer key. This is generally expected to run daily but could be run more frequently depending on your exact scenario. The versioned DataSealer supports a history of keys meaning the key roll-over for this feature is seamless.

Whatever you choose be sure it **is** rotated regularly. The Session Recovery token contains personally identifiable information and historically it's been possible to decipher cryptographic keys given enough cipher text to process.


## SAML signing and encryption keys

By default, self-signed, long lived X509 certificates and keys are used in Shibboleth SP to encrypt and sign SAML messages.

It is better to have separate signing and encryption keys because this lessens the impact if either one is compromised.

Rotation of these keys is also worth considering, **however** because these keys are what make up the trust between your SP and the IdP(s) that your users are logging in with any change to these must be orchestrated with your direct partners and any federations which you are publishing via to ensure smooth running during the key roll-over.

## Admin 'API' Handlers

Shibboleth SP can be configured with some administrative HTTP endpoints configured. Some of these may disclose information that can be considered a security risk:

### The 'Status' handler

If a status handler is configured, it displays information at a given status URL (normally https://host.example.org/Shibboleth.sso/Status. Some of the information displayed might be considered sensitive, so be sure to check the ACL is also configured. By default it is set to the safe value of "127.0.0.1 ::1", for example:

```
<Handler type="Status" Location="/Status" acl="127.0.0.1 ::1" />
```

### The 'External Auth' handler

Some configurations may have enabled the ExternalAuth handler, if so there should be a ACL associated with it to limit its access to just the calling code.

```
<Handler type="ExternalAuth" Location="/ExternalAuth" acl="127.0.0.1 ::1" />
```

A ExternalAuth handler configured without a sufficiently limiting ACL is a **critical** vulnerability.

## SLO Redirect Accept List

Single Logout (SLO) is a feature that allows users to log out from all applications in a single session. Optionally it can then re-direct the user to another site. Recent versions default to restricting the destination of the redirect to the same scheme, host, and port of the server handling the request. Some earlier versions had a more permissive default.

The ```redirectLimit="exact"``` property on the ```Sessions``` configuration stanza should work in most scenarios. In more complicated scenarios options like ```"whitelist"``` and ```"host"``` can be used. ```"none"``` should be avoided.

If redirects are unrestricted the SLO feature can be used to create fake URLs for phishing emails by presenting users with an email that appears to be at your SP but then redirects users to another website hosting the phishing scam form.

## Updates

Keeping Shibboleth SP up-to-date with the latest security patches and updates is critical to maintaining its security posture. It is recommended to have a regular update schedule in place and apply any security patches as soon as possible.

Subscribe to the [Shibboleth announce](https://shibboleth.net/mailman/listinfo/announce) mailing list to receive notifications of security advisories and new versions of Shibboleth products.

## HTTP Transport TLS

Transport Layer Security (TLS) is used to secure communication between the SP the users browser. Shibboleth SP doesn't do this directly, instead it works along side a web server like Apache HTTPD or IIS.

Whilst it is possible to configure Shibboleth SP to accept SAML messages to endpoints without TLS it is strongly discouraged.

Additionally it is a good idea to test your frontend TLS configuration using a tool like [Qualys SSL Labs SSL server test](https://www.ssllabs.com/ssltest/index.html) to get a overall score for your configuration and information about any weaknesses in it.

As far as Shibboleth SP is concerned, the ```handlerSSL``` property on the ```<Sessions>``` stanza enforces the requirement for SSL transport for SAML messages. It defaults to ```true```. If it has been explicitly set to ```false``` it's worth checking why, and ensuring the transport traffic is reasonably protected.

## Header Injection Protection

In many circumstances Shibboleth SP passes additional information about a user from the assertion made by their IdP, to the web app they are accessing, using what are known as HTTP headers.

Where this is the case, care must be taken to ensure the front end web server (such as IIS or Apache Httpd) is preventing  any injection of these HTTP headers in the original request.

In Apache, explicitly ```unset``` then ```set``` any headers which you rely on as part of your authentication framework. For example:

```
RequestHeader unset X-Example-Identity-Header
RequestHeader set X-Example-Identity-Header %{source}e
```

If you are using a web application that is part Apache's environment and able to access Shibboleth session variables directly, such as PHP, then do not use headers. Headers are only needed if using IIS, or reverse-proxying over HTTP to a separate  HTTP service.

Obfuscating headers may also help but should *not be relied upon*. A header named "username" could be guessed by a random attacker, while a header named "36827390a78-username" is much harder to guess, but it is not impossible. Make sure headers are cleared when an HTTP request is received, and before set by Shibboleth SP.

## Access to Configuration Files

Access to Shibboleth SP's configuration files must be restricted to authorised users only. It is recommended to use file permissions and access control lists to ensure that only authorised users can access and modify the configuration files.

Of course access to a production server should already be carefully controlled and a server with many users is probably a poor place to host secure web services.

## Session Cache

By default Shibboleth SP uses an in-memory session cache to store user session data.

However in some scenarios a session cache based on a different ```StorageService``` may be configured. Namely either ```memcached``` or via database ```ODBC```. If an external session cache store is configured then the security of that service should also be checked because the session cache data will contain sensitive information.

Consider clustering using encrypted cookies instead of using a shared session cache.

## Conclusion

A up-to-date Shibboleth SP with a close to default configuration is very secure. However care must be taken in more complex scenarios where secure defaults are sometimes loosened to allow a specific approach. Additionally it is important to keep up to date with new versions of the software and react to security advisories as they are announced.

As always we are ready to help if you need assistance! Please [get in touch](https://www.mimoto.co.uk/contact) if you are unsure whether or not you are affected, or need help updating your solution.
