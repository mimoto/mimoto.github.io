---
layout: post
title:  "Duo MFA in Shibboleth IDP v3.3.x"
date:   2017-06-01 14:54:58 +0100
author: Sam Jones
categories: Shibboleth-IDP Duo MFA
---
Multi-factor authentication is becoming increasingly prevelant today, and in our experience many are choosing to use Duo to use a user's mobile phone as a second factor.

![A better picture is needed to illustrate this ... ](/assets/images/child_and_bear.jpg)

Shibboleth IDP has very good support for MFA. Duo have a plugin on their site which can be used with an earlier version, but Duo is supported in the main distribution from version 3.3.0. IDP v3.3.x is a very flexible bit of software, and there are lots of ways you and configure it to work with Duo depending on your requirements, what follows is a relatively simple configuration:

Ultimately we're going to do 4 things ...

* modify idp.properties to bring in the authentication handler we need
* modify the duo.properties to set some duo properties
* modify the mfa-authn-config.xml to describe the multi-factor behaviour we want
* modify the relying-party.xml to trigger the MFA process

First, let's make the Duo and MFA authentication flows available by modifying the **conf/idp.properties** file:

{% highlight java %}
#idp.authn.flows= Password
idp.authn.flows= MFA|Duo|Password
{% endhighlight %}

Next, we'll get the various keys we need for Duo in place, in **conf/authn/duo.properties** .

3 of these keys come from Duo control panel, one of them you create yourself as described here <https://duo.com/docs/duoweb#1.-generate-an-akey>.

{% highlight java %}
idp.duo.apiHost = <the api host as specified in the duo control panel >
idp.duo.applicationKey = <a key you need to generate as described here: https://duo.com/docs/duoweb#1.-generate-an-akey >
idp.duo.integrationKey = <you'll find this key when you setup Shibboleth IDP as an application in the Duo control panel >
idp.duo.secretKey = <Again, you'll find this in the Duo control panel >
{% endhighlight %}

Our 3rd step is to describe the MFA behaviour we expect in the **conf/authn/mfa-authn-config.xml** :

{% highlight xml %}
<util:map id="shibboleth.authn.MFA.TransitionMap">
  <!-- First rule runs the Password login flow. -->
    <entry key="">
      <bean parent="shibboleth.authn.MFA.Transition" p:nextFlow="authn/Password" />
    </entry> 
  <!-- Second rule runs a function if Password succeeds, to determine whether an additional factor is required. -->
   <entry key="authn/Password">
     <bean parent="shibboleth.authn.MFA.Transition" p:nextFlowStrategy-ref="checkSecondFactor" />
   </entry>
   <!-- An implicit final rule will return whatever the final flow returns. -->
</util:map> 
<!-- Example script to see if second factor is required. -->
<bean id="checkSecondFactor" parent="shibboleth.ContextFunctions.Scripted" factory-method="inlineScript">
  <constructor-arg>
    <value>
      <![CDATA[
        nextFlow = "authn/Duo";
        nextFlow;   // pass control to second factor or end with the first
      ]]>
    </value>
  </constructor-arg>
</bean>
{% endhighlight %}

This is the default, it tells the IDP to do Password authentication first, then on success pass them to Duo. If you want a more advanced behaviour, for example if you only want to enable Duo for certain users, then you can limit the Duo step to only those who have the relevant attribute here, but for our purposes we're going to stick with the default.

The final file we need to look at is the **conf/relying-party.xml**, where we're going to enable MFA as the authencation flow for Shibboleth.SSO and SAML2.SSO protocols:

{% highlight java %}
    <bean id="shibboleth.DefaultRelyingParty" parent="RelyingParty">
        <property name="profileConfigurations">
            <list>
                <bean parent="Shibboleth.SSO" p:authenticationFlows="#{{'MFA'}}" p:postAuthenticationFlows="attribute-release" />
                <ref bean="SAML1.AttributeQuery" />
                <ref bean="SAML1.ArtifactResolution" />
                <bean parent="SAML2.SSO" p:authenticationFlows="#{{'MFA'}}" p:postAuthenticationFlows="attribute-release" />
                <ref bean="SAML2.ECP" />
                <ref bean="SAML2.Logout" />
                <ref bean="SAML2.AttributeQuery" />
                <ref bean="SAML2.ArtifactResolution" />
                <ref bean="Liberty.SSOS" />
            </list>
        </property>
    </bean>
{% endhighlight %}

That's it, reload the web app and you should now have a second factor on all your web based SAML logins.