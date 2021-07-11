IAM Reference Architecture Model
================================

Abstract
--------

This article provides a reference model to organize the presentation of technical details associated with various implementations of identity and access management (IAM) architectural concepts. The model is conceptual, as are the set of abstract components which it provides. 

To move out of the conceptual realm into specifics additional articles follow, each with a focus on a specific technical use-cases. Each such use-case indicates which of the abstract components comprise a particular implementation 

The model is a restatement/extension of the ISO/IEC framing [Note 1]. Some UML detail has been removed for simplicity. The IAM model has been extended so that authorization, governance and risk-control can be included.

Some of the ISO/IEC names have been changed to reflect more common usage. In come cases, the ISO names have been used in a way that is more expansive than their definition.

The model has been reviewed in conjunction with the FICAM, Internet 2, and NIST Zero Trust frameworks.

Introduction
------------

The following is the basic organization of an identity management system (IMS), supporting multiple relying services, or relying parties (RP).

![Diagram Description automatically generated](resources/basic-component-dependencies.png){width="6.268055555555556in" height="4.636805555555555in"}

The most basic function of the identity system is to provide secure storage of the information about identities and a way for relying  parties, to use that data to control access to resources. Note that the term Relying Service is used by ISO/IEC to encompass all types of components that use identity services, including systems, sub-systems, and applications, independent of the domain or operator.  We will use the more common Relying Party (or RP).

The audit repository is shown since that is perhaps one of the most salient aspects of providing that security.

While, it is possible to have an identity management system that is populated without attaching to an external data service, this is typically not the case. Usually, employee or customer data needs to be imported.

The model can be used at different levels. Here are a couple of examples:
#### Example 1
A modern architecture may have a web-hosted application (the RP) that calls an Identity as a Service (IDaaS) cloud identity service, acting as the Identity Management System. The RP in this case could be a customer facing application or a workforce facing application.

#### Example 2
A computer's file system (RP) provides access control based on the user information acquired at login (IMS). Despite both the file system and the identity management function being encapsulated in an operating system, the model holds.

Terminology
-----------

The terms are defined below and provided with abbreviations to facilitate reference in the use-cases.

### Identity Management System (IMS)

A set of policies, procedures, technology, and other resources for maintaining identity information. In this model it contains information about principals/subjects including credentials. It also including other data such as meta data to enable interoperability with other components.  The IMS is shown with a dotted line to indicate that it is a conceptual grouping of components, not a full fledged system in itself.

### Relying  Party (RP)

A component, system or application that uses the IMS to identify its users. The RP has its own resources and logic. This is also known as the Relying Service in the ISO/IEC model. This roughly corresponds to the Agency Endpoint in the FICAM model, or to Identity Consumers in the Internet2 model.

### Identity Information Authority (IIA)

This represents one or more data sources that are used by the IMS as the basis for the master set of principal/subject identity records. Each IIA may supply a subset of records and a subset of attributes. Sometimes the IIA is distinguished from the Identity Information Provider or IIP.  Here we mean this term to include the service that actually provides the information as well as the root authority.  Sometimes the authority for attributes is distinguished from the authority for identities.  In this case the term Attribute Provider is sometimes used.  Here we use this term to include both. This corresponds to Identity Information Source in ISO/IEC 24760-2, and Identity Sources in Internet 2.

### Enrolment 
Also known as Registration. Enrolment is concerned with  the proofing, and lifecycle aspects of the principal (or subject).  The entity that performs enrolment is known as a Registration Authority.

### Credential Service Provider (CSP)
A credential allows for authentication of an entity.  The Credential Service Provider is here meant to include the issuer as well as an subsequent management of the credentials.  FICAM separates this into a first-class component called Credential Management System, which also includes PKI information for federation, which this model indicates under metadata and discovery.

### Identity Register

This is the data store that contains the enroled entities, and their attributes.  We use this to include the storage related to credentials, although in practice, all or some of the credentials may be stored in their own physical repository.  

### Authentication (AUTHN)

The act of determining that the principal/subject is authentic to a level of assurance. In this model this is shown as a collaborative activity between the IMS and the RSVC. The FICAM model, at a more abstract level, includes this in the first-class component called Access Management.

