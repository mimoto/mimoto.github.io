---
layout: post
title:  "SAML Metadata - Introduction"
date:   2019-06-13 16:50:00 +0100
author: pete_birkinshaw
summary: An introduction to SAML metadata
image: /assets/insight/img/header-7.jpg
categories: explanations
---
# SAML Metadata

If you've ever been involved in project that uses SAML for authentication then you've probably encountered SAML metadata. 

The purpose of SAML metadata is to let different services work together, but something that we've noticed over the years is that different organisations often have differing interpretations of what SAML metadata is for and how it should be used, and this can make collaboration between them awkward. 

## SAML entities

If you're running a SAML service using software like Shibboleth, SimpleSAMLphp or ADFS then your service is identified as one or more *SAML entities*. An entity is a named, unique service, usually identified with a URL.

The two most common roles of an entity are *Identity Provider* (IdP) - where users can authenticate, and Service Provider (SP) - the service (usually a website) that requires authentication.

SPs and IdPs could be internal services on your office network, shared resources at partner companies, academic resources such as journals, cloud SaaS websites such as Google Docs or PaaS environments like Amazon's AWS.

## Metadata's role

SAML entities need three things in order to work together:

- Discoverability 
- Compatibility
- Security and Trust

Discoverability: an SP needs to know which IdPs are available to provide authentication. Users of services need to be able to find their IdP, and might want to browse available SPs in a service catalogue.

Compatibility: SAML offers a variety of ways for services to communicate, and the URLs handling the process can vary. Services need to work out which protocols they have in common.

Security and Trust: It's unwise to freely share all information about your users with everyone, and it's important to make sure the other SAML sites are what they claim to be. 

SAML metadata is a chunk of XML that can be used to provide all three. Just as a business card given you by someone you trust lets you identify and contact them when added to your address book, sharing metadata allows an SP or IdP to know about another entity and how to talk to it. Metadata is typically downloaded and an SP or IdP is configured to read the file.

Here's an example I've taken from Wikipedia:

```xml
    <md:EntityDescriptor entityID="https://sso.example.org/idp" validUntil="2017-08-30T19:10:29Z"
    xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata"
    xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
    xmlns:mdrpi="urn:oasis:names:tc:SAML:metadata:rpi"
    xmlns:mdattr="urn:oasis:names:tc:SAML:metadata:attribute"
    xmlns:mdui="urn:oasis:names:tc:SAML:metadata:ui"
    xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    <!-- insert ds:Signature element (omitted) -->
    <md:Extensions>
      <mdrpi:RegistrationInfo registrationAuthority="https://registrar.example.net"/>
      <mdrpi:PublicationInfo creationInstant="2017-08-16T19:10:29Z" publisher="https://registrar.example.net"/>
      <mdattr:EntityAttributes>
        <saml:Attribute Name="http://registrar.example.net/entity-category" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:uri">
          <saml:AttributeValue>https://registrar.example.net/category/self-certified</saml:AttributeValue>
        </saml:Attribute>
      </mdattr:EntityAttributes>
    </md:Extensions>
    <md:IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
      <md:Extensions>
        <mdui:UIInfo>
          <mdui:DisplayName xml:lang="en">Example.org</mdui:DisplayName>
          <mdui:Description xml:lang="en">The identity provider at Example.org</mdui:Description>
          <mdui:Logo height="32" width="32" xml:lang="en">https://idp.example.org/myicon.png</mdui:Logo>
        </mdui:UIInfo>
      </md:Extensions>
      <md:KeyDescriptor use="signing">
        <ds:KeyInfo>...</ds:KeyInfo>
      </md:KeyDescriptor>
      <md:SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://idp.example.org/SAML2/SSO/Redirect"/>
      <md:SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://idp.example.org/SAML2/SSO/POST"/>
    </md:IDPSSODescriptor>
    <md:Organization>
      <md:OrganizationName xml:lang="en">Example.org Non-Profit Org</md:OrganizationName>
      <md:OrganizationDisplayName xml:lang="en">Example.org</md:OrganizationDisplayName>
      <md:OrganizationURL xml:lang="en">https://www.example.org/</md:OrganizationURL>
    </md:Organization>
    <md:ContactPerson contactType="technical">
      <md:SurName>SAML Technical Support</md:SurName>
      <md:EmailAddress>mailto:technical-support@example.org</md:EmailAddress>
    </md:ContactPerson>
  </md:EntityDescriptor>
```

## Creating Metadata

In most cases you won't need to create your own metadata from scratch, as your IdP or SP software will generate an initial version of it for you when you first configure it.

If you do need to create metadata from scratch, [OneLogin provide a handy web tool](https://www.samltool.com/sp_metadata.php) to get it started. You'll still to know the technical details, but it will wrap them up suitable XML

You will probably need to edit the metadata a little. The default metadata will reflect the way your IdP or SP has been configured when first installed and will probably not be updated if you reconfigure your service. You'll need to make sure the metadata continues to describe the service you are running. You might also like to disable certain features, or add additional descriptive information such as logos, privacy information, and location.


## Sharing individual metadata documents

The most basic way to use metadata is close to the business card metaphor: staff running the IdP or SP you want to use will send you a file or a URL with metadata for their entity, which you configure your entity to read. They do the same with your entity's metadata.

If the two systems are compatible and configured correctly they will read the metadata and use it communicate with each other.

## Cloud services 

Many Software-as-a-Service websites (SaaS) offer SAML authentication, often as a luxury perk of paying for a more expensive subscription. Very few of them accept normal metadata files for their customer's IdPs. Frequently you will be presented with a file for their metadata and a form where only certain configuration details for your service have to be manually configured. The terms they use to describe each configuration option will be often be confusing.

You'll find the information they need in your metadata file - copy and paste the relevant parts of it.

## Signing Metadata

Metadata can be signed with cryptographic keys to make it more secure: your service can be configured to use the public key of the metadata provider to check you are using an authentic, unchanged copy of the file. If the metadata has been changed it will fail a signature validation check and will not be used.

## The problems with exchanging individual metadata files

Configuring your service to use individual metadata file for each service works fine for smaller organisation with a few SSO services - maybe an intranet portal, cloud office suite, and so on. In fact, Microsoft's ADFS *only* supports individual metadata records, and has limits to how many entities it can remember.

However, configuring each relationship with another entity with individual files can easily become **very awkward** as the number of entities you wish to access grows.

- An IdP needs to know in advance what your users want to access, and SPs need to know all a potential user's IdPs. When using individual files everything needs to be configured in advance.
- If files are stored locally then whenever an entity changes its configuration new files will need to be sent out to replace the old one - potentially to many other organisations. This can lead to mistakes, downtime, and a lot of wasted time.  You will need to maintain a list of everyone who needs your metadata.
- If files are downloaded automatically the chance of some metadata becoming unavailable increases
- If signed metadata is used then the management of many keys also becomes a problem: if a key expires metadata will not be available, so administrators need to manage key roll over, distribution, verification and so on.
- You need to assess the configuration and trust of each new entity.

For academic organisations typically using many, many online service this would make managing individual metadata files an enormous hassle, so it's no surprise that the SAML software commonly used for federated SSO at universities (such as Shibboleth and simpleSAMLPhp) takes a different approach: aggregated metadata, provided by national federations.

In the next post I'll describe metadata aggregation, how it makes large scale SSO possible, and how it's reaching its limit...
