---
title: aaaManage DNS-zones in Azure DNS - Azure CLI 2.0 | Microsoft Docs
description: U kunt DNS-zones met Azure CLI 2.0 beheren. Dit artikel laat zien hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Hoe toomanage DNS-Zones in Azure DNS met behulp van Azure CLI 2.0 Hallo

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)


Deze handleiding wordt getoond hoe toomanage uw DNS-zones met behulp van Hallo platformoverschrijdende CLI van Azure, die beschikbaar is voor Windows, Mac en Linux. U kunt ook beheren met behulp van DNS-zones [Azure PowerShell](dns-operations-dnszones.md) of hello Azure-portal.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel.

## <a name="introduction"></a>Inleiding

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Azure CLI 2.0 instellen voor Azure DNS

### <a name="before-you-begin"></a>Voordat u begint

Controleer of u Hallo volgende items voordat u begint met de configuratie.

* Een Azure-abonnement. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).

* Installeer de nieuwste versie Hallo van hello Azure CLI 2.0, die beschikbaar zijn voor Windows, Linux of MAC. Meer informatie vindt u op [installeren hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Meld u aan tooyour Azure-account

Open een consolevenster en doorloop de verificatie met uw referenties. Zie het logboek voor meer informatie in tooAzure van hello Azure CLI

```
az login
```

### <a name="select-hello-subscription"></a>Hallo-abonnement selecteren

Controleer de abonnementen Hallo voor Hallo-account.

```
az account list
```

Kies welke van uw Azure-abonnementen toouse.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Echter, omdat alle DNS-resources globaal en niet regionaal zijn, heeft Hallo keuze van de locatie voor resourcegroep geen invloed op Azure DNS.

U kunt deze stap overslaan als u een bestaande resourcegroep gebruikt.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Help opvragen

Alle betreffende tooAzure DNS CLI 2.0-opdrachten starten met `az network dns`. Help beschikbaar is voor elke opdracht met Hallo `--help` optie (korte versie `-h`).  Bijvoorbeeld:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Een DNS-zone maken

Een DNS-zone wordt gemaakt met Hallo `az network dns zone create` opdracht. Zie `az network dns zone create -h` voor help.

Hallo volgende voorbeeld maakt u een DNS-zone aangeroepen *contoso.com* in de resourcegroep Hallo aangeroepen *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate een DNS-zone met labels

Hallo volgende voorbeeld laat zien hoe toocreate een DNS-zone met twee [Azure Resource Manager-tags](dns-zones-records.md#tags), *project = demo* en *env = test*, met behulp van Hallo `--tags` parameter (korte versie `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Ophalen van een DNS-zone

gebruik van een DNS-zone tooretrieve `az network dns zone show`. Zie `az network dns zone show --help` voor help.

Hallo volgende voorbeeld retourneert Hallo DNS-zone *contoso.com* en de bijbehorende gegevens van de resourcegroep *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Hallo volgende voorbeeld is Hallo antwoord.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Houd er rekening mee dat DNS-records worden niet geretourneerd door `az network dns zone show`. gebruik van DNS-records van toolist `az network dns record-set list`.


## <a name="list-dns-zones"></a>Lijst met DNS-zones

tooenumerate DNS-zones, gebruik `az network dns zone list`. Zie `az network dns zone list --help` voor help.

Het opgeven van het Hallo-resourcegroep bevat alleen deze zones in de resourcegroep Hallo:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Hallo resourcegroep als weggelaten een lijst met alle zones in abonnement Hallo:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Bijwerken van een DNS-zone

Wijzigingen tooa DNS-zoneresource kan worden gemaakt met behulp van `az network dns zone update`. Zie `az network dns zone update --help` voor help.

Met deze opdracht wordt niet Hallo DNS-recordsets binnen de zone Hallo bijgewerkt (Zie [hoe tooManage DNS-records](dns-operations-recordsets-cli.md)). Alleen gebruikte tooupdate eigenschappen van Hallo zoneresource zelf is. Deze eigenschappen zijn momenteel beperkt toohello [Azure Resource Manager 'labels'](dns-zones-records.md#tags) voor Hallo zoneresource.

Hallo volgende voorbeeld ziet u hoe tooupdate Hallo codes op een DNS-zone. Hallo bestaande labels worden vervangen door Hallo waarde die is opgegeven.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Een DNS-zone verwijderen

DNS-zones worden verwijderd met een `az network dns zone delete`. Zie `az network dns zone delete --help` voor help.

> [!NOTE]
> Een DNS-zone verwijderen, verwijdert tevens alle DNS-records in Hallo zone. Deze bewerking kan niet ongedaan worden gemaakt. Als Hallo DNS-zone gebruikt wordt, mislukt services met behulp van de zone Hallo wanneer Hallo zone wordt verwijderd.
>
>tooprotect tegen het onbedoeld zone verwijderen, Zie [hoe tooprotect DNS-zones en registreert](dns-protect-zones-recordsets.md).

Met deze opdracht vraagt om bevestiging. Hallo optionele `--yes` schakeloptie deze vraag wordt geblokkeerd.

Hallo volgende voorbeeld laat zien hoe toodelete zone Hallo *contoso.com* uit resourcegroep *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[beheren recordsets en records](dns-getstarted-create-recordset-cli.md) in uw DNS-zone.

Meer informatie over hoe te[delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).

