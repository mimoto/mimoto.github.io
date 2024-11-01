---
layout: post
title: "Cyber Essentials"
summary: "Thoughts on IT Security and the Cyber Essentials scheme"
date: 2024-03-11 10:00:00
categories: security
image: /assets/images/cyber-essentials.png
author: sam_jones
published: false
---

![Cyber Essentials](/assets/images/cyber-essentials.png)

# Cyber Essentials

Recently Mimoto gained the UK Government's Cyber Essentials certification. We thought we'd take this opportunity to reflect on the certification process and the Cyber Essentials scheme.

## TL;DR

Over the last 10 years or so, there has been an acceleration of cyber attacks on organizations and individuals. The news is littered with stories of costly attacks on organizations and individuals privacy being compromised. The average standard of IT security needs to improve, Cyber Essentials is a catalyst for that change, and in our opinion: it's helping.

As a national initiative, it has a very broad audience, and it clearly tries to accommodate the whole range of organizations in that audience, but in some instances it feels awkward. It feels like the scheme is designed for a medium sized enterprise, based around a central office, using Microsoft based infrastructure, with limited cloud adoption. However, it often feels clumsy for very large or very small organizations, or for fully cloud based or non Microsoft based ones.

That said, the free insurance it offers to qualifying small organizations is a nice initiative.

At Mimoto we do a lot of work with federated identity, and in our opinion whilst CE is aware of federated identity, it phrases some questions in a way that make it impossible to answer them positively whilst using federated identity. This is clearly counter it's main improving IT security mission.

## Cyber Essentials: encouraging change

One strong aspect of the scheme: it's name is excellent, picture this conversation between a supplier and a potential customer:

```
Customer: "Is the IT infrastructure your service depends on secure?"

Supplier: "Oh! Yes! Our IT infrastructure's security is second to none! We use world leading technologies inline with best practice to provide a impenetrable system that will keep you and your users safe!"

Customer: "Do you have the Cyber Essentials certification?"

Supplier: ".... no?"
```

To be clear, it's certainly possible to run a secure infrastructure without having Cyber Essentials. But for the supplier in the example it's important to be able to answer the "Do you meet Cyber Essentials?" question affirmatively, because if they can't manage Cyber *Essentials* how can anything they offer be secure?

Increasingly UK public sector procurement teams and frameworks ask about Cyber Essentials. If you sell an IT services to the UK, it's becoming very important to have Cyber Essentials.

Another lever that the Cyber Essentials scheme is using the foster adoption: a Cyber Essentials organization only maintains that certification if all the suppliers on which it depends also meet Cyber Essentials. This requirement means that, similar to a virus, Cyber Essentials can spread from organization to organization, following the matrix of organizational links and dependencies that exist, at least in theory.

It's not a free certification, and it's price is set by the size of the organization applying for it. As well as the cost of the certification, which is yearly, there is a myriad of organizations offering to prepare & help organizations with their certification. At the time of writing IASME charge around £300 for the smallest organizations (less than 10 employees), and around £600 for the largest (250+ employees).

It's not an expensive certification, but the costs do not seem proportionate. Very few large organizations will struggle to justify £600/year for a scheme like this, but some one person organizations will find £300/year difficult to swallow.

However, if a small organization does go ahead, and manages to get a Cyber Essentials certificate that covers their whole organization, then they can also take up the free cyber incident insurance on offer. A nice touch.

## Who's the audience?

The UK Government states: "Cyber Essentials is suitable for all organizations, of any size, in any sector.". It's audience is vast and diverse.

Cyber Essentials is not a new scheme, it celebrated it's 10 year anniversary on the 23rd of October 2024. So, perhaps that's why at times it feels like it's been written with a particular kind of organization in mind:

* A medium sized organization of 50 to 200 people
* A office based organization, perhaps with satellite offices
* Traditional Microsoft infrastructure
* A clear Internet perimeter

To be clear, we're not suggesting it's impossible for an organization that isn't like the one above to get Cyber Essentials. Mimoto is exactly unlike the organization I describe above, but we still got the Cyber Essentials certificate. But there is a friction in the process.

TODO examples

## Federated Identity

CE has a not unreasonable focus around password and account security, broadly:
* Passwords should be sufficiently long
* Some shorter passwords are acceptable if combined with another measure
  * Multi-factor authentication
  * Authentication attempt rate limiting

All very reasonable, but it presents a problem for service providers using federated identity to provide access to resources to users from a different organization; they don't control any of these parts of the authentication. This model is extremely prevalent in Higher Education. Access to e-Resource providers is authenticated by the subscribing University, with authorization and content delivery being handled by the e-Resource provider. Because the e-Resource provider does not handle the authentication itself, it cannot make any guarantee on password length, or that any rate limit has been imposed.

