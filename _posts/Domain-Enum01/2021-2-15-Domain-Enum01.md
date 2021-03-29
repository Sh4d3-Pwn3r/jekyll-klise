---
author: Sh4d3
title: Active Directory (Domain Enumeration) 01
discreption: In this part we will talk about Domain Enumeration
featured-img: apple-icon.png
categories: [Network, Active-Directory] 
tags: [Network, Active-Directory]
---
<img src="https://i.imgur.com/1iYVeY0.png" alt="Domain-Enum01">

In this part we will discus Domain Enumration using PowerView or ADModule and I'll use PowerView.

let's import it

```console
PS C:\Users\adlab> . .\PowerView.ps1
```

## Domain Enumeration.

### Get current Domain: 

```console
PS C:\Users\adlab> Get-NetDomain
```

### Get other Domains:

```console
PS C:\Users\adlab> Get-NetDomain -Domain <Domain name>
```

### Get Domain SID for current Domain:

```console
PS C:\Users\adlab> Get-DomainSID
```

### Get current Domain Controller:

```console
PS C:\Users\adlab> Get-NetDomainController
```

### Get Domain controller for another Domain:

```console
PS C:\Users\adlab> Get-NetDomainConroller -Domain <Domain Name>
```

### Get Domain Policy:

```console
PS C:\Users\adlab> Get-DomainPolicy
```

## User Enumertation.

### Get list of users in current Domain with all properties:

```console
PS C:\Users\adlab> Get-NetUser
```

### And we can Filter the result to get only Names of the Users: 

```console
PS C:\Users\adlab> Get-NetUser | select cn
```

### Get info of the Specific User:

```console
PS C:\Users\adlab> Get-NetUser -SamAccountName <The name of User>
```

### Get User Property:

```console
PS C:\Users\adlab> Get-UserProperty
```

### Get Last password change:

```console
PS C:\Users\adlab> Get-UserProperty -Properties pwdlastset
```

### Get a particular String in a user's attributes:

```console
PS C:\Users\adlab> Find-UserField -SearchField Description -SearchTerm "password"
```

```console
sameaccountname        Description
---------------        -----------
SQL Service my pass is : MYpassword123$ 
```
###  Get activity logged users on a machine (needs local admin rights on the target):

```console
PS C:\Users\adlab> Get-NetLoggedon -ComputerName <servername>
```

### To Get list of names of computers in current Domain: 

```console
PS C:\Users\adlab> Get-NetComputer
```
### Get more Data about Computers in Current Domain:

```console
PS C:\Users\adlab> Get-NetComputer -FullData
```
### To know which machines are alive or not:

```console
PS C:\Users\adlab> Get-NetComputer -ping
```
### Get Groups for current Domain:

```console
PS C:\Users\adlab> Get-NetGroup
```
### Get Groups for specific Domain:

```console
PS C:\Users\adlab> Get-NetGroup -Domain <targetdoamin>
```
### Get more Data about Groups for Current Domain:

```console
PS C:\Users\adlab> Get-NetGroup -FullData
```
### Get All Groups in the Domain containing the word "admin" :

```console
PS C:\Users\adlab> Get-NetGroup *admin*
```
### Get all members of the Domain Admins Group:

```console
PS C:\Users\adlab> Get-NetGroupMember -GroupName 'Domain Admins'
```
### Get list of membership on a machine (needs administrator priv on non DC machine) :

```console
PS C:\Users\adlab> Get-NetLocalGroup -ComputerName <dcname>
```
### Get list of all local Groups on a machine (needs administrator priv on non DC machine) :

```console
PS C:\Users\adlab> Get-NetLocalGroup -ComputerName <dcname> -ListGroups
```
### Get Shares files in current Domain:

```console
PS C:\Users\adlab> Invoke-ShareFinder -verbose
```
### Get sensitive files on computers in current Domain:

```console
PS C:\Users\adlab> Invoke-FileFinder -verbose
```
### Get all fileservers in current Domain:

```console
PS C:\Users\adlab> Get-NetFileserver -verbose
```

