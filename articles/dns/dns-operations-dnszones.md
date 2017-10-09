---
title: aaaManage DNS-zones in Azure DNS - PowerShell | Microsoft Docs
description: U kunt DNS-zones met Azure Powershell beheren. Dit artikel wordt beschreven hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a>Hoe toomanage DNS-Zones met behulp van PowerShell

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Dit artikel laat zien hoe toomanage uw DNS-zones met behulp van Azure PowerShell. U kunt ook de DNS-zones met behulp van de platformoverschrijdende Hallo beheren [Azure CLI](dns-operations-dnszones-cli.md) of hello Azure-portal.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Een DNS-zone maken

Een DNS-zone wordt gemaakt met behulp van Hallo `New-AzureRmDnsZone` cmdlet.

Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Hallo volgende voorbeeld laat zien hoe toocreate een DNS-zone met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Ophalen van een DNS-zone

een DNS-zone tooretrieve gebruiken Hallo `Get-AzureRmDnsZone` cmdlet. Deze bewerking retourneert een DNS-zone-object bijbehorende tooan bestaande zone in Azure DNS. Hallo object bevat gegevens over Hallo zone (zoals Hallo aantal recordsets), maar bevat geen Hallo-recordsets zelf (Zie `Get-AzureRmDnsRecordSet`).

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a>Lijst met DNS-zones

Door de zonenaam Hallo van weg te laten `Get-AzureRmDnsZone`, kunt u alle zones in een resourcegroep opsommen. Deze bewerking retourneert een matrix van objecten van de zone.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Door zowel zonenaam Hallo Hallo Resourcegroepnaam van weg te laten `Get-AzureRmDnsZone`, kunt u alle zones in hello Azure-abonnement opsommen.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Bijwerken van een DNS-zone

DNS-zoneresource kan worden gemaakt met behulp van tooa wijzigingen `Set-AzureRmDnsZone`. Deze cmdlet werkt niet Hallo DNS-recordsets binnen de zone Hallo bij (Zie [hoe tooManage DNS-records](dns-operations-recordsets.md)). Het is alleen tooupdate eigenschappen van Hallo zoneresource zelf gebruikt. Hallo beschrijfbare zone-eigenschappen zijn momenteel beperkt toohello [Azure Resource Manager '-tags' voor Hallo zoneresource](dns-zones-records.md#tags).

Gebruik een van de volgende twee manieren tooupdate Hallo een DNS-zone:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Hallo-zone met Hallo zone en de bron-groep opgeven

Deze aanpak vervangen Hallo bestaande zone codes door Hallo waarden die zijn opgegeven.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Hallo-zone met behulp van een object $zone opgeven

Deze aanpak Hallo bestaande zone object opgehaald, Hallo labels wijzigt en vervolgens Hallo wijzigingen worden doorgevoerd. Op deze manier kunnen u bestaande labels behouden.

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

Wanneer u `Set-AzureRmDnsZone` met een object $zone [Etag controleert](dns-zones-records.md#etags) worden gebruikt tooensure gelijktijdige wijzigingen worden niet overschreven. U kunt optioneel Hallo `-Overwrite` overschakelen toosuppress deze controles.

## <a name="delete-a-dns-zone"></a>Een DNS-Zone verwijderen

DNS-zones worden verwijderd met de Hallo `Remove-AzureRmDnsZone` cmdlet.

> [!NOTE]
> Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in Hallo zone. Deze bewerking kan niet ongedaan worden gemaakt. Als Hallo DNS-zone gebruikt wordt, mislukt services met behulp van de zone Hallo wanneer Hallo zone wordt verwijderd.
>
>tooprotect tegen het onbedoeld zone verwijderen, Zie [hoe tooprotect DNS-zones en registreert](dns-protect-zones-recordsets.md).


Gebruik een van de volgende twee manieren toodelete Hallo een DNS-zone:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Geef Hallo-zone met behulp van de zonenaam Hallo en de naam van resourcegroep

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Hallo-zone met behulp van een object $zone opgeven

U kunt opgeven dat Hallo zone toobe verwijderd met een `$zone` object dat wordt geretourneerd door `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

Hallo zone object kan ook worden doorgesluisd in plaats van dat wordt doorgegeven als parameter:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Net als bij `Set-AzureRmDnsZone`, geven Hallo zone met behulp van een `$zone` object kunt Etag controleert tooensure gelijktijdige wijzigingen worden niet verwijderd. Gebruik Hallo `-Overwrite` overschakelen toosuppress deze controles.

## <a name="confirmation-prompts"></a>Bevestiging vragen

Hallo `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, en `Remove-AzureRmDnsZone` cmdlets alle bevestiging vragen ondersteunen.

Beide `New-AzureRmDnsZone` en `Set-AzureRmDnsZone` vragen om bevestiging als hello `$ConfirmPreference` PowerShell voorkeursvariabele een waarde heeft van `Medium` of lager. Vanwege het potentieel grote invloed van de toohello van het verwijderen van een DNS-zone hello `Remove-AzureRmDnsZone` cmdlet vraagt om bevestiging als hello `$ConfirmPreference` PowerShell variabele heeft de waarde van een andere waarde dan `None`.

Sinds de standaardwaarde Hallo voor `$ConfirmPreference` is `High`, alleen `Remove-AzureRmDnsZone` vraagt om bevestiging standaard.

U kunt de huidige Hallo overschrijven `$ConfirmPreference` instelling met de Hallo `-Confirm` parameter. Als u opgeeft `-Confirm` of `-Confirm:$True` , Hallo cmdlet vraagt u om bevestiging voordat deze wordt uitgevoerd. Als u opgeeft `-Confirm:$False` , Hallo cmdlet wordt u niet gevraagd om bevestiging.

Voor meer informatie over `-Confirm` en `$ConfirmPreference`, Zie [over Voorkeursvariabelen](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[beheren recordsets en records](dns-operations-recordsets.md) in uw DNS-zone.
<br>
Meer informatie over hoe te[delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).
<br>
Bekijk Hallo [Azure DNS PowerShell-naslagdocumentatie](/powershell/module/azurerm.dns).

