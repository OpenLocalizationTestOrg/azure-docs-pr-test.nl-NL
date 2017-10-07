---
title: aaaManage DNS-zones in Azure DNS - Azure CLI 1.0 | Microsoft Docs
description: U kunt DNS-zones met behulp van Azure CLI 1.0 beheren. Dit artikel laat zien hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a>Hoe toomanage DNS-Zones in Azure DNS met behulp van Azure CLI 1.0 Hallo

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Deze handleiding wordt getoond hoe toomanage uw DNS-zones met behulp van Hallo platformoverschrijdende Azure CLI 1.0, die beschikbaar is voor Windows, Mac en Linux. U kunt ook beheren met behulp van DNS-zones [Azure PowerShell](dns-operations-dnszones.md) of hello Azure-portal.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel.

## <a name="introduction"></a>Inleiding

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a>Help opvragen

Alle betreffende tooAzure DNS CLI 1.0-opdrachten starten met `azure network dns`. Help beschikbaar is voor elke opdracht met Hallo `--help` optie (korte versie `-h`).  Bijvoorbeeld:

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a>Een DNS-zone maken

Een DNS-zone wordt gemaakt met Hallo `azure network dns zone create` opdracht. Zie `azure network dns zone create -h` voor help.

Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*:

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate een DNS-zone met labels

Hallo volgende voorbeeld laat zien hoe toocreate een DNS-zone met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*, met behulp van Hallo `--tags` parameter (korte versie `-t`):

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a>Ophalen van een DNS-zone

gebruik van een DNS-zone tooretrieve `azure network dns zone show`. Zie `azure network dns zone show -h` voor help.

Hallo volgende voorbeeld retourneert Hallo DNS-zone *contoso.com* en de bijbehorende gegevens van de resourcegroep *MyResourceGroup*. 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

Hallo volgende voorbeeld is Hallo antwoord.

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

Houd er rekening mee dat DNS-records worden niet geretourneerd door `azure network dns zone show`. gebruik van DNS-records van toolist `azure network dns record-set list`.


## <a name="list-dns-zones"></a>Lijst met DNS-zones

tooenumerate DNS-zones, gebruik `azure network dns zone list`. Zie `azure network dns zone list -h` voor help.

Het opgeven van het Hallo-resourcegroep bevat alleen deze zones in de resourcegroep Hallo:

```azurecli
azure network dns zone list MyResourceGroup
```

Hallo resourcegroep als weggelaten een lijst met alle zones in abonnement Hallo:

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a>Bijwerken van een DNS-zone

Wijzigingen tooa DNS-zoneresource kan worden gemaakt met behulp van `azure network dns zone set`. Zie `azure network dns zone set -h` voor help.

Met deze opdracht wordt niet Hallo DNS-recordsets binnen de zone Hallo bijgewerkt (Zie [hoe tooManage DNS-records](dns-operations-recordsets-cli-nodejs.md)). Alleen gebruikte tooupdate eigenschappen van Hallo zoneresource zelf is. Deze eigenschappen zijn momenteel beperkt toohello [Azure Resource Manager 'labels'](dns-zones-records.md#tags) voor Hallo zoneresource.

Hallo volgende voorbeeld ziet u hoe tooupdate Hallo codes op een DNS-zone. Hallo bestaande labels worden vervangen door Hallo waarde die is opgegeven.

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a>Een DNS-Zone verwijderen

DNS-zones worden verwijderd met een `azure network dns zone delete`. Zie `azure network dns zone delete -h` voor help.

> [!NOTE]
> Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in Hallo zone. Deze bewerking kan niet ongedaan worden gemaakt. Als Hallo DNS-zone gebruikt wordt, mislukt services met behulp van de zone Hallo wanneer Hallo zone wordt verwijderd.
>
>tooprotect tegen het onbedoeld zone verwijderen, Zie [hoe tooprotect DNS-zones en registreert](dns-protect-zones-recordsets.md).

Met deze opdracht vraagt om bevestiging. Hallo optionele `--quiet` gaan (korte versie `-q`) deze prompt onderdrukt.

Hallo volgende voorbeeld laat zien hoe toodelete zone Hallo *contoso.com* uit resourcegroep *MyResourceGroup*.

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[beheren recordsets en records](dns-getstarted-create-recordset-cli-nodejs.md) in uw DNS-zone.

Meer informatie over hoe te[delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).

