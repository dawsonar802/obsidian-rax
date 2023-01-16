
#terraform #azure #avd #virtual #desktop 

## Overview

### Terminology
https://learn.microsoft.com/en-us/azure/virtual-desktop/environment-setup

#### Host Pool
A host pool is a collection of Azure virtual machines that register to Azure Virtual Desktop as session hosts when you run the Azure Virtual Desktop agent. All session host virtual machines in a host pool should be sourced from the same image for a consistent user experience. You control the resources published to users through app groups.

A host pool can be one of two types:

-   Personal, where each session host is assigned to an individual user. Personal host pools provide dedicated desktops to end-users that optimize environments for performance and data separation.
-   Pooled, where user sessions can be load balanced to any session host in the host pool. There can be multiple different users on a single session host at the same time. Pooled host pools provide a shared remote experience to end-users, which ensures lower costs and greater efficiency.

#### App groups
An app group is a logical grouping of applications installed on session hosts in the host pool.

An app group can be one of two types:

-   RemoteApp, where users access the RemoteApps you individually select and publish to the app group. Available with pooled host pools only.
-   Desktop, where users access the full desktop. Available with pooled or personal host pools.

#### Workspaces
A workspace is a logical grouping of application groups in Azure Virtual Desktop. Each Azure Virtual Desktop application group must be associated with a workspace for users to see the remote apps and desktops published to them.

#### User Sessions
 - Active - A user session is considered "active" when a user signs in and connects to their remote app or desktop resource.
 - Disconnected - A disconnected user session is an inactive session that the user hasn't signed out of yet. When a user closes the remote session window without signing out, the session becomes disconnected. When a user reconnects to their remote resources, they'll be redirected to their disconnected session on the session host they were working on. At this point, the disconnected session becomes an active session again.
 - Pending - A pending user session is a placeholder session that reserves a spot on the load-balanced virtual machine for the user. Because the sign-in process can take anywhere from 30 seconds to five minutes depending on the user profile, this placeholder session ensures that the user won't be kicked out of their session if another user completes their sign-in process first.


## Requirements
https://learn.microsoft.com/en-us/azure/virtual-desktop/prerequisites

### Network
https://learn.microsoft.com/en-us/azure/virtual-desktop/prerequisites#network

## Limitations
- The user account must exist in the Azure AD tenant you use for Azure Virtual Desktop. Azure Virtual Desktop doesn't support [B2B](https://learn.microsoft.com/en-us/azure/active-directory/external-identities/what-is-b2b), [B2C](https://learn.microsoft.com/en-us/azure/active-directory-b2c/overview), or personal Microsoft accounts.
- When using hybrid identities, either the UserPrincipalName (UPN) or the Security Identifier (SID) must match across Active Directory Domain Services and Azure Active Directory. For more information, see [Supported identities and authentication methods](https://learn.microsoft.com/en-us/azure/virtual-desktop/authentication#hybrid-identity).
- If you're joining session hosts to an AD DS domain and you want to manage them using [Intune](https://learn.microsoft.com/en-us/mem/intune/fundamentals/what-is-intune), you'll need to configure [Azure AD Connect](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/whatis-azure-ad-connect) to enable [hybrid Azure AD join](https://learn.microsoft.com/en-us/azure/active-directory/devices/hybrid-azuread-join-plan).

## Deployment

### Deployment Params
-   Domain name, if using AD DS or Azure AD DS.
-   Credentials to join session hosts to the domain.
-   Organizational Unit (OU), which is an optional parameter that lets you place session hosts in the desired OU at deployment time.

### Terraform Deployment
- Configure AVD: https://learn.microsoft.com/en-us/azure/developer/terraform/configure-azure-virtual-desktop
- Create Session Host: https://learn.microsoft.com/en-us/azure/developer/terraform/create-avd-session-host
- Azure Files: https://learn.microsoft.com/en-us/azure/developer/terraform/create-avd-azure-files-storage
- 

## Security 
https://learn.microsoft.com/en-us/azure/virtual-desktop/security-guide

## Other

```ad-info
If you're planning on using Azure AD only with [FSLogix Profile Container](https://learn.microsoft.com/en-us/fslogix/configure-profile-container-tutorial), you will need to [store profiles on Azure Files](https://learn.microsoft.com/en-us/azure/virtual-desktop/create-profile-container-azure-ad), which is currently in public preview. In this scenario, user accounts must be [hybrid identities](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/whatis-hybrid-identity), which means you'll also need AD DS and [Azure AD Connect](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/whatis-azure-ad-connect). You must create these accounts in AD DS and synchronize them to Azure AD. The service doesn't currently support environments where users are managed with Azure AD and synchronized to Azure AD DS.

```