### Session (SESS)

A period of time after an authentication event when an RSVC grants access to the principal/subject.

### Authorization (AUTHZ)

Authorization is how a decision is made to allow someone to access a resource. This is not included in the ISO or Internet 2 models. The FICAM framework includes this as a subcomponent of the Access Management System and is more explicit about the location of the implementation of the authorization

### Access Governance (IGA)

Access governance provides oversight and control over access rights implemented by relying systems using dedicated or shared authorization systems. The abbreviation used is for Identity Governance and Administration and is commonly used in the commercial sector. This roughly corresponds to the Access Certification section of the first-class component Governance Systems in the FICAM model. IGA is not specifically addressed in the ISO/IEC model.

### Risk Context (RCTX)

Risk Context consists of additional facts that can be brought to bear to improve the overall security of the ecosystem. Internal or external events and facts can be applied to enable, limit, or terminate access. This is similar to the section Monitors and Sensors under FICAM\'s Governance Systems, and, NIST 800-207 (Zero Trust) to many of the inputs of the Policy Decision Point as shown in Figure 2.

### Metadata (META)

Control data that allows the Identity Management System to recognize and trust the Relying Service. This corresponds to Relying Party data in the Internet 2 model.

Provisioning
------------

Provisioning is a term that encompases the processes and methods that create, modify, and, eventually, delete the identity and profile information used by IT infrastructure and business applications. By these method, records are created, or updated in the identity repository, and removed from it.  Often, provisioing needs to extend to applications  to support authorization decisions.

Note that the authoritative sources for identity attributes transcend the HR system and may include the email system, phone system, training certification etc. In some cases, a company may have more than one HR system.

The act of provisioning may include certain logic, best modeled as governance.  In some cases the IGA system actually takes on all the provisioning duties. 

Also note, the notion of importing data does not necessarily mean making a physical copy of data, although it often does. The notion also supports the idea of virtualization - where the import of identity information is done at run-time.

The Identity Register could be implemented in several ways. Common methods include the use of general-purpose databases, optimized stores such directories i.e., a physical or a virtual directory.

Also shown, is the Principal and Credential Management function. This is intended to include steps needed to originate an identity (such as proofing or vetting) as well as on-going maintenance such as password reset and other credential management activities such as token provisioning. This function includes administrative activities and self-serve activities.

Also noted is the function of propagating selected information further into the ecosystem. This typically occurs when a relying services needs additional information about the users, e.g. for the purpose of access control, or personalization. The relying system makes a copy of the identity data and that is used in the application processes. A complete solution will allow for the full lifecycle including creation, update and eventual deletion of the identity data stored locally.

So far, the provisioning function is restricted to "admin-time".  However, there are some cases where provisioning occurs at run time. 

Not shown here, but sometimes implemented, are provisioning actions that occur on a just-in-time basis. This can happen when additional identity information is passed to a relying service in real-time to support a specific application requirement, possibly including identity attributes. A similar case involves the relying service querying the identity management system in order to acquire attributes.

![Diagram Description automatically generated](resources/provisioning.png){width="6.268055555555556in" height="5.839583333333334in"}

Authentication and sessions
---------------------------

Authentication is the process by which a subject's credentials are used to verify their identity. The Identity Management System checks and verifies credentials that are presented to it. Typically, the Relying Service presents the credentials on behalf of the user and receives an assessment from the IMS regarding the level of certainty that the user is authentic. There are multiple scenarios.

A common pattern is to associate the authentication event with the start of a session. The session is mostly the concern of the relying system. However, it is sometimes desirable to keep the sessions supported by several relying parties in synch. For instance, logging out of one session will terminate concurrent sessions. To do this, often the Identity Management System will act to orchestrate sessions termination. In high security environments, session management must support termination based on real-time identity data such as when a user's entitlements have been modified.

Another important concept is step-up authentication. A session can keep track of the level of assurance of a particular authentication, so when a user requests access to a transaction or application requiring a higher level of identity assurance, the Identity Management System can be prepared to determine the course of action. The detection of the assurance gap and subsequent action could be done at the relying system, but that would end up with a poor user experience if multiple relying systems with step-up needs were in play.

