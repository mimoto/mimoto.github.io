---
layout: post
title:  "Duo iframe retirement: a warning to Shibboleth IdPv3 and some IdPv4 operators"
summary: Update now or your login system will break
date:   2023-04-28 14:41:00
categories: idp mfa
image: /assets/images/machine-gear.jpg
author: sam_jones
published: true
---

![a old machine](/assets/images/machine-gear.jpg)
###### Title photo: [Markus Spiske](https://www.pexels.com/@markusspiske/)

## A warning

**Using Duo for MFA with IdPv3? You should expect your MFA to stop working March 2024!**

**Using Duo for MFA with IdPv4? Check you are using the using the OIDC method for Duo and not the iframe. The iframe will stop working in March 2024!**

## Background

This week the Shibboleth development team announced a tentative plan to remove the Duo v2 WebSDK feature from IdPv5. Shibboleth IdPv5 is expected to be released this year, and given the termination date for Duo v2 WebSDK (30th March 2024) it's easy to see why they are proposing to drop it (at the time of
writing, it is *just* a proposal).

However, the announcement made us think it was worth amplifying the message to operators of older IdPs who may not be aware they face a completely broken MFA scenario next year if they do nothing.

In 2020, [Duo announced they would retire their iframe based 2FA approach](https://duo.com/blog/breaking-up-with-the-iframe-introducing-our-new-developer-tooling), and move to provide the same functionality via OIDC and WebSDK. Since then, they have [announced 30th March 2024](https://help.duo.com/s/article/7839?language=en_US) as the end-of-life milestone for Duo web v2 SDK.

The Duo v2 WebSDK has been widely used by IdPv3 operators to provide an extra layer of security to their authentication process.

Shibboleth IdPv4 had been available for less than a year at the time Duo announced the plan to retire the iframe approach, so those installs would also have been using the WebSDK approach.

Since then, IdPv3 has gone out of support and IdPv4 has gained support for the new Duo authentication mechanisms via plugins.

## How can you tell if you are using the iframe approach?

A simple way to tell is to go through your login process in a way that triggers Duo MFA. When you reach the Duo part of the process, look at the page: does the Duo prompt appear within a small box on the page with institution specify styling on the rest of the page? If so you're using the Duo v2 WebSDK and must take action.

You can also look at the URL bar of the browser: does the URL point at your login service, or is it pointing to a duo.com address? If it's pointing at your login service whilst displaying the Duo MFA prompt, you using the old approach and must take action.

## What should you do if you are affected?

First, if you're using IdPv3 or IdPv4.0 you **must** upgrade to IdPv4.1+ . IdPv3 has been out of support for some time so this upgrade should be seen as a necessary part of maintaining a secure authentication system, regardless of Duo v2 WebSDK.

If you're using IdPv4.1+, you must use the [DuoOIDC plugin](https://shibboleth.atlassian.net/wiki/spaces/IDPPLUGINS/pages/1374027959/DuoOIDCAuthnConfiguration). Be sure to use the OIDC plugin and **not** to use the native DuoAuthnConfiguration described [here](https://shibboleth.atlassian.net/wiki/spaces/IDP4/pages/1265631604/DuoAuthnConfiguration).

We can help! Please [get in touch](https://www.mimoto.co.uk/contact) if you are unsure whether or not you are affected, or need help updating your solution.
