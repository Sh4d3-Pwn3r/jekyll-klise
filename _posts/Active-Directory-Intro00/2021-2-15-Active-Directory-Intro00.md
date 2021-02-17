---
author: Sh4d3
title: Introduction to Active Directory 00
discreption: Some stuffs you should to know about Active Directory befor Getting deeper
featured-img: apple-icon.png
categories: [Network, Active-Directory]
tags: [Network, Active-Directory]
---
<img src="https://i.imgur.com/JQ4TC12.png" alt="Active-Directory-Intro00">

## Active Directory (AD):

Its a directory service used to managed windows network, 
Store the information on the network and makes it easily available to users and admin.

## Domain Cotroller (DC):

In short the DC is The Admin of the Active Directory that he has an access of all the network,
An explanation for that the role of Domain Controler is to provide authentication and Authorization to different services and users.

## NTDS.DIT:

An Active Directory contains DataBase that has information about users, services and applications, in NTDS.DIT file and this file locate is "%SystemROOT\NTDS%" folder,
Bassed on that it is the most critical file if the AD. 

# AD components you should know.

## Domain: 

Domain is used to group objects together and manage them and it provides an Authentication and Authorization that provides a way to limit the scop of access to the resourses of that domain.

## Trees:

Goup of Domains with the same root and Domains in this group trust each other ex: CORP.local >> x.CORP.local , y.CORP.local.

## Forest:

forest is the highst level of the organization hierarchy and it contains a collection of trees and the trees are connected by trust relationships. 

## Organizational Units (OU):

It is a container holds Active Directory objects like users, groups, and computers, it is the smallest unit in AD, the administrator can assign group policy settings or account permissions, and OU cant contain objects from another Domain. 

## Trust:

Its way to let more than differant Domain can access resources between other in order to gain permission to this resources, there are two type of trusts. 

## Directional Trust:

This trust is easy to understand its just trusting domain to trusted domain.

## Transitive Trust: 

Its a two-way relationship created between parent and child Domains, when we created Domain it shares resources with parent domain by default, the transitive property of equality states that if a = b and b = c, then a = c. transitive trust relationship, if domain A trusts domain B, and domain B trusts domain C, then domain A trusts domain C.

##  Lightweight Directory Access Protocol (LDAP):

AD is based on the Lightweight Directory Access Protocol (LDAP). This protocol provides a common language for clients and servers to speak to one another. 

## SID:

Security Identifer is a unique ID that the Domain Controller uses to identify user, group, computer on a DC network.

## Group Policy (GPO):

The Group Policy provides the ability to manage configuration and changes easily in AD.

## Configuration like:

1. Security settings.
2. Registry-based policy settings.
3. Group policy preferences like startup/shutdown/log-on/log-off/script settings.
4. Software installation.

The `GPO` can be abused for various attacks like privesc, backdoors, persistence etc.

## Access Control Model:

Its the ability of control the proccess to access objects and resourses in Active directory based on. 

1. Access Token : Security context of a process (identity and privs of user).
2. Security Descriptors : SID of the owner, Discretionary ACL (DACL), System ACL (SACL).

## Access Control List (ACL):

Its a list of access control entries (ACE), ACE corresponds to individual permission or audits access, who has permission and what can be done on an object?

## Discretionary ACL (DACL):

The list of permission that who have the permission to access the object.

## System ACL (SACL):

logs success and failure audit messages when an object is accessed.
 

I hope its useful see you in the next part <3 .
