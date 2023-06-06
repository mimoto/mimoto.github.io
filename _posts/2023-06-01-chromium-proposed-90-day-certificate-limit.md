---
layout: post
title:  "Chromium's suggested 90 day certificate limit"
summary: A positive trend to improve security will challenge traditional behaviours around server certificates.
date:   2023-06-07 11:15:00
categories: certificates
image: /assets/images/can-production-line.jpg
author: sam_jones
published: true
---

![A can production line](/assets/images/can-production-line.jpg)

###### Photo by [cottonbro studio](https://www.pexels.com/@cottonbro/)

# Introduction

In the ever-evolving landscape of Internet security it is essential for IT managers to stay updated on the latest
developments that impact their organisation's web infrastructure.

One such potential development is the reduction of TLS server certificate validity periods suggested by Chromium, the
open-source browser project behind Google Chrome.

In
a [post entitled "Moving forward together"](https://www.chromium.org/Home/chromium-security/root-ca-policy/moving-forward-together/)
they listed a series of intended changes. We're choosing to focus on just one: **"a reduction of TLS server
authentication subscriber certificate maximum validity from 398 days to 90 days."**

# Background and Context

TLS server certificates are a essential part of the system of trust that web encryption relies on.
If you visit an https site you're connection is encrypted using keys disclosed to your browser via the server's
certificate. The certificate may also have other data to help assure you that the site you've visited is the one you
expected and not a fraudulent site with malicious intent.

A group of "certificate authorities" are responsible for generating certificates in a way that makes it difficult for
nefarious types to forge them. 
If you've ever visited a website and seen a warning about "self-signed certificates" then you've seen a part of this
protection in action: self-signed certificates are certificates that have **not** been endorsed by a recognised authority
and should be treated with extreme caution.

In the early days of the technology arranging a server certificate was a manual process. A certificate request would be
generated, likely by hand, sent to a certificate authority, then after some delay a certificate would be returned. Long
certificate lifetimes reflected the administrative burden of replacing expiring certificates in order to keep encrypted
web services running.

The current certificate maximum life time of 398 days used to be higher. However there are risks associated with long
lived certificates. A compromised server will allow an attacker to acquire a server's certificate and keys and thus pass
themselves off as that server. Over time SSL protocol suites are defeated allowing attackers with enough traffic to
determine the private key without compromising the actual server. Certificate revocation lists help to address this,
though they have they also have issues.

A better security practice is automated certificate issuance, which has been available for a few years via the ACME protocol.
Because the process doesn't require manual intervention it can be run far more frequently and certificates can therefore have much
short lifespans, 7 days for example. The most famous ACME certificate authority is [Let's Encrypt](https://letsencrypt.org/)
but other certificate authorities can offer automated issuance using ACME too. You can even run your own ACME service using
software like [Smallstep](https://smallstep.com/blog/private-acme-server/), especially useful for internal, 
backend infrastructure services.

# Reasons for the change

The suggested change goes someway to reducing the impact of compromised certificates, but with a lifespan of 90 days
there would certainly still be some potential for impact. More broadly the change aims to encourage the adoption of
better security practices. It's not inconceivable that certificates are renewed every 90 days manually, but it is
certainly onerous.

Looking ahead one might well imagine if all certificates were being renewed automatically the lifetimes could be much
shorter than 90 days, which would be a big improvement.

# Implications for service owners

If you're already using automated certificate renewal, none. You've already minimised the human effort required, and
will also already be using short lived certificates thus reducing the impact of compromise.

However, if like a lot of organisations you still have a manual process for some or all of your certificate management
then expect your IT team to spend much more time dealing with certificate renewals than they do now. Additionally, this
will put more pressure on the business processes and tooling you use to track when your certificates are expiring.

On the positive side, there is a mild security benefit from the increased frequency, though not as much as can already
be attained by moving to a automated process.

# What about signing and encryption certificates for Shibboleth IdP and SP?

These are very unlikely to be affected. The suggested change appears to be aimed at the certificates a web server would
present to a web browser. The signing and encryption certificates for Shibboleth SP and IdP are used as a part of the
SAML2 protocol to allow parts of the authentication infrastructure to trust each other and are not used by a user's web
browser directly. Indeed, these certificates are not usually signed by a certificate authority because the trust is
derived from the metadata exchange. 

For most IdPs and SPs the expiry of these "trust fabric" certificates is irrelevant and
the browser is unaware of them.

# Conclusion

Chromium's suggested change may or may not come to pass. But if your organisation still has a manual process for
certificate renewal, maybe now is the time to review that.

By embracing this change and adopting robust certificate management practices you will enhance your organisation's
security posture and ensure the trustworthiness and reliability of your web services. Staying informed, planning ahead,
and using automation tools will enable your organisation to navigate the transition seamlessly and maintain a secure
service whilst avoiding increased staff time managing certificates.

Even if the suggested change does not come to pass you'll still have a much improved infrastructure and a saving in
administration time.
