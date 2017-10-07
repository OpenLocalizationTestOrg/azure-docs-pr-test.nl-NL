---
title: aaaGet de slag met Azure DNS met behulp van PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate een DNS-zone en een record in Azure DNS. Dit is een stapsgewijze handleiding toocreate en beheren van uw eerste DNS-zone en vastleggen met behulp van PowerShell.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>Aan de slag met Azure DNS met behulp van PowerShell

> [!div class="op_single_selector"]
> * [Azure Portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Dit artikel begeleidt u bij Hallo stappen toocreate, uw eerste DNS-zone en een record met behulp van Azure PowerShell. U kunt ook u deze stappen uitvoert met behulp van hello Azure-portal of Hallo platformoverschrijdende Azure CLI.

Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein. toostart die als host fungeert voor uw domein in Azure DNS, moet u een DNS-zone toocreate voor die domeinnaam. Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone. Ten slotte toopublish uw DNS-zone-toohello Internet, moet u tooconfigure Hallo-naamservers voor Hallo-domein. Deze stappen worden hieronder allemaal beschreven.

Deze instructies wordt ervan uitgegaan dat u al hebt geïnstalleerd en tooAzure PowerShell aangemeld. Zie voor informatie over [hoe toomanage DNS zones met behulp van PowerShell](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Voordat u Hallo DNS-zone maakt, wordt een resourcegroep toocontain Hallo DNS-Zone gemaakt. Hallo hieronder vindt u Hallo-opdracht.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>Een DNS-zone maken

Een DNS-zone wordt gemaakt met behulp van Hallo `New-AzureRmDnsZone` cmdlet. Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*. Hallo voorbeeld toocreate een DNS-zone, vervangen door Hallo waarden voor uw eigen gebruik.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>Een DNS-record maken

U recordsets maakt met behulp van Hallo `New-AzureRmDnsRecordSet` cmdlet. Hallo volgende voorbeeld wordt een record met Hallo relatieve naam 'www' in de DNS-Zone 'contoso.com' in de resourcegroep 'MyResourceGroup' Hallo. Hallo volledig gekwalificeerde naam van de recordset Hallo is 'www.contoso.com'. Hallo-recordtype is "A", met IP-adres '1.2.3.4' en Hallo TTL 3600 seconden is.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Voor andere recordtypen voor recordsets met meer dan een record en bestaande records toomodify, Zie [beheren DNS-records en recordsets met Azure PowerShell](dns-operations-recordsets.md). 


## <a name="view-records"></a>Records weergeven

toolist hello DNS-records in de zone gebruiken:

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Naamservers bijwerken

Wanneer u zich ervan overtuigd dat uw DNS-zone en records hebben is ingesteld, moet u tooconfigure uw domeinnaam toouse hello Azure DNS-naamservers. Hierdoor kunnen andere gebruikers op Hallo Internet toofind de DNS-records.

Hallo-naamservers voor uw zone worden gegeven voor Hallo `Get-AzureRmDnsZone` cmdlet:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Deze naamservers moeten worden geconfigureerd met Hallo domeinnaamregistrar (waarbij u hebt aangeschaft Hallo-domeinnaam). Uw registrar bieden Hallo optie tooset up Hallo naamservers voor Hallo-domein. Zie voor meer informatie [delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Alle resources verwijderen

toodelete alle resources die worden gemaakt in dit artikel nemen Hallo stap:

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

Zie toolearn meer informatie over Azure DNS [Azure DNS-overzicht](dns-overview.md).

Zie toolearn meer informatie over het beheren van DNS-zones in Azure DNS [beheren DNS-zones in Azure DNS met behulp van PowerShell](dns-operations-dnszones.md).

Zie toolearn meer informatie over het beheren van DNS-records in Azure DNS [beheren DNS-records en -recordsets stelt u in Azure DNS met behulp van PowerShell](dns-operations-recordsets.md).

