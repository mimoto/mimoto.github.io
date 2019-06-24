---
layout: post
title:  "Aggregated SAML Metadata and Federations in Higher Education"
date:   2019-06-24 16:53:00 +0100
author: pete_birkinshaw
summary: How FE & HE use identity federations to keep SAML manageable
image: /assets/insight/img/header-7.jpg
categories: explanations
---
# Aggregated SAML Metadata and Federations in Higher Education

My [previous post](https://mimoto.co.uk/explanations/2019/06/13/saml-metadata-intro.html) explained the purpose of SAML metadata, and ended by listing the potential problems with configuring metadata by manually copying files between each service.

Recap of previous episode: Exchanging metadata in advance with each service you want to use is fine for a few services but doesn't scale at all. It may be practical for small organisations, but for academic institutions using hundreds of services it will become a considerable problem.

## Federations

Fortunately there's a simple solution: have someone else do the hard work, trust them to provide trustworthy information for many entities, and download the metadata for **all** the other entities at once. This is the main role of academic identity federations, usually run by National Research and Education Networks (NRENs). In the UK the [UK Access Management Federation](https://www.ukfederation.org.uk/) performs this role as part of [JISC](https://www.jisc.ac.uk/), while in the USA it's [InCommon](https://www.incommon.org/), part of [Internet2](https://www.internet2.edu/). Many [other countries and regions](https://refeds.org/federations) have their own academic federations.

Identity federations will require their members to agree to follow a code of practice. Members send the metadata for their entities to the federation, where it is then tidied up and sometimes enhanced by the federation to carry extra information. 

The cleaned-up entity metadata is then compiled into a metadata aggregate - an XML collection of entity metadata records. Larger federations publish metadata aggregates with over 5000 entities.  Rather than configuring an IdP or SP to read many individual metadata records an operator can configure their SAML software to regularly download the entire aggregate.

In my [previous blog post](https://mimoto.co.uk/explanations/2019/06/13/saml-metadata-intro.html) I described an individual metadata record as being a little like a business card for a service. That metaphor can be pushed a bit further here - aggregated metadata is like a telephone directory.

## The Benefits of Using Aggregated Metadata

- An IdP using federated metadata already knows about many services in advance, so if a user tries to access a service that is part of the federation, SSO might work without any additional configuration at all.
- When services are reconfigured and their metadata changes the operator only needs to send their new metadata to the federation. The next time the federation's aggregate updates (usually once a day) all other members of the federation will receive the changes without any extra effort.
- Federations provide very reliable, high bandwidth download services for aggregate files
- Federations will sign their aggregate, and only one key will be needed to verify the signature of all entities.
- Federations will have already established a basic legal relationship with the operators of the entities, and can sanction operators who don't behave properly.

## Inter-federation

Organisations can join more than one federation, and have metadata for their entities published in many different aggregates. For instance, EBSCO's metadata is published by over 25 federations, Web Of Science by over 24.

For smaller organisations the overhead of joining many federations can be prohibitive. This is particularly an issue for international research projects, where service providers and IdPs may be in a variety of different national federations.

[Edugain](https://edugain.org/) aims to solve this problem by acting as a federation-of-federations: accepting metadata from national federations to form a new international aggregate, and then encouraging national federations to import entities from the new combined aggregate back into their own aggregates. Edugain's hope is that a small organisation will be able to join their national federation and soon afterwards have their entity's metadata available to services all over the world. 

[REFEDS](https://refeds.org/) is an open organisation that acts as an industry forum for federation operators and members, developing standards, interoperability, and encouraging debate and innovation. They're a good source of tools to explore metadata from federations. 

## The Future

NREN identity federations and aggregated metadata have made SAML a practical approach for higher and and further education, and helped education become the leading sector for modern authentication. Over 26 million students and academic staff have access to services using Edugain metadata, and tens of thousands of entities have metadata published via federations. 

But academic identity federations have been a victim of their own success: aggregates are becoming unwieldy as they continue to gain more entities. Some federations include website logo data directly in the metadata rather than as links - this has benefits buts considerably bloats aggregates. 

Daily or even hourly downloads of 50MB files are not really an issue themselves, but 50MB of XML is an awful lot of XML to process. Processing large metadata aggregates can cause SP software to start up so slowly that the operating system decides the service has crashed and shuts it down. IdPs loading metadata from federations into memory can require gigabytes of RAM per federation. 

This problem wasn't unexpected - in fact for the early pioneers of SAML this was a problem that they hoped to have one day. Aggregates were a simple solution to metadata management that worked well and made SSO such a success in education. They accepted that when aggregates became too large another metadata distribution method could be developed.

The successor to simple aggregates is already being rolled out - it's called MDQ, and the next blog post will hopefully explain how helpful this simple new standard can be.