The existence of a centralized point of view about sessions, can be leveraged to support good security practices. For example, if the identity attributes of a user with an active session changes and then contravenes an access control policy the session should terminate, or if session management becomes aware of a terminated account it should end any active session that the user has. This could also occur in advanced scenarios which include external risk facts. See Risk Context below.

![Diagram Description automatically generated](resources/authentication-and-sessions.png){width="6.268055555555556in" height="4.636805555555555in"}

Authorization
-------------

Authorization models are many and diverse. The diagram illustrates two approaches for authorization.

Both approaches typically use subject attributes help determine access. These values may have been provisioned into a local store, in the Provisioning process described above. Or the values can be acquired at run-time from the Identity Management System as shown by the attribute query.

Many relying services perform authorization tasks internally. Often the fine-grained access control required by a protected resource makes this appealing. For instance, a financial management system may maintain a user's entitlements to specific functionality with the application.

Sometimes authorization is a shared resource for many relying services. This design can improve consistency of authorization decisions and supports organizations wishing to include advanced access decisions strategies such as those required by a \"Zero Trust\" access control approach, as described by NIST 800-207. Shared authorization systems typically have a consistent approach to policy such as a standardized policy language.

![Diagram Description automatically generated](resources/authorization-models.png){width="6.268055555555556in" height="5.809027777777778in"}

Access governance
-----------------

Access Governance provides oversight and control over access rights implemented in multiple local or shared authorization systems. These may rely on user attributes such as group memberships or roles stored in an Identity Register.

Typically, governance activities review and may modify the data in one or more of the authorization components in order to effect a change in entitlements.

Access Governance is required in enterprise systems focusing on management of staff (employee/contractor) entitlements. The concept can also apply to customer facing scenarios such as business to business delegated rights or business to customer scenarios where delegation such as power of attorney or other agents are required.

![Diagram Description automatically generated](resources/access-governance.png){width="6.268055555555556in" height="5.809027777777778in"}

Risk Context
------------

Risk context information can be valuable to improve the security of the relying service. External events may be visible to the Identity Management System operator through consortia or vendor packages. In some mutual-support scenarios, it may be possible for the IMS operator to also publish events for the benefit of others, supporting a relying party's risk management requirement.

Events need to be delivered into the Identity Management System so that they can selectively be used to modify the behavior of the authentication function. In some severe scenarios it may be desirable to attach the events to the session management function so that current sessions can be reviewed and terminated if needed.

As shown in the diagram, shared authorization systems may consume risk data as well. For example, an authorization might be denied if the subject\'s recent activity history is outside of normal bounds, possibly indicating a compromised credential. Logically this could happen with local authorization as well, but this is not shown.

The linkage from the IMS Audit Repository illustrates that the Risk Context consumes one or more inputs to the trust algorithm. (See NIST 800-207).

![Diagram Description automatically generated](resources/risk-context.png){width="6.268055555555556in" height="5.815277777777778in"}

Metadata and Discovery
----------------------

Metadata refers to control data that allows the Identity Management System to recognize and trust the Relying Service. The inverse is also true, but the metadata of the Relying System is not shown diagrammatically. This may include information that limits the types of interactions and scope of the data that is exchanged. It can also contain security information to allow the counterparties to authenticate each other. For instance, public key components such as certificates with a common trust root may be used.

Discovery is a service relying parties need to identify where a user's identity data resides. A Discovery service can advise where specific data can be accessed and which end-points are maintained to allow a relying party to query the correct repository for the required information.

![Diagram Description automatically generated](resources/metadata-discovery.png){width="6.268055555555556in" height="4.636805555555555in"}

References
----------

1. ISO/IEC 24760-2:2015(E) Figure C.1 provided the starting point.  ISO/IEC 24760-1 Second edition provided improved naming and granularity (specifically breaking out CSP and Enrolment)

2.  FICAM [[https://playbooks.idmanagement.gov/arch/components/]{.underline}](https://playbooks.idmanagement.gov/arch/components/)

3.  Internet 2 [[https://playbooks.idmanagement.gov/arch/components/]{.underline}](https://playbooks.idmanagement.gov/arch/components/)

4.  NIST Zero Trust [[https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf]{.underline}](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-207.pdf)
