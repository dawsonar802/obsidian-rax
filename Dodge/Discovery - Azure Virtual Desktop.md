
#terraform #azure #avd #virtual #desktop 


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
https://learn.microsoft.com/en-us/azure/developer/terraform/configure-azure-virtual-desktop

## Other

```ad-info
If you're planning on using Azure AD only with [FSLogix Profile Container](https://learn.microsoft.com/en-us/fslogix/configure-profile-container-tutorial), you will need to [store profiles on Azure Files](https://learn.microsoft.com/en-us/azure/virtual-desktop/create-profile-container-azure-ad), which is currently in public preview. In this scenario, user accounts must be [hybrid identities](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/whatis-hybrid-identity), which means you'll also need AD DS and [Azure AD Connect](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/whatis-azure-ad-connect). You must create these accounts in AD DS and synchronize them to Azure AD. The service doesn't currently support environments where users are managed with Azure AD and synchronized to Azure AD DS.

```
