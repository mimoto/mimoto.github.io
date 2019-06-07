---
layout: post
title:  "External authentication in Spring Boot"
date:   2017-11-13 15:40:00 +0100
author: sam_jones
summary: Enabling federated authentication to your e-resource or web application.
categories: java shibboleth_sp
---

Here at Mimoto we believe if you're doing web application development you should avoid cooking authentication into your application. We're also big fans of the Shibboleth SP software as a way of enabling federated authentication to your e-resource or web application.

A lot of people use the Spring Boot frame work for web application and a feature I quite like about it is the ability to run your web application [directly from the jar file](https://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-running-your-application.html#using-boot-running-as-a-packaged-application). It's even easy to make it into a neat [deployable executable](https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html) that fits well with init.d or systemd.

Before we had that, we'd roll out a war file and deploy that with Tomcat. If one wanted to add Shibboleth SP as the authentication layer for the webapp, then that would be done by adding a AJP connector to tomcat with "tomcatAuthentication" turned off, then proxying to that via Apache HTTPD and using the Shibboleth SP module to protect the application.

We can now do better: using Spring Boot we can bring up a AJP connector inside our own web application and disable tomcatAuthentication within that so we can delegate authentication to Apache HTTPD and Shibboleth SP. This means we no longer need to manage the Tomcat software itself!

Here's how I've been enabling this in my Application.java:


```java
package org.example.tomcatauthtest;

import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.SpringApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.boot.context.embedded.EmbeddedServletContainerFactory;
import org.springframework.boot.context.embedded.tomcat.TomcatEmbeddedServletContainerFactory;
import org.apache.catalina.connector.Connector;


@SpringBootApplication
public class Application {

  public static void main(final String[] args) {
    SpringApplication.run(Application.class, args);
  }


  @Bean
  public EmbeddedServletContainerFactory servletContainer() {
    TomcatEmbeddedServletContainerFactory tomcat = new TomcatEmbeddedServletContainerFactory();
    Connector ajp = new Connector("AJP/1.3");
    ajp.setProtocol("AJP/1.3");
    ajp.setPort(8009);
    ajp.setSecure(false);
    ajp.setAllowTrace(false);
    ajp.setScheme("http");
    ajp.setAttribute("tomcatAuthentication", false);
    tomcat.addAdditionalTomcatConnectors(ajpConnector);
    return tomcat;
  }

}

```

Provided you front your web application with something that talks AJP and handles the authentication, you should now be able to access details of the authenticated user by using the Principal object within one of your controllers.

If you have questions about this, or need help integrating federated identity with your infrastructure feel free to [talk to us](/contact/)

