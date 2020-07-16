---
layout: post
title:  "Identity challenges in higher education"
date:   2020-07-16 12:57:00 +0100
author: sam_jones
summary: Identity is often more complex in a University environment than it first appears.
image: /assets/images/uni.jpg
categories: 
published: true
---

![](/assets/images/uni.jpg)

One way to look at Universities, is to say that they are like businesses. 

They have employees who work for the university, and they have customers
(students) who pay money to consume the institution's product. Indeed, becoming
more business-like has been a broad strategic direction for Universities for
many years now.
 
From a systems and software point of view this way of thinking is appealing!
There is a vast market of software for business that academic IT departments
can consume if they think less in terms of students and lecturers and more in
terms of customers and employees. Certainly a lot of good has come from
re-purposing software from industry.

But it's not all roses, let's talk about some of the problems here.

## Separation of the user pool into distinct user types or systems

Thinking of our students as customers tends to lead us down a path where we
create separate systems for our staff and students.

In a commercial organisation this is normally a very sensible thing to do. If
we're an organisation that makes widgets, the needs of our customers and staff
are totally different with little or no overlap. Customers and staff will still
both have identity information we need to keep track of. We could try and push
that all into a single system, but what is the pay off if the two groups of
users never access the same systems?  On the other hand what is the risk of
doing this? Adding our customers to the same identity infrastructure as our
staff exposes us to possible priviledge escalation attacks that would be
impossible if they are in separate systems..

User requirements in a University tend to have more overlap. Everyone is going
to need access to email, files, and calendar. Most are going to need access to
the online learning environment.  There are some systems that only staff should
have access to like finance and HR. There is also an array of smaller systems
to support particular teaching and research objectives that only a few staff
should have access to.

If we don't want our users to drown in username and password combinations we're
goning to need a authentication system that grants access to all of these systems
with a single set of credentials per user.

If we limit ourselves into thinking about just staff or just student when we're
thinking about our users, the systems we build reflect that.  Hence we end up
with an email system for students that's totally separate from the email system
for staff, or with separate files storage systems, desktop experiences, web
portals, etc.

We un-wittingly build borders around our perceived user groups.

A lot of commercial software makes similar assumptions. For example it's not
uncommon to find help desk systems that assume you're either a member of
support staff or a customer with no nuances in between.

If you're a company that sells widgets, how often does one of your customers
login to the helpdesk system and start working on tickets? Probably not that
often, but this kind of exception is quite common in HE.

## Students and Staff and everything in between

One way things can get murky when we build these barriers, is it makes it hard
for us to decide how to handle people who sit in the awkward middle ground.

Many times a university will want to treat certain classes of student more like
staff and less like students, but not completely like staff! This happens a
lot with PhD students who are often expected to take on teaching assistant
roles. Similarly IT support roles are sometimes delegated to enthusiastic
technically-able students.

When we make hard boundaries between the systems we provide for our users,
limiting some and enhancing others, we make handling these edge case scenarios
difficult or impossible.  

We might decide to work around cases like this by spinning up a second IT
identity for the student, one that represents their more staff-like role, and
telling them to choose their identity based on the task at hand. This is
confusing for users, but it's also a problem from an auditing and compliance
point of view. How are accounts like this managed? When do they get revoked? If
there aren't good answers to these questions this kind of work-around becomes a
security hazard.

## It's common for Universityies to buy their own produce; and that's good!

This behaviour of treating a student like a member of staff is a part of a
larger process. It goes like this:

1. Student attends university as undergraduate and studies hard.
1. Student completes degree and decides to continue to a postgraduate degree
1. Student starts to take on staff-like functions e.g: teaching
1. Student finishes postgraduate degree and continues to carry out some staff like functions
1. Student acquires post-doctoral role or lectureship and becomes "staff"

Universities, at their core, are in the business of knowledge. They train
people to be knowledgeable and equip them to be able to create/discover
knowledge. Obviously, it's going to make sense for them to retain a portion of
their graduates as staff. So this scenario is very common.

