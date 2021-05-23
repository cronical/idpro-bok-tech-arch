# Technical Architecture Model
## Abstract
This document provides a model to organize the presentation of technical details associated with various implementations of the architectural concepts.  This article provides the set of generic components which are exemplified below.  It is a restatement/extension of the ISO framing. The extension allows authorization and governance can be included. It is simplified to remove the UML fine points, which will be off putting to the typical reader. 

## Introduction
The following is the basic organization of an identity management system.  It supports multiple relying services.

![](resources/basic-component-dependencies.png)

The most basic function of the identity system is to provide secure storage of the information about identities.  The audit repository is shown since that is perhaps one of the most salient aspects of providing that security.

We will add on more detail during the next several sections.

## Provisioning
Provisioning describes how the data gets into the identity repository and how it flows further on to support authorization decisions.

![](resources/provisioning.png)