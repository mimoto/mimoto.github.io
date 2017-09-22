---
layout: post
title:  "Password policies: myths and tips"
date:   2017-09-22 14:30:00 +0100
author: sam_jones
categories: passwords
---

It's been a busy time here at Mimoto working on new products and supporting our clients' SAML and identity needs, but we thought we'd take some time out to talk here about password policies.

You may have seen in the [news](https://www.wsj.com/articles/the-man-who-wrote-those-password-rules-has-a-new-tip-n3v-r-m1-d-1502124118) a few weeks ago that the father of the policy most people are forced to use has said he regrets the advice he's given. Your probably familiar with this style of policy:
* At least 1 capital letter
* At least 1 lower case letter
* At least 1 symbol
* At least 1 digit
* Changed every 3 months
* At least 8 characters long

It's a style that's frustrating for users, and it doesn't improve security. 


![](/assets/images/waterfall_and_rock.jpg)

# Tips

Passwords are a non-ideal answer to Internet security, but they're not going away anytime soon so in the meantime hereare our tips:

## 1) Get a single sign on solution, integrate it with as many of your services as you can.

Most policies tell users to set different passwords for different systems, and in most cases users ignore this advice (often understanably: remembering lots of things is hard). You can solve help solve this by getting a Single Sign On system, doing so vastly reduces the number of passwords your users will be pretending to remember, and also reduces the risk that your users' credentials will be discovered through a data breach because they will be stored in fewer places.

## 2) Use a second factor (which isn't a second password) to protect key services

No matter what infrastructure is in place, or what password policy is being enforced, passwords will always be weak. At the least because humans can easily be convinced to hand over their password. It's a good idea to protect your key services with a second layer of security but avoid simply adding a second level of password. Be very wary of implementing a second level of security that can be set using the first (eg: a second password that can be changed using your primary username and password, or a phone based call out where the phone can be setup using your primary credentials).

## 3) Passphrases are better than passwords

Encourage your users to use passphrases rather than passwords. As the name suggests, in a passphrase you choose a memorable series of words that you keep secret. Humans are good at remembering a sequence of words and how to spell those words. By using pass phrases your users will comfortably generate secrets that are 20 characters or more. In general the longer a password is the harder it is for a computer to crack, or for someone to work out by watching someone type it.

## 4) Don't store passwords

Storing passwords in clear text is straight irresponsible, storing them with reversible encrypting is still very dangerous, even hashing done poorly can be a risk. This is a another reason to use a SSO system, if there are lots of systems handling and storing passwords then the approaches some of them use will be weak. Your infrastructure is only as strong as it's weakest link in this regard.


If your oranisation needs help with password managment, getting a SSO system in place, or integrating your existing SSO system with a service you do not yet have working with your SSO system: [we'd be happy to help](/contact/)
