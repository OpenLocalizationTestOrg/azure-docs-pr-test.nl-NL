---
title: aaaCreate identiteit voor Azure-app met PowerShell | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure PowerShell toocreate een Azure Active Directory-toepassing en service-principal en verleen deze toegang hebben tot tooresources via op rollen gebaseerde toegang beheren. Er wordt weergegeven hoe tooauthenticate toepassing met een wachtwoord of certificaat.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken

Wanneer u een app of een script dat tooaccess resources moet hebt, kunt u een identiteit voor het Hallo-app instellen en Hallo-app met een eigen referenties verifiëren. Deze identiteit staat bekend als een service-principal. Deze aanpak kunt u:

* Wijs machtigingen toe toohello app identiteit die anders zijn dan uw eigen machtigingen. Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo.
* Een certificaat voor verificatie gebruiken bij het uitvoeren van een onbewaakt script.

Dit onderwerp leest u hoe toouse [Azure PowerShell](/powershell/azure/overview) tooset van alles wat u nodig hebt voor een toepassing toorun onder een eigen referenties en identiteit.

## <a name="required-permissions"></a>Vereiste machtigingen
toocomplete in dit onderwerp, moet u voldoende machtigingen in uw Azure Active Directory en uw Azure-abonnement hebben. In het bijzonder moeten kunnen toocreate een app in Azure Active Directory hello, en Hallo service principal tooa rol toe te wijzen. 

Hallo gemakkelijkste manier toocheck of uw account de juiste machtigingen heeft, is via Hallo-portal. Zie [controleert u de vereiste machtiging](resource-group-create-service-principal-portal.md#required-permissions).

Nu gaan tooa sectie voor verificatie met:

* [wachtwoord](#create-service-principal-with-password)
* [zelf-ondertekend certificaat](#create-service-principal-with-self-signed-certificate)
* [certificaat van certificeringsinstantie](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>PowerShell-opdrachten

tooset van een service-principal die u gebruikt:

| Opdracht | Beschrijving |
| ------- | ----------- | 
| [Nieuwe AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Hiermee maakt u een Azure Active Directory service-principal |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Wordt toegewezen Hallo RBAC-rol toohello opgegeven principal opgegeven, op Hallo opgegeven bereik. |


## <a name="create-service-principal-with-password"></a>Service-principal maken met wachtwoord

toocreate gebruiken voor een service-principal met de rol van Inzender Hallo voor uw abonnement: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

Hallo voorbeeld modus ingeschakeld gedurende 20 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory. Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "

Hallo volgende script kunt u een scope dan Hallo standaardabonnement toospecify en pogingen Hallo roltoewijzing als er een fout optreedt:

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Enkele items toonote over Hallo script:

* toogrant hello identiteit toegang toohello standaardabonnement, hoeft u geen tooprovide ResourceGroup of SubscriptionId parameters.
* Hallo ResourceGroup parameter opgeven wanneer u toolimit Hallo bereik van Hallo rol toewijzing tooa-resourcegroep.
*  In dit voorbeeld voegt u Hallo service principal toohello de rol van Inzender. Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).
* Hallo script modus ingeschakeld gedurende 15 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory. Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "
* Als u toogrant Hallo principal toegang toomore serviceabonnementen of resourcegroepen nodig hebt, voert u Hallo `New-AzureRMRoleAssignment` cmdlet opnieuw met een verschillend bereik.


### <a name="provide-credentials-through-powershell"></a>Geef referenties op via PowerShell
Nu moet u toolog in als Hallo toepassing tooperform bewerkingen. Gebruik voor gebruikersnaam Hallo Hallo `ApplicationId` die u hebt gemaakt voor de toepassing hello. Gebruik voor Hallo wachtwoord, hello een die hebt opgegeven toen u Hallo-account. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

Hallo tenant-ID is niet gevoelige, dus u deze rechtstreeks in uw script insluiten kunt. Als u tooretrieve hello tenant-ID nodig hebt, gebruikt:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Service-principal maken met een zelf-ondertekend certificaat

toocreate gebruiken voor een service-principal met een zelfondertekend certificaat en de rol van Inzender Hallo voor uw abonnement: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

Hallo voorbeeld modus ingeschakeld gedurende 20 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory. Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "

Hallo volgende script kunt u een scope dan Hallo standaardabonnement toospecify, en pogingen Hallo roltoewijzing als er een fout optreedt. U moet Azure PowerShell 2.0 op Windows 10 of Windows Server 2016 hebben.

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Enkele items toonote over Hallo script:

* toogrant hello identiteit toegang toohello standaardabonnement, hoeft u geen tooprovide ResourceGroup of SubscriptionId parameters.
* Hallo ResourceGroup parameter opgeven wanneer u toolimit Hallo bereik van Hallo rol toewijzing tooa-resourcegroep.
* In dit voorbeeld voegt u Hallo service principal toohello de rol van Inzender. Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).
* Hallo script modus ingeschakeld gedurende 15 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory. Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "
* Als u toogrant Hallo principal toegang toomore serviceabonnementen of resourcegroepen nodig hebt, voert u Hallo `New-AzureRMRoleAssignment` cmdlet opnieuw met een verschillend bereik.

Als u **hebben geen Windows 10 of Windows Server 2016 Technical Preview**, moet u toodownload hello [zelf-ondertekend certificaat generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) van Microsoft Script Center. Pak de inhoud en Hallo cmdlet, u moet importeren.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
In Hallo-script vervangen door de volgende twee regels toogenerate Hallo certificaat Hallo.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Geef het certificaat via automatische PowerShell-script
Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app. Een tenant is een exemplaar van Azure Active Directory. Als u slechts één abonnement hebt, kunt u het volgende gebruiken:

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

Hallo-toepassing-ID en tenant-ID kunnen niet gevoelige, dus u kunt ze rechtstreeks insluiten in uw script. Als u tooretrieve hello tenant-ID nodig hebt, gebruikt:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Als u tooretrieve Hallo toepassings-ID nodig hebt, gebruikt:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Service-principal maken met het certificaat van certificeringsinstantie
toouse een certificaat is uitgegeven door een certificeringsinstantie toocreate service-principal, gebruik Hallo script volgen:

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Enkele items toonote over Hallo script:

* Toegang is binnen het bereik toohello abonnement.
* In dit voorbeeld voegt u Hallo service principal toohello de rol van Inzender. Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).
* Hallo script modus ingeschakeld gedurende 15 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory. Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "
* Als u toogrant Hallo principal toegang toomore serviceabonnementen of resourcegroepen nodig hebt, voert u Hallo `New-AzureRMRoleAssignment` cmdlet opnieuw met een verschillend bereik.

### <a name="provide-certificate-through-automated-powershell-script"></a>Geef het certificaat via automatische PowerShell-script
Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app. Een tenant is een exemplaar van Azure Active Directory.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

Hallo-toepassing-ID en tenant-ID kunnen niet gevoelige, dus u kunt ze rechtstreeks insluiten in uw script. Als u tooretrieve hello tenant-ID nodig hebt, gebruikt:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Als u tooretrieve Hallo toepassings-ID nodig hebt, gebruikt:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Referenties wijzigen

toochange hello referenties voor een AD-app, hetzij vanwege een beveiligingsinbreuk of een vervaldatum referentie gebruiken Hallo [verwijderen AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) en [nieuw AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.

tooremove alle Hallo referenties voor een toepassing gebruiken:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

een wachtwoord, tooadd gebruiken:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd de waarde van een certificaat, wordt er een zelfondertekend certificaat maken zoals in dit onderwerp. Vervolgens gebruikt:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Toegang tot het token toosimplify aanmelden opslaan
tooavoid hello service principal referenties telkens wanneer het toolog in, kunt u het toegangstoken Hallo opslaan.

toouse hello huidige toegangstoken in een latere sessie, Hallo profiel opslaan.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Hallo profiel openen en bekijk de inhoud ervan. U ziet dat deze een toegangstoken bevat. In plaats van handmatig opnieuw in te loggen, moet u gewoon Hallo profiel laden.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> Hallo toegangstoken is verlopen, zodat u met behulp van een opgeslagen profiel werkt alleen voor zolang Hallo token geldig is.
>  

U kunt ook de REST-bewerkingen van het PowerShell-toolog in aanroepen. U kunt van antwoord Hallo-verificatie, Hallo toegangstoken voor gebruik met andere bewerkingen ophalen. Zie voor een voorbeeld van het toegangstoken Hallo ophalen door aan te roepen REST-bewerkingen [genereren van een Token toegang](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Fouten opsporen

Hallo volgende fouten bij het maken van een service-principal kunnen optreden:

* **'Authentication_Unauthorized'** of **'geen abonnement gevonden in de context van Hallo'.** -U hebt deze fout te zien wanneer uw account geen Hallo [vereist machtigingen](#required-permissions) op Hallo Azure Active Directory tooregister een app. Normaal gesproken u deze fout te zien wanneer alleen admin gebruikers in uw Azure Active Directory apps registreren kunnen en uw account niet een beheerder is. Vraag uw beheerder tooeither tooan beheerdersrol of tooenable gebruikers tooregister apps toewijzen.

* Uw account **"heeft geen autorisatie tooperform actie 'Microsoft.Authorization/roleAssignments/write' bereik/subscriptions / {guid}."**  -Deze fout te zien wanneer uw account geen voldoende machtigingen tooassign tooan identiteit van een rol. Vraag uw beheerder abonnement tooadd u tooUser toegang beheerdersrol.

## <a name="sample-applications"></a>Voorbeeldtoepassingen
Zie voor informatie over logboekregistratie in als de toepassing hello via verschillende platforms:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Volgende stappen
* Zie voor gedetailleerde stappen voor het integreren van een toepassing in Azure voor het beheren van resources [Developer's guide tooauthorization Hello Azure Resource Manager-API](resource-manager-api-authentication.md).
* Zie voor een meer gedetailleerde uitleg van toepassingen en service-principals [toepassingsobjecten en Service-Principal objecten](../active-directory/active-directory-application-objects.md). 
* Zie voor meer informatie over Azure Active Directory-verificatie, [verificatie scenario's voor Azure AD](../active-directory/active-directory-authentication-scenarios.md).
* Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd toousers [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).

