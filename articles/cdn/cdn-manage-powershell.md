---
title: aaaManage Azure CDN met PowerShell | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure PowerShell-cmdlets toomanage Azure CDN.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="91a3c-103">Azure CDN met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="91a3c-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="91a3c-104">PowerShell is een van de meest flexibele methoden toomanage Hallo uw Azure CDN-profielen en -eindpunten.</span><span class="sxs-lookup"><span data-stu-id="91a3c-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="91a3c-105">U kunt PowerShell kunt gebruiken, interactief of door het schrijven van scripts tooautomate beheertaken.</span><span class="sxs-lookup"><span data-stu-id="91a3c-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="91a3c-106">Deze zelfstudie ziet u diverse van Hallo meest algemene taken u kunt uitvoeren met PowerShell toomanage uw Azure CDN-profielen en -eindpunten.</span><span class="sxs-lookup"><span data-stu-id="91a3c-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91a3c-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="91a3c-107">Prerequisites</span></span>
<span data-ttu-id="91a3c-108">toouse PowerShell toomanage uw Azure CDN-profielen en eindpunten, moet u hello Azure PowerShell-module geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="91a3c-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="91a3c-109">toolearn hoe tooinstall Azure PowerShell en verbinding maken met behulp van Hallo tooAzure `Login-AzureRmAccount` cmdlet, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91a3c-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91a3c-110">U moet zich aanmelden met `Login-AzureRmAccount` voordat u Azure PowerShell-cmdlets kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="91a3c-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="91a3c-111">Aanbieding hello Azure CDN-cmdlets</span><span class="sxs-lookup"><span data-stu-id="91a3c-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="91a3c-112">U kunt alle hello Azure CDN-cmdlets met Hallo lijst `Get-Command` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91a3c-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="91a3c-113">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="91a3c-113">Getting help</span></span>
<span data-ttu-id="91a3c-114">U kunt hulp krijgen met een van deze cmdlets met Hallo `Get-Help` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91a3c-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="91a3c-115">`Get-Help`biedt informatie over het gebruik en de syntaxis en eventueel ziet u voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="91a3c-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="91a3c-116">In de lijst bestaande Azure CDN-profielen</span><span class="sxs-lookup"><span data-stu-id="91a3c-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="91a3c-117">Hallo `Get-AzureRmCdnProfile` cmdlet zonder parameters haalt alle uw bestaande CDN-profielen.</span><span class="sxs-lookup"><span data-stu-id="91a3c-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="91a3c-118">Deze uitvoer kan doorgesluisd toocmdlets voor opsomming zijn.</span><span class="sxs-lookup"><span data-stu-id="91a3c-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="91a3c-119">U kunt ook één profiel terugkeren door op te geven Hallo-profiel en de bron-groep.</span><span class="sxs-lookup"><span data-stu-id="91a3c-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="91a3c-120">Het is mogelijk toohave meerdere CDN-met dezelfde naam, Hallo profielen zolang ze zich in verschillende resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="91a3c-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="91a3c-121">Hallo weglaten `ResourceGroupName` parameter retourneert alle profielen met een overeenkomende naam.</span><span class="sxs-lookup"><span data-stu-id="91a3c-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="91a3c-122">In de lijst bestaande CDN-eindpunten</span><span class="sxs-lookup"><span data-stu-id="91a3c-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="91a3c-123">`Get-AzureRmCdnEndpoint`een afzonderlijke eindpunt of alle Hallo eindpunten voor een profiel ophalen.</span><span class="sxs-lookup"><span data-stu-id="91a3c-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="91a3c-124">CDN-profielen en eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="91a3c-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="91a3c-125">`New-AzureRmCdnProfile`en `New-AzureRmCdnEndpoint` gebruikte toocreate CDN-profielen en eindpunten zijn.</span><span class="sxs-lookup"><span data-stu-id="91a3c-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="91a3c-126">Beschikbaarheid van de endpoint-naam controleren</span><span class="sxs-lookup"><span data-stu-id="91a3c-126">Checking endpoint name availability</span></span>
<span data-ttu-id="91a3c-127">`Get-AzureRmCdnEndpointNameAvailability`retourneert een object waarmee wordt aangegeven of de naam van een eindpunt beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="91a3c-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="91a3c-128">Een aangepast domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="91a3c-128">Adding a custom domain</span></span>
<span data-ttu-id="91a3c-129">`New-AzureRmCdnCustomDomain`Hiermee voegt u een aangepast domein naam tooan bestaande eindpunt toe.</span><span class="sxs-lookup"><span data-stu-id="91a3c-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91a3c-130">U moet instellen Hallo CNAME met uw DNS-provider zoals beschreven in [hoe toomap aangepaste domeinen tooContent Delivery Network (CDN) eindpunt](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="91a3c-131">U kunt testen Hallo toewijzing voordat het wijzigen van uw eindpunt met `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="91a3c-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="91a3c-132">Een eindpunt wijzigen</span><span class="sxs-lookup"><span data-stu-id="91a3c-132">Modifying an endpoint</span></span>
<span data-ttu-id="91a3c-133">`Set-AzureRmCdnEndpoint`Hiermee wijzigt u een bestaand eindpunt.</span><span class="sxs-lookup"><span data-stu-id="91a3c-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="91a3c-134">Opschonen van/Pre-loading CDN activa</span><span class="sxs-lookup"><span data-stu-id="91a3c-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="91a3c-135">`Unpublish-AzureRmCdnEndpointContent`schoont in de cache opgeslagen activa, terwijl `Publish-AzureRmCdnEndpointContent` vooraf geladen activa op ondersteunde eindpunten.</span><span class="sxs-lookup"><span data-stu-id="91a3c-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="91a3c-136">Starten/stoppen CDN-eindpunten</span><span class="sxs-lookup"><span data-stu-id="91a3c-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="91a3c-137">`Start-AzureRmCdnEndpoint`en `Stop-AzureRmCdnEndpoint` kunnen worden gebruikt toostart en afzonderlijke eindpunten of groepen van eindpunten stoppen.</span><span class="sxs-lookup"><span data-stu-id="91a3c-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="91a3c-138">CDN-resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="91a3c-138">Deleting CDN resources</span></span>
<span data-ttu-id="91a3c-139">`Remove-AzureRmCdnProfile`en `Remove-AzureRmCdnEndpoint` kan worden gebruikt tooremove profielen en -eindpunten.</span><span class="sxs-lookup"><span data-stu-id="91a3c-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="91a3c-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91a3c-140">Next Steps</span></span>
<span data-ttu-id="91a3c-141">Meer informatie over hoe Azure CDN tooautomate met [.NET](cdn-app-dev-net.md) of [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="91a3c-142">Zie toolearn over de functies in CDN [overzicht van CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91a3c-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

