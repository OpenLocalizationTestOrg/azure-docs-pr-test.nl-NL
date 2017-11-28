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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="07d05-104">Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken</span><span class="sxs-lookup"><span data-stu-id="07d05-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="07d05-105">Wanneer u een app of een script dat tooaccess resources moet hebt, kunt u een identiteit voor het Hallo-app instellen en Hallo-app met een eigen referenties verifiëren.</span><span class="sxs-lookup"><span data-stu-id="07d05-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="07d05-106">Deze identiteit staat bekend als een service-principal.</span><span class="sxs-lookup"><span data-stu-id="07d05-106">This identity is known as a service principal.</span></span> <span data-ttu-id="07d05-107">Deze aanpak kunt u:</span><span class="sxs-lookup"><span data-stu-id="07d05-107">This approach enables you to:</span></span>

* <span data-ttu-id="07d05-108">Wijs machtigingen toe toohello app identiteit die anders zijn dan uw eigen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="07d05-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="07d05-109">Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo.</span><span class="sxs-lookup"><span data-stu-id="07d05-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="07d05-110">Een certificaat voor verificatie gebruiken bij het uitvoeren van een onbewaakt script.</span><span class="sxs-lookup"><span data-stu-id="07d05-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="07d05-111">Dit onderwerp leest u hoe toouse [Azure PowerShell](/powershell/azure/overview) tooset van alles wat u nodig hebt voor een toepassing toorun onder een eigen referenties en identiteit.</span><span class="sxs-lookup"><span data-stu-id="07d05-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="07d05-112">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="07d05-112">Required permissions</span></span>
<span data-ttu-id="07d05-113">toocomplete in dit onderwerp, moet u voldoende machtigingen in uw Azure Active Directory en uw Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="07d05-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="07d05-114">In het bijzonder moeten kunnen toocreate een app in Azure Active Directory hello, en Hallo service principal tooa rol toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="07d05-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="07d05-115">Hallo gemakkelijkste manier toocheck of uw account de juiste machtigingen heeft, is via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="07d05-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="07d05-116">Zie [controleert u de vereiste machtiging](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="07d05-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="07d05-117">Nu gaan tooa sectie voor verificatie met:</span><span class="sxs-lookup"><span data-stu-id="07d05-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="07d05-118">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="07d05-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="07d05-119">zelf-ondertekend certificaat</span><span class="sxs-lookup"><span data-stu-id="07d05-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="07d05-120">certificaat van certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="07d05-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="07d05-121">PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="07d05-121">PowerShell commands</span></span>

<span data-ttu-id="07d05-122">tooset van een service-principal die u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="07d05-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="07d05-123">Opdracht</span><span class="sxs-lookup"><span data-stu-id="07d05-123">Command</span></span> | <span data-ttu-id="07d05-124">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="07d05-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="07d05-125">Nieuwe AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="07d05-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="07d05-126">Hiermee maakt u een Azure Active Directory service-principal</span><span class="sxs-lookup"><span data-stu-id="07d05-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="07d05-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="07d05-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="07d05-128">Wordt toegewezen Hallo RBAC-rol toohello opgegeven principal opgegeven, op Hallo opgegeven bereik.</span><span class="sxs-lookup"><span data-stu-id="07d05-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="07d05-129">Service-principal maken met wachtwoord</span><span class="sxs-lookup"><span data-stu-id="07d05-129">Create service principal with password</span></span>

<span data-ttu-id="07d05-130">toocreate gebruiken voor een service-principal met de rol van Inzender Hallo voor uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="07d05-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="07d05-131">Hallo voorbeeld modus ingeschakeld gedurende 20 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d05-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="07d05-132">Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "</span><span class="sxs-lookup"><span data-stu-id="07d05-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="07d05-133">Hallo volgende script kunt u een scope dan Hallo standaardabonnement toospecify en pogingen Hallo roltoewijzing als er een fout optreedt:</span><span class="sxs-lookup"><span data-stu-id="07d05-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

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

