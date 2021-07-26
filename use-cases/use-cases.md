Appendix - Use Cases
--------------------

Each article describes a single use-case as implemented in a particular architecture to illustrate a set of components and how they are connected and interact to perform the use-case. These articles are grouped by the functions defined in the model.

To retain context from \"Introduction to IAM Architecture,\" IDPro Body of Knowledge\" the article will indicate what architecture type(s) the use case applies to.

The use-case articles follow a common structure:

-   Use-case name, which will be the title of the article

-   Architecture Type or types Host, Client-Server, N-tier, Hub & Spoke, Remote Access, Cloud Environments

-   Short description

-   Actors, components and connectors included (with a diagram).

    -   The components and connectors refer to the abstract architectural components and their implementations in this use-case.

-   Prerequisites

-   Exposition on how the components work together and some level of detail deemed by the author appropriate for the reader

-   Where to find more information on this and adjacent use-cases

Example: of a use-case. This example is chosen to indicate how constrained these articles are intended to be. There could be quite a few variations on Windows login.

Name: Employee logs in to Windows domain - Kerberos Short Description: Interactive domain login using password (Kerberos) Architecture Type: Client-Server Description: An existing employee logs into the corporate Windows environment with a password. Actors/Components: User (employee), network attached computer running Windows 10, Microsoft Active Directory (IDENTITY REGISTER), Kerberos protocol (AUTHENTICATION)

### List of use-cases

The list of use-case articles is intended to grow over time. \[seeded 5/20/21 - discuss with cmte for more\]

#### Function: Authentication

1.  Employee logs in to Windows domain - Kerberos
3.  Customer logs in from web browser - OpenID Connect

4.  Cloud service authenticates via delegation - SAML

#### Function: Provisioning

1.  Directory absorbs changed people information from HR - LDAP

2.  Directory synchronizes with downstream resource - SCIM

#### Function: Attribute Exchange

1.  Attributes are provided in assertion - SAML

2.  Attributes are requested - OpenID Connect

#### Function: Authorization

1.  File system authorizes access - Windows

2.  Application authorizes based on attributes - custom

3.  Application delegates to policy service - OAuth

4.  Cloud service authorizes based on role assumed from single signon - Cloud