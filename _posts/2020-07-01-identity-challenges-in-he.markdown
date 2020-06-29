---
layout: post
title:  "Identity challenges in higher education"
date:   2020-06-01 09:00:00 +0100
author: sam_jones
summary: Identity is often more complex in a University environment than it first appears.
image: /assets/images/uni.jpg
categories: 
published: true
---

![](/assets/images/uni.jpg)

One way to look at Universities, albeit very simplistically, is to say that
they are in effect rather like a regular business.

They have employees who work for the university, and they have customers
(students) who pay money to consume the institution's product. Indeed,
Universities being more business like has been a broad strategic direction for
many years now.
 
From a systems and software point of view this way of thinking is appealing!
There is a vast market of software for business in the world that academic IT
departments can consume if think less in terms of students and lecturers and
more in terms of customers and employees. Certainly a lot of good has come from
re-purposing software from industry.

But it's not all roses, let's talk about some of the problems here.

## Seperation of the user pool into distinct user types or systems

If we're a company that makes widgets and then sells them online, from an IT
point of view, we have our staff and some customers. They're all people, but from
an IT perspective they have different needs and it makes sense for us to treat
them as two very different, quite obvious, types.

Customers; who buy the widget they want, they can access support resources, and
can access a online portal to manage their widget

Staff; Need access to the customer support system, some file storage for
documents, email, etc. We also need to track a bunch of data about them, eg
payroll/leave. 

Clearly, in this example, there is no real cross over between the two groups,
it makes sense to have seperate systems for the these tasks. Indeed, trying to
shove these identities into a single system would add an information security
risk because it makes us easier to accidentally give more access than is
appropriate.

In a university we have students and we have staff. Students need to be able to
access learning resources from across the world, we probabaly also have a
teaching platform that they need to access, we'll give them an email account,
they'll need somewhere to put files, and a range of other things. Staff will
need many of the same things, but sometimes in a different way. They'll need
email and files in much the same way as the students, they'll also need access
to the teaching platform but as a content creator/curator rather than as a
client, also staff will need access to systems that give information about
students like their grade history. We need to be careful about the access
students have to that!

Clearly here we have a lot of cross over. Email and files are the same
function, the users maybe need different access rights but it's more efficent
to use the same system for both and avoid seperating the user pool. As far as
the teaching system is concerned, students and staff need to be in the same one
by necessity if the students are to consume the content created by staff.
Though clearly, their roles are very different.

## Students and Staff and everything in between

Let's run with the teaching system example. We have two very clear roles; you're
either a content creator or a content consumer. We can describe this in our
software system in a simple way by creating the two roles and then governing
all access to this system based on which one the user at the time has.

This seems to fit the requirement, but it breaks down when the lines between
student and staff get a little blurred. It's common to recruit MSc students as
teaching assistants for undergraduate courses; how does this affect our systems
security model?  Ideally the access needs to be more nuanced, the MSc
student/teaching assistant needs to be a mixture of the two roles. If the
software isn't able to handle this, then we end up with clumbersome work
arounds like giving the person two different logins and putting the
responsibility on them to use the correct identity for a given task. This is
often confusing for users.

Spinning up multiple identities for an individual also makes it hard to revoke
access when it is no longer required as it is harder to manage in an automated
way. We can try to manage this manually, but this tends to mean access isn't
revoked in a timely way and often manually managed access control lists contain
a large number of accounts who should not have access, an obvious security
risk.

## It's common for University's buy their own produce

A student studies at a University, they like the academic life, they're good at
their field and they have a strong desire to study it deeper. Their lecturers
are pleased with the student is doing and think tey hold potential. The
students course ends and as they start to look for work they notice a position
is available at the Uni their studying at. They apply, they get the role, the
student becomes a member of staff with no break between their study and
professional roles.

This is in fact a overly simplified version of a very common pattern in HE that
doesn't really apply in other sectors. Our example is simplistic because the
change is rarely this binary. Normally a student will phase across to academic
life by undertaking a higher level course with some expecation of teaching, and
gradually getting closer to a role focused more directly on research or
teaching and less on being taught (although they are likely always learning).

How does IT reflect this? We need to revoke access to systems as it becomes
inappropriate for them to have access, we need to grant new access as it is
necessary, we need to find a way to manage the murky middle ground as they
transition from one role to the other.

In reality most commercial software aimed at HE has some cover for this so our
example of the online learning platform is probably capable of handling tihs,
but other functions get tripped up here and it's important to be aware of this
when utlizing software designed for other sectors in HE; how well does it fit
your more unusual needs?

## More efficency! More data responsibility! More utility!

There are several trends in HE IT right now that vy with each other. Data
processing maturity is becoming increasingly important with big fines and
scandals waiting for organisations that treat their data neglagently. Cost is a
factor given the changing funding landscape for HE, so where Universities would
previously run or develop their own in house systems to meet their users' needs,
now the cost of having systems administration staff and development staff
competes with things that are more core to the Universities goals. This
internal competition increases the desire to seek efficency gains by doing less
costly development and hosting internally. At the same time the general
expecation of what we get from our IT systems is higher than ever before.
Universities also face some more recent competition in the form of MOOCs where
the technological experience plays a key role, but the organisational cost
model is radically different.

These requirements compete with each othher for time and money. Our identity
model is complex and data handling maturity is importance for complicance, an
answer would be to develop and run systems in house but the cost is high and it
robs our core business functions of resources.

Off the shelf and Software as a Service solutions are comparatively cheap,
which means we can focus better on our core objectives, but they often have a
security model that doesn't neatly match our identity scenario. If unchecked we
can end up handling sensitive data poorly because of this, or add unwanted
complexity from a user point of view.

We can expand our scenario yet futher. Many Universities offer pre-access
programs to bring students-to-be up to a required standard before thhey start
their course. This and other factors means sometimes students are younger than 18.
How does an organisations responsibilities change when some of their users
are legally not adults? We can restrict all student access as if they were not
adults to safe guard the organisation in this respect, but what is the fall out
of treating everyone like a child when only a minority are not yet adults?

## Who is a part of your organisation?

Age, and pre-course programs bring another question. E-resource providers
license their content to Universities. As a part of the terms of such
contracts, Universities must authenticate their users and make statements about
the user's membership of the University. The E-resource then restricts based on
those statements. It is a legal requirement that the statements are correct.

Is our pre-access course student a member of the institution, should they have
access to the resource acording to the agreed license? How is this expressed by
the IT system? I would argue there is likely not a single answer and one needs
system that is flexible enough to facilitate a range of scenarios.

This goes deeper as you explore the miriad of relationships Universities have
with people. Some Universities make their libraries open to the public, what IT
access should these people get? Sometimes a professor will retire after a long
career but because their interest was always the field and not the pay they
continue to carry out their important work for their now former employer, how
does this feed into our identity management? If we hire 3rd party contractors
to work on our IT systems, are they the members of the institution that should
have access to certain licensed e-resources?

Universities also have alumni. Clearly Alumni do not need a lot of access to
systems at the institution but they remain a source of funding for Universities
and if a University chooses to seek a closer relationship with it's alumni then
those people will likely need an increasingly rich digitial identity from a
University perspective.

You can see how the devil is in the detail!

## Bring your own device

A comparatively recent concern in the commercial world is BYOD (Bring your own
device). The rise of smart phone and wireless technology has posed a data
access question to organisations who hither-to did not need to consider it:
what access to organisational resources should a user owned device get?

Previously it wasn't much of a concern because few people had phones capable of
email and web, and the data access to do so was expensive at any rate. Working
from home on ones own computer was also less of an acceptable idea (to both
parties) as it is now. Organisations could easily hide all their infrastructure
behind one big firewall and control access tightly by only allowing
organsiational equipment access to the corporate network.

Universities got early exposure to the bring your own device problem: students
in halls would often bring their own equipment and do their best to manage
access control in a situation where not all devices on the network could be
considered safe.

## Legacy infrastructure

All but the newest (or most diligent) of organisations have some legacy
infrastructure. But most universities have a history that pre-dates the change
in funding that has effected the sector, which is not necessarily true in other
industries. Additionally, the Higher Education sector played a central role in
the early days of the Internet. This means sometimes HE Organisations are
burdended with a legacy infrastructure based on a radically different set of
requirements and cost model than what they have today. A harder to resolve
situtation than in commerce where legacy infrastructure tends to refer merely
to an out of date way of solving a problem that still exists in much the same
way it did before.

For any organisation legacy is a pain. There is much risk switching between
systems, likely user distruption, and little percieved business benefit.

These systems often quietly get on with their day to day business, knowinly or
unknowningly ignored by the IT organisation, often requiring expertise or
knowledge that has left the organisation or is the domain of very few
individuals. The strategy of waiting for the inevitable is not a good one!

## So what to do?

 * Rich identity management that accurately reflects your users roles is key.
 * Buy into software and services which provide rich controls over access and
	 permissions, and ideally externalise these.
 * Avoid software that pushes you compromise your users experience because of
   an inferior access model.
 * Avoid software that has it's own authentication system and cannot intergrate
   with your wider authentication infrastructure.
 * Avoid software that makes it hard to honour your data processing compliance
   obligations.

## Get help!

If these experiences strike a cord with you, maybe you're finding yourself in a
situation where you're having to unpick a similar situation. If so consider
[getting in touch](/contact/), we're only to happy to help!





