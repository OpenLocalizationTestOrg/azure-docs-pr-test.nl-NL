---
title: aaaGet de slag met Azure DNS met Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe toocreate een DNS-zone en een record in Azure DNS. Dit is een stapsgewijze handleiding toocreate en beheren van uw eerste DNS-zone en een record met behulp van hello Azure CLI 1.0.
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a>Aan de slag met Azure DNS met behulp van Azure-CLI 1.0

> [!div class="op_single_selector"]
> * [Azure Portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Dit artikel begeleidt u bij Hallo stappen toocreate uw eerste DNS-zone en platformoverschrijdende Azure CLI 1.0 met behulp van record Hallo die beschikbaar is voor Windows, Mac en Linux. U kunt deze stappen met hello Azure-portal of Azure PowerShell ook uitvoeren.

Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein. toostart die als host fungeert voor uw domein in Azure DNS, moet u een DNS-zone toocreate voor die domeinnaam. Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone. Ten slotte toopublish uw DNS-zone-toohello Internet, moet u tooconfigure Hallo-naamservers voor Hallo-domein. Deze stappen worden hieronder allemaal beschreven.

Deze instructies wordt ervan uitgegaan dat u al hebt geïnstalleerd en aangemeld tooAzure CLI 1.0. Zie voor informatie over [hoe toomanage DNS zones met behulp van Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Voordat u Hallo DNS-zone maakt, wordt een resourcegroep toocontain Hallo DNS-Zone gemaakt. Hallo hieronder vindt u Hallo-opdracht.

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a>Een DNS-zone maken

Een DNS-zone wordt gemaakt met Hallo `azure network dns zone create` opdracht. help voor deze opdracht toosee plaatst `azure network dns zone create -h`.

Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*. Hallo voorbeeld toocreate een DNS-zone, vervangen door Hallo waarden voor uw eigen gebruik.

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a>Een DNS-record maken

toocreate een DNS-record gebruiken Hallo `azure network dns record-set add-record` opdracht. Zie `azure network dns record-set add-record -h` voor help.

Hallo volgende voorbeeld wordt een record met Hallo relatieve naam 'www' in de DNS-Zone 'contoso.com' in de resourcegroep 'MyResourceGroup' Hallo. Hallo volledig gekwalificeerde naam van de recordset Hallo is 'www.contoso.com'. Hallo-recordtype is "A", met IP-adres '1.2.3.4' en een standaard-TTL van 3600 seconden (1 uur) wordt gebruikt.

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

Voor andere recordtypen voor recordsets met meer dan één record, voor alternatieve TTL waarden en toomodify bestaande records, Zie [beheren DNS-records en recordsets met behulp van Azure CLI 1.0 Hallo](dns-operations-recordsets-cli-nodejs.md).


## <a name="view-records"></a>Records weergeven

toolist hello DNS-records in de zone gebruiken:

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a>Naamservers bijwerken

Wanneer u zich ervan overtuigd dat uw DNS-zone en records hebben is ingesteld, moet u tooconfigure uw domeinnaam toouse hello Azure DNS-naamservers. Hierdoor kunnen andere gebruikers op Hallo Internet toofind de DNS-records.

Hallo-naamservers voor uw zone worden gegeven voor Hallo `azure network dns zone show` opdracht:

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

Deze naamservers moeten worden geconfigureerd met Hallo domeinnaamregistrar (waarbij u hebt aangeschaft Hallo-domeinnaam). Uw registrar bieden Hallo optie tooset up Hallo naamservers voor Hallo-domein. Zie voor meer informatie [delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Alle resources verwijderen
 
toodelete alle resources die worden gemaakt in dit artikel nemen Hallo stap:

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

Zie toolearn meer informatie over Azure DNS [Azure DNS-overzicht](dns-overview.md).

Zie toolearn meer informatie over het beheren van DNS-zones in Azure DNS [beheren DNS-zones in Azure DNS met Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).

Zie toolearn meer informatie over het beheren van DNS-records in Azure DNS [beheren DNS-records en -recordsets stelt u in Azure DNS met Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).

