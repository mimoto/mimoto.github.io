---
layout: post
title:  "Password policies: myths and tips"
date:   2017-09-22 14:30:00 +0100
author: sam_jones
summary: The father of the password policy that many people are forced to use now regrets the advice he's given
categories: passwords
---

You may have seen the [news](https://www.wsj.com/articles/the-man-who-wrote-those-password-rules-has-a-new-tip-n3v-r-m1-d-1502124118) a few weeks ago that the father of the password policy that many people are forced to use now regrets the advice he's given. You're probably familiar with this style of policy:

* At least 1 capital letter
* At least 1 lower case letter
* At least 1 symbol
* At least 1 digit
* Changed every 3 months
* At least 8 characters long

It's a style that's frustrating for users, and it doesn't improve security. 

![](/assets/images/waterfall_and_rock.jpg)

# Tips

Passwords are a far-from-ideal way to authenticate users, but they're not going away anytime soon. So in the meantime here are our tips for helping your staff or customers use passwords more effectively:

## 1) Use a single sign on (SSO) service, and integrate it with as many of your services as you can.

Most policies tell users to set different passwords for different systems, and in most cases users ignore this advice (often understandably: remembering lots of things is difficult). You can help solve this by getting a Single Sign On system - doing so vastly reduces the number of passwords your users will be pretending to remember, and also reduces the risk that your users' credentials will be discovered through a data breach because they will be stored in fewer places.

## 2) Require a second factor (which isn't a second password) to access key services

No matter what infrastructure is in place, or what password policy is being enforced, passwords will always be weak, because humans can easily be tricked into handing over their password. It's a good idea to protect your key services with a second layer of security, but avoid simply adding a second level of password checks. Also be very wary of implementing another level of security that can be set using the first (for example, a second password that can be changed using your primary username and password, or a phone-based call-out or SMS message to a phone that can be setup using your primary credentials).

## 3) Passphrases are better than passwords

Encourage your users to use passphrases rather than passwords. As the name suggests, in a passphrase you choose a memorable series of words that you keep secret. Humans are good at remembering a sequence of words and how to spell those words. By using passphrases your users will comfortably generate secrets that are 20 characters or more. In general the longer a password is the harder it is for a computer to crack, or for someone to work out by watching someone type it.

## 4) Avoid storing your users passwords

Storing passwords in clear text is simply irresponsible, storing them with reversible encryption is still very vulnerable, and even one-way hashing done poorly can be a significant risk. This is a another reason to use an SSO system: if there are lots of systems handling and storing passwords then the approaches some of them use will be weak. Your infrastructure is only as strong as it's weakest link in this regard.

If your organisation needs help with password management, getting a SSO system in place, or integrating your existing SSO system with a new service, then [we'd be happy to help](/contact/)
