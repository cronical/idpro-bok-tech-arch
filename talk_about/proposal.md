A walk through IDPro's Reference Architecture

This talk will walk through a model, which was published in the IDPro Body of Knowledge in 2021. 

The model has a technical slant, but it necessarily touches on some of the process, legal, and capability dimensions as well.  This talk will s intended to give the reader a set of concepts that can be applied when thinking about identity and access management.  

The model is based on the idea that the management of identities and access can (mostly) be separated from their use.  This concept can apply to distributed systems as well as self-contained systems.  So when you see IAM working together with, say, an application it may mean that these are separate physical systems or it could mean these parts are separate pieces of software running on a single system.

The main goal of this article is allow consistent discussion of more specific use-cases. 

The model started with the ISO/IEC framing [ISO/IEC 24760-1][ISO/IEC 24760-2]. The UML detail was removed for simplicity and the IAM model has been extended so that authorization, governance and risk-control can be included.

Some of the ISO/IEC names have been changed to reflect more common usage. In some cases, the ISO names have been used in a way that is more expansive than their original definition.

In an attempt to adopt the most useful terminology, the model has been reviewed in conjunction with the [FICAM], [Internet 2], [NIST SP-800-63 definitions],  [NIST Zero Trust frameworks], and with the Identity Stack presented at Identiverse 2019.