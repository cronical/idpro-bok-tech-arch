# Technical Architecture Model
## Abstract
This document provides a model to organize the presentation of technical details associated with various implementations of the architectural concepts.  This article provides the set of generic components which are exemplified below.  It is a restatement/extension of the ISO framing. It is simplified to remove the UML fine points, which the typical reader, may not find helpful. The extension allows authorization and governance can be included. Another extension shows how external risk context can be incorporated into the identity management system. 

## Introduction
The following is the basic organization of an identity management system, which supports multiple relying services.

![](resources/basic-component-dependencies.png)

The most basic function of the identity system is to provide secure storage of the information about identities.  The audit repository is shown since that is perhaps one of the most salient aspects of providing that security. 

While, it is possible to have an identity management system without attaching it to external data, this is typically not the case. Usually employee or customer data needs to be imported.

The model can be used at different levels.  For instance, a modern architecture may have a web-hosted application that calls on an Identity as a Service (IDaaS) cloud provider, which acts as the Identity Management System.  In another example, a file system grants access to users based on the user information acquired at login.  Despite both these functions being encapsulated in an operating system, the model holds.

We will add on more detail during the next several sections.

## Provisioning
Provisioning describes how the data gets into the identity repository and how it flows further on to support authorization decisions.

Note that the Identity Information Source can be singular, such as a single HR system.  Or it can plural, for instance in the case of a company that has, say, more than one HR system.

Also note, that the notion of importing does not necessarily mean making a physical copy of data, although it often does. The notion also supports the idea of virtualization - where the import of identity information is done at run-time.

The Identity Register could be implemented several ways.  Common methods include the use of general purposed databases, optimized stores such as directories and, as mentioned above, virtual directories.

Shown also, here is the function Principal and Credential Management.  This is intended to include steps needed to orginate and identity (such as proofing or vetting) as well as on-going maintenance such as password reset and other credential management activities such as token provisioning.  This function includes administrative activities and self-serve activities.

Also noted is the function of propagating selected information further into the ecosystem.  This is typically done for relying services that need additional information about the users, often for the purpose of access control or personalization.  The assumption is that the relying system makes a copy of the identity data and integrates it with application data.  Of course, a complete solution will allow for the full lifecycle including creation, update and eventual dispostion of the identity data stored locally.

Not shown here, but sometimes implemented, are provisioning actions that occur more on a just-in-time basis.  This can happen based on an assertion that the user is authenticated.  In this case identity information, possibly including, attributes is passed on to the relying system "just-in-time".  In a similar case, the relying party, may query the indenty management system, in order to acquire attributes.

![](resources/provisioning.png)

## Authentication and sessions
By authentication we mean that the Idenity Management System checks and verifies credentials that are presented by the Relying Service on behalf of the user.  There are many such scenarios.  

A common pattern is to associate the authentication event with the start of a session.  The session is mostly the concern of the relying system.  However, it is sometimes desirable to keep the sessions supported by several relying parties in synch. For instance, logging out of one, logs out of all.  To do this, often the Identity Management System plays a role.

The session can play an important role in step-up authentication.  The session can keep track of the level of assurance of a particular authentication, so when a relying service has a sensitive transaction needing step-up authentication, the identity management system can be prepared to determine the course of action.  This could be done at the relying system, but that would end up with a poor user experience if multiple relying systems with step-up needs were in play.

The existence of a centralized point of view about sessions, can be leveraged for advanced scenarios which include external risk facts. See Risk Context below.

![](resources/authentication-and-sessions.png)
## Authorization models 
Authorization models vary alot. The diagram shows two alternative approaches for authorization.

Both approaches typically use user attributes help determine access.  These values can be provisioned into a local store, as described above in Provisioning.  Or the values can be acquired at run-time from the Identity Management System. 

Many relying services perform authorization tasks internally.  The local nature of the protected resources often makes this appealing.  

Sometimes authorization is a shared resource for many relying services.  

![](resources/authorization-models.png)
## Access governance
Access Governance provides oversight and control over access rights implemented in many local or shared authorization systems.  Both of these may rely on user attributes such as groups or roles stored in an Identity Register. 

Typically, goverance activities review and may modify the data in one or more of the authorization components in order to effect a change in entitlements.

This is frequently implemented in enterprise systems focusing of employee/contractor entitlements.  However, the concept can also apply to customer facing scenarios such as busines to business delegated rights or business to customer scenarios where delegation such as power of attorney or other agents are implemented.

![](resources/access-governance.png)
## Risk Context
Risk context information can be valuable to improve the security of the relying service.  External events may be visiable to the Identity Management System operator through consortia or vendor packages.  In some mutual-support scenarios, it may be possible for the operator to also publish events for the benefit of others.

Events need to be delivered into the Identity Management System so that they can selectively be used to modify the behavior of the authentication function.  In some severe scenarios it may be desirable to attach the events to the session management function so that current sessions can be reviewed and terminated if needed.

![](resources/risk-context.png)