<span data-ttu-id="07d05-134">Enkele items toonote over Hallo script:</span><span class="sxs-lookup"><span data-stu-id="07d05-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="07d05-135">toogrant hello identiteit toegang toohello standaardabonnement, hoeft u geen tooprovide ResourceGroup of SubscriptionId parameters.</span><span class="sxs-lookup"><span data-stu-id="07d05-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="07d05-136">Hallo ResourceGroup parameter opgeven wanneer u toolimit Hallo bereik van Hallo rol toewijzing tooa-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="07d05-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="07d05-137">In dit voorbeeld voegt u Hallo service principal toohello de rol van Inzender.</span><span class="sxs-lookup"><span data-stu-id="07d05-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="07d05-138">Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="07d05-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="07d05-139">Hallo script modus ingeschakeld gedurende 15 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d05-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="07d05-140">Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "</span><span class="sxs-lookup"><span data-stu-id="07d05-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="07d05-141">Als u toogrant Hallo principal toegang toomore serviceabonnementen of resourcegroepen nodig hebt, voert u Hallo `New-AzureRMRoleAssignment` cmdlet opnieuw met een verschillend bereik.</span><span class="sxs-lookup"><span data-stu-id="07d05-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="07d05-142">Geef referenties op via PowerShell</span><span class="sxs-lookup"><span data-stu-id="07d05-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="07d05-143">Nu moet u toolog in als Hallo toepassing tooperform bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="07d05-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="07d05-144">Gebruik voor gebruikersnaam Hallo Hallo `ApplicationId` die u hebt gemaakt voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="07d05-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="07d05-145">Gebruik voor Hallo wachtwoord, hello een die hebt opgegeven toen u Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="07d05-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="07d05-146">Hallo tenant-ID is niet gevoelige, dus u deze rechtstreeks in uw script insluiten kunt.</span><span class="sxs-lookup"><span data-stu-id="07d05-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="07d05-147">Als u tooretrieve hello tenant-ID nodig hebt, gebruikt:</span><span class="sxs-lookup"><span data-stu-id="07d05-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="07d05-148">Service-principal maken met een zelf-ondertekend certificaat</span><span class="sxs-lookup"><span data-stu-id="07d05-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="07d05-149">toocreate gebruiken voor een service-principal met een zelfondertekend certificaat en de rol van Inzender Hallo voor uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="07d05-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="07d05-150">Hallo voorbeeld modus ingeschakeld gedurende 20 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d05-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="07d05-151">Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "</span><span class="sxs-lookup"><span data-stu-id="07d05-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="07d05-152">Hallo volgende script kunt u een scope dan Hallo standaardabonnement toospecify, en pogingen Hallo roltoewijzing als er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="07d05-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="07d05-153">U moet Azure PowerShell 2.0 op Windows 10 of Windows Server 2016 hebben.</span><span class="sxs-lookup"><span data-stu-id="07d05-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="07d05-154">Enkele items toonote over Hallo script:</span><span class="sxs-lookup"><span data-stu-id="07d05-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="07d05-155">toogrant hello identiteit toegang toohello standaardabonnement, hoeft u geen tooprovide ResourceGroup of SubscriptionId parameters.</span><span class="sxs-lookup"><span data-stu-id="07d05-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="07d05-156">Hallo ResourceGroup parameter opgeven wanneer u toolimit Hallo bereik van Hallo rol toewijzing tooa-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="07d05-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="07d05-157">In dit voorbeeld voegt u Hallo service principal toohello de rol van Inzender.</span><span class="sxs-lookup"><span data-stu-id="07d05-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="07d05-158">Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="07d05-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="07d05-159">Hallo script modus ingeschakeld gedurende 15 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d05-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="07d05-160">Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "</span><span class="sxs-lookup"><span data-stu-id="07d05-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="07d05-161">Als u toogrant Hallo principal toegang toomore serviceabonnementen of resourcegroepen nodig hebt, voert u Hallo `New-AzureRMRoleAssignment` cmdlet opnieuw met een verschillend bereik.</span><span class="sxs-lookup"><span data-stu-id="07d05-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="07d05-162">Als u **hebben geen Windows 10 of Windows Server 2016 Technical Preview**, moet u toodownload hello [zelf-ondertekend certificaat generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) van Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="07d05-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="07d05-163">Pak de inhoud en Hallo cmdlet, u moet importeren.</span><span class="sxs-lookup"><span data-stu-id="07d05-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="07d05-164">In Hallo-script vervangen door de volgende twee regels toogenerate Hallo certificaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="07d05-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="07d05-165">Geef het certificaat via automatische PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="07d05-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="07d05-166">Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app.</span><span class="sxs-lookup"><span data-stu-id="07d05-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="07d05-167">Een tenant is een exemplaar van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d05-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="07d05-168">Als u slechts één abonnement hebt, kunt u het volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="07d05-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="07d05-169">Hallo-toepassing-ID en tenant-ID kunnen niet gevoelige, dus u kunt ze rechtstreeks insluiten in uw script.</span><span class="sxs-lookup"><span data-stu-id="07d05-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="07d05-170">Als u tooretrieve hello tenant-ID nodig hebt, gebruikt:</span><span class="sxs-lookup"><span data-stu-id="07d05-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="07d05-171">Als u tooretrieve Hallo toepassings-ID nodig hebt, gebruikt:</span><span class="sxs-lookup"><span data-stu-id="07d05-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="07d05-172">Service-principal maken met het certificaat van certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="07d05-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="07d05-173">toouse een certificaat is uitgegeven door een certificeringsinstantie toocreate service-principal, gebruik Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="07d05-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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