How does IT reflect this? We need to revoke access to systems that become
inappropriate for them to access, we need to grant new access as it is
necessary, we need to find a way to manage the murky middle ground as they
transition from one role to the other.

As is often the case it's easy to think of ways IT can drop the ball here, eg:
revoke access to all students at the end of their course, there-by locking out
our example user as well.

If we've separated out our user pool into grouping based on type then arguably
we should find a way to manage this migration as seamlessly as possible. This
is often very hard, commercial data migration tools tend only support migration
paths that suit the commercial interests of the supplier. That is to say
inbound migration tends to be easy and outbound migration ... not so easy. 

Even where a tool exists, often, some aspects of the data will be lost. 

Sometimes this problem is passed to the user "Please backup your data so we can
migrate you to the staff system." before presenting them with a new and empty
account after the migration.

## More efficiency! More data responsibility! More utility!

There are several trends in HE IT right now that conflict with each other.

 * Data processing maturity is becoming increasingly important with big fines
   and scandals waiting for organisations that treat personal data poorly.

 * The current funding model means that higher education instituions are under
	 pressure to reduce costs. Therefore where once an institution would have the
	 capacity to run a service in house, it may now seek to move the function to
	 an external provider. Allowing it to focus on core teaching and learning
   functions[^1].

 * Society as a whole expects to get more from IT than ever before.

These requirements compete with each other for time and money. If our identity
model is complex and data handling maturity is important for compliance, an
answer might be to develop and run systems in house but the cost is high and it
robs our core business functions of resources.

Off the shelf and Software as a Service (SaaS) solutions are comparatively
cheap, but they often have a security model that doesn't neatly match our
identity scenario. If unchecked we can end up handling sensitive data poorly
because of this, or add unwanted complexity from a user point of view.

The amount of sensitive data a University might handle is huge, just think
about the strong links that Universities often have with hospitals! Most
students are older than 18, but pre-access programs and similar mean that not
all are. Many students live in University owned and run premises, which leads
to yet more information security risks.

## Who is a part of your organisation?

E-resource providers license their content to Universities. As a part of the
terms of such contracts, Universities must authenticate their users and make
statements about the user's membership of the University. The E-resource then
restricts based on those statements. This can only work because the statements
the Universities make are expected to be accurate.

If we grant an external organisation some level of access to our systems and
give their users identities within our infrastructure, then should those people
also get access to the licensed content? Clearly not, but this limitation must
be expressed by the IT System to adequately effect the restrictions of the
license. Otherwise, the likely default of those user accounts represents a
breach of the license terms.

This goes deeper as you explore the myriad of relationships Universities have
with people:

 * Some Universities make their libraries open to the public, what IT access
   should these people get?

 * Sometimes a professor will retire after a long career but continue to carry
	 out their important work for their now former employer. How do we know when
	 to revoke this access so that we're managing our user population maturely?
   What systems should they have access to?

 * Universities also have alumni and may wish to extend services to them, but
   without jeopardizing the rest of the estate.

## So what to do?

We're a long way from the student and staff model we started with. Identity
provision is a complex task in a University environment and the right path 
depends on the exact requirements, but there are some things that can help:

 * Rich identity management that accurately reflects your users roles is key.
 * Buy into software and services which provide rich controls over access and
	 permissions, and can ideally externalize these.
 * Avoid software that pushes you compromise your users experience because of
   an inferior access model.
 * Avoid software that has its own authentication system and cannot integrate
   with your wider authentication infrastructure.
 * Avoid software that makes it hard to honour your data processing compliance
   obligations.

## Get help!

Do these issues strike a cord with you, or maybe you're finding yourself in a
similar situation? If so consider [getting in touch](/contact/), we're only to
happy to help!

---
# Footnotes:

[^1]: Switching from a legacy IT System is rarely as clean as this, often
ending in a situation where both new and old worlds exist in parrallel for some
time.


