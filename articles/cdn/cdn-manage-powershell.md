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
# <a name="manage-azure-cdn-with-powershell"></a>Azure CDN met PowerShell beheren
PowerShell is een van de meest flexibele methoden toomanage Hallo uw Azure CDN-profielen en -eindpunten.  U kunt PowerShell kunt gebruiken, interactief of door het schrijven van scripts tooautomate beheertaken.  Deze zelfstudie ziet u diverse van Hallo meest algemene taken u kunt uitvoeren met PowerShell toomanage uw Azure CDN-profielen en -eindpunten.

## <a name="prerequisites"></a>Vereisten
toouse PowerShell toomanage uw Azure CDN-profielen en eindpunten, moet u hello Azure PowerShell-module geïnstalleerd hebben.  toolearn hoe tooinstall Azure PowerShell en verbinding maken met behulp van Hallo tooAzure `Login-AzureRmAccount` cmdlet, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

> [!IMPORTANT]
> U moet zich aanmelden met `Login-AzureRmAccount` voordat u Azure PowerShell-cmdlets kunt uitvoeren.
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a>Aanbieding hello Azure CDN-cmdlets
U kunt alle hello Azure CDN-cmdlets met Hallo lijst `Get-Command` cmdlet.

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

## <a name="getting-help"></a>Help opvragen
U kunt hulp krijgen met een van deze cmdlets met Hallo `Get-Help` cmdlet.  `Get-Help`biedt informatie over het gebruik en de syntaxis en eventueel ziet u voorbeelden.

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

## <a name="listing-existing-azure-cdn-profiles"></a>In de lijst bestaande Azure CDN-profielen
Hallo `Get-AzureRmCdnProfile` cmdlet zonder parameters haalt alle uw bestaande CDN-profielen.

```powershell
Get-AzureRmCdnProfile
```

Deze uitvoer kan doorgesluisd toocmdlets voor opsomming zijn.

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

U kunt ook één profiel terugkeren door op te geven Hallo-profiel en de bron-groep.

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> Het is mogelijk toohave meerdere CDN-met dezelfde naam, Hallo profielen zolang ze zich in verschillende resourcegroepen.  Hallo weglaten `ResourceGroupName` parameter retourneert alle profielen met een overeenkomende naam.
> 
> 

## <a name="listing-existing-cdn-endpoints"></a>In de lijst bestaande CDN-eindpunten
`Get-AzureRmCdnEndpoint`een afzonderlijke eindpunt of alle Hallo eindpunten voor een profiel ophalen.  

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

## <a name="creating-cdn-profiles-and-endpoints"></a>CDN-profielen en eindpunten maken
`New-AzureRmCdnProfile`en `New-AzureRmCdnEndpoint` gebruikte toocreate CDN-profielen en eindpunten zijn.

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a>Beschikbaarheid van de endpoint-naam controleren
`Get-AzureRmCdnEndpointNameAvailability`retourneert een object waarmee wordt aangegeven of de naam van een eindpunt beschikbaar is.

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a>Een aangepast domein toevoegen
`New-AzureRmCdnCustomDomain`Hiermee voegt u een aangepast domein naam tooan bestaande eindpunt toe.

> [!IMPORTANT]
> U moet instellen Hallo CNAME met uw DNS-provider zoals beschreven in [hoe toomap aangepaste domeinen tooContent Delivery Network (CDN) eindpunt](cdn-map-content-to-custom-domain.md).  U kunt testen Hallo toewijzing voordat het wijzigen van uw eindpunt met `Test-AzureRmCdnCustomDomain`.
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

## <a name="modifying-an-endpoint"></a>Een eindpunt wijzigen
`Set-AzureRmCdnEndpoint`Hiermee wijzigt u een bestaand eindpunt.

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a>Opschonen van/Pre-loading CDN activa
`Unpublish-AzureRmCdnEndpointContent`schoont in de cache opgeslagen activa, terwijl `Publish-AzureRmCdnEndpointContent` vooraf geladen activa op ondersteunde eindpunten.

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a>Starten/stoppen CDN-eindpunten
`Start-AzureRmCdnEndpoint`en `Stop-AzureRmCdnEndpoint` kunnen worden gebruikt toostart en afzonderlijke eindpunten of groepen van eindpunten stoppen.

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a>CDN-resources verwijderen
`Remove-AzureRmCdnProfile`en `Remove-AzureRmCdnEndpoint` kan worden gebruikt tooremove profielen en -eindpunten.

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe Azure CDN tooautomate met [.NET](cdn-app-dev-net.md) of [Node.js](cdn-app-dev-node.md).

Zie toolearn over de functies in CDN [overzicht van CDN](cdn-overview.md).