<span data-ttu-id="07d05-174">Enkele items toonote over Hallo script:</span><span class="sxs-lookup"><span data-stu-id="07d05-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="07d05-175">Toegang is binnen het bereik toohello abonnement.</span><span class="sxs-lookup"><span data-stu-id="07d05-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="07d05-176">In dit voorbeeld voegt u Hallo service principal toohello de rol van Inzender.</span><span class="sxs-lookup"><span data-stu-id="07d05-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="07d05-177">Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="07d05-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="07d05-178">Hallo script modus ingeschakeld gedurende 15 seconden tooallow enige tijd Hallo nieuwe service principal toopropagate in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d05-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="07d05-179">Als uw script niet lang genoeg wacht, ziet u een foutbericht waarin wordt gemeld: ' PrincipalNotFound: Principal {id} bestaat niet in de directory Hallo. "</span><span class="sxs-lookup"><span data-stu-id="07d05-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="07d05-180">Als u toogrant Hallo principal toegang toomore serviceabonnementen of resourcegroepen nodig hebt, voert u Hallo `New-AzureRMRoleAssignment` cmdlet opnieuw met een verschillend bereik.</span><span class="sxs-lookup"><span data-stu-id="07d05-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="07d05-181">Geef het certificaat via automatische PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="07d05-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="07d05-182">Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app.</span><span class="sxs-lookup"><span data-stu-id="07d05-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="07d05-183">Een tenant is een exemplaar van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07d05-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="07d05-184">Hallo-toepassing-ID en tenant-ID kunnen niet gevoelige, dus u kunt ze rechtstreeks insluiten in uw script.</span><span class="sxs-lookup"><span data-stu-id="07d05-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="07d05-185">Als u tooretrieve hello tenant-ID nodig hebt, gebruikt:</span><span class="sxs-lookup"><span data-stu-id="07d05-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="07d05-186">Als u tooretrieve Hallo toepassings-ID nodig hebt, gebruikt:</span><span class="sxs-lookup"><span data-stu-id="07d05-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="07d05-187">Referenties wijzigen</span><span class="sxs-lookup"><span data-stu-id="07d05-187">Change credentials</span></span>