notice :: if you do not know what is GPO go to introduction of Active Directory you will get it there.

### Get list of GPO in current domain: 

```console
PS C:\Users\adlab> Get-NetGPO
```

### Filter the result to get only the Group policy:

```console
PS C:\Users\adlab> Get-NetGPO | select displayname
```

### Get list of GPO for specific domain: 

```console
PS C:\Users\adlab> Get-NetGPO -ComputerName <ComputerName>
```

And there is a tool in PowerView called (gpresult)
It display the resultant set of policy information for a target user and computer,
and we will use pareameter '/R' for display SRoP summary data and also we can use too '/v' parameter to display verbose information of the domain

```console
PS C:\Users\adlab> gpresult /R /V
```
### Get restricted groups: 

```console
PS C:\Users\adlab> Get-NetGPOGroup
```
### Get users which are in local Group of machine using GPO:

```console
PS C:\Users\adlab> Find-GPOComputer -ComputerName <domainname>
```
### Get machines where the given user is member of a specific group:

```console
PS C:\Users\adlab> Find-GPOLocation -UserName <username> -verbose
```
### Get OU in a Domain:
 
```console
PS C:\Users\adlab> Get-NetOU -FullData
```
### Get GPO applied on an OU using gplink:

```console
PS C:\Users\adlab> GetNetGPO -GPOname "gplink" 
```

## Enumeerate ACLs:

### Get ACLs associated with specific object:

```console
PS C:\Users\adlab> Get-ObjectAcl -SamAccountName <domainname> -ResolveGUIDs
```

### Get a list of all Domain trusts for the cuurent Domain:

```console
PS C:\Users\adlab> Get-NetDomainTrusts
```

### Get Details about the current Forest:

```console
PS C:\Users\adlab> Get-NetForest
```

### Get All domains in the current Forest

```console
PS C:\Users\adlab> Get-NetForestDomain
```

*### Get all global cataloges for the current Forest:

```console
PS C:\Users\adlab> Get-NetForestCatalog
```

### Get Trusts of the Forest:

```console
PS C:\Users\adlab> Get-NetForestTrust
```

### Get a list of all Domain trusts for the cuurent Domain:

```console
PS C:\Users\adlab> Get-NetDomainTrusts
```

### Get all machines on the current domain that the current user has local admin access:

```console
PS C:\Users\adlab> Find-LocalAdminAccess -Verbose
```

There is another way if ports like (RPC, SMB) used by Find-LocalAdminAccess are blocked , we can done it using remote administrator tools like WMI and PowerShell remoting.

```console
PS C:\Users\adlab> . .\Find-WMILocalAdminAccess.ps1
```

```console
PS C:\Users\adlab> Find-WMILocalAdminAccess
```

### Get Computers where a domain admin has sessions:

```console
PS C:\Users\adlab> Invoke-UserHunter
```

### To confirm admin access:

```console
PS C:\Users\adlab> Invoke-UserHunter -CheckAccess
```

### Get computers that domain admin looged in:

```console
PS C:\Users\adlab> Invoke-UserHunter -Stealth
```

know we will talk about Defending part and have a look at most lethal enumeration techniques : user hunting.

Netcease : is an script which changes permission on the NetSessionEnum method by removing permission for Authenticated users group.

This script fails many of attacker's session enumeration.

```console
PS C:\Users\adlab> . .\NetCease.ps1
```

There is another interesting script from the same auther is SAMRi10 which hardens Windows10 and windows server 2016 against enumertion which uses SAMAR protocol like (net.exe)

### Enumeration Using BloodHound:

Using powershell module ingestor

```console
PS C:\Users\adlab> . .\SharpHound.ps1
```

```console
PS C:\Users\adlab> Invoke-BloodHound -CollectionMethod All
```

Using powershell module ingestor

```console
PS C:\Users\adlab> .\SharpHound.exe -CollectionMethod All
```

And now we finish this sieres (Active Directory Enumeration) in the next sieres we will talk about Local Privilege Escalation part , I hope you enjoy reading .. see you <3.