<span data-ttu-id="07d05-188">toochange hello referenties voor een AD-app, hetzij vanwege een beveiligingsinbreuk of een vervaldatum referentie gebruiken Hallo [verwijderen AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) en [nieuw AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="07d05-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="07d05-189">tooremove alle Hallo referenties voor een toepassing gebruiken:</span><span class="sxs-lookup"><span data-stu-id="07d05-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="07d05-190">een wachtwoord, tooadd gebruiken:</span><span class="sxs-lookup"><span data-stu-id="07d05-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="07d05-191">tooadd de waarde van een certificaat, wordt er een zelfondertekend certificaat maken zoals in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="07d05-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="07d05-192">Vervolgens gebruikt:</span><span class="sxs-lookup"><span data-stu-id="07d05-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="07d05-193">Toegang tot het token toosimplify aanmelden opslaan</span><span class="sxs-lookup"><span data-stu-id="07d05-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="07d05-194">tooavoid hello service principal referenties telkens wanneer het toolog in, kunt u het toegangstoken Hallo opslaan.</span><span class="sxs-lookup"><span data-stu-id="07d05-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="07d05-195">toouse hello huidige toegangstoken in een latere sessie, Hallo profiel opslaan.</span><span class="sxs-lookup"><span data-stu-id="07d05-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="07d05-196">Hallo profiel openen en bekijk de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="07d05-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="07d05-197">U ziet dat deze een toegangstoken bevat.</span><span class="sxs-lookup"><span data-stu-id="07d05-197">Notice that it contains an access token.</span></span> <span data-ttu-id="07d05-198">In plaats van handmatig opnieuw in te loggen, moet u gewoon Hallo profiel laden.</span><span class="sxs-lookup"><span data-stu-id="07d05-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="07d05-199">Hallo toegangstoken is verlopen, zodat u met behulp van een opgeslagen profiel werkt alleen voor zolang Hallo token geldig is.</span><span class="sxs-lookup"><span data-stu-id="07d05-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="07d05-200">U kunt ook de REST-bewerkingen van het PowerShell-toolog in aanroepen.</span><span class="sxs-lookup"><span data-stu-id="07d05-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="07d05-201">U kunt van antwoord Hallo-verificatie, Hallo toegangstoken voor gebruik met andere bewerkingen ophalen.</span><span class="sxs-lookup"><span data-stu-id="07d05-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="07d05-202">Zie voor een voorbeeld van het toegangstoken Hallo ophalen door aan te roepen REST-bewerkingen [genereren van een Token toegang](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="07d05-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="07d05-203">Fouten opsporen</span><span class="sxs-lookup"><span data-stu-id="07d05-203">Debug</span></span>

<span data-ttu-id="07d05-204">Hallo volgende fouten bij het maken van een service-principal kunnen optreden:</span><span class="sxs-lookup"><span data-stu-id="07d05-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="07d05-205">**'Authentication_Unauthorized'** of **'geen abonnement gevonden in de context van Hallo'.**</span><span class="sxs-lookup"><span data-stu-id="07d05-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="07d05-206">-U hebt deze fout te zien wanneer uw account geen Hallo [vereist machtigingen](#required-permissions) op Hallo Azure Active Directory tooregister een app.</span><span class="sxs-lookup"><span data-stu-id="07d05-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="07d05-207">Normaal gesproken u deze fout te zien wanneer alleen admin gebruikers in uw Azure Active Directory apps registreren kunnen en uw account niet een beheerder is. Vraag uw beheerder tooeither tooan beheerdersrol of tooenable gebruikers tooregister apps toewijzen.</span><span class="sxs-lookup"><span data-stu-id="07d05-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="07d05-208">Uw account **"heeft geen autorisatie tooperform actie 'Microsoft.Authorization/roleAssignments/write' bereik/subscriptions / {guid}."**  -Deze fout te zien wanneer uw account geen voldoende machtigingen tooassign tooan identiteit van een rol.</span><span class="sxs-lookup"><span data-stu-id="07d05-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="07d05-209">Vraag uw beheerder abonnement tooadd u tooUser toegang beheerdersrol.</span><span class="sxs-lookup"><span data-stu-id="07d05-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="07d05-210">Voorbeeldtoepassingen</span><span class="sxs-lookup"><span data-stu-id="07d05-210">Sample applications</span></span>
<span data-ttu-id="07d05-211">Zie voor informatie over logboekregistratie in als de toepassing hello via verschillende platforms:</span><span class="sxs-lookup"><span data-stu-id="07d05-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="07d05-212">.NET</span><span class="sxs-lookup"><span data-stu-id="07d05-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="07d05-213">Java</span><span class="sxs-lookup"><span data-stu-id="07d05-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="07d05-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="07d05-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="07d05-215">Python</span><span class="sxs-lookup"><span data-stu-id="07d05-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="07d05-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="07d05-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="07d05-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07d05-217">Next steps</span></span>
* <span data-ttu-id="07d05-218">Zie voor gedetailleerde stappen voor het integreren van een toepassing in Azure voor het beheren van resources [Developer's guide tooauthorization Hello Azure Resource Manager-API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="07d05-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="07d05-219">Zie voor een meer gedetailleerde uitleg van toepassingen en service-principals [toepassingsobjecten en Service-Principal objecten](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="07d05-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="07d05-220">Zie voor meer informatie over Azure Active Directory-verificatie, [verificatie scenario's voor Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="07d05-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="07d05-221">Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd toousers [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="07d05-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

