---
title: de volgende hop aaaFind met Azure-netwerk-Watcher volgende Hop - Azure CLI 2.0 | Microsoft Docs
description: In dit artikel wordt beschreven hoe u welke Hallo type voor het volgende hop is en het gebruik van IP-adres van volgende Hop met Azure CLI kunt vinden.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a>Ontdek welke Hallo volgend hoptype Hallo volgende Hop mogelijkheid gebruikt in Azure met Azure CLI 2.0 netwerk-Watcher

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST-API](network-watcher-check-next-hop-rest.md)

De volgende hop is een functie van netwerk-Watcher die de mogelijkheid Hallo biedt Hallo volgend hoptype en IP-adres op basis van een opgegeven virtuele machine ophalen. Deze functie is handig bij het bepalen of een virtuele machine uitgaand verkeer van een gateway, internet of virtuele netwerken tooget tooits bestemming passeert.

In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Voordat u begint

In dit scenario gebruikt u Azure CLI toofind Hallo volgend hoptype hello en IP-adres.

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher. Hallo scenario wordt ervan uitgegaan dat een resourcegroep met een geldige virtuele machine toobe gebruikt bestaat.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel maakt gebruik van volgende Hop, een functie van netwerk-Watcher waarmee wordt gezocht naar het volgende hoptype hello en IP-adres voor een resource. toolearn meer informatie over het volgende Hop, gaat u naar [volgende Hop overzicht](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Ophalen van de volgende Hop

tooget hello volgende hop noemen we Hallo `az network watcher show-next-hop` cmdlet. We geven Hallo cmdlet Hallo netwerk-Watcher-resourcegroep, Hallo NetworkWatcher virtuele machine Id, IP-bronadres en IP-doeladres. In dit voorbeeld is de IP-doeladres Hallo tooa VM in een ander virtueel netwerk. Er is een virtuele netwerkgateway tussen Hallo twee virtuele netwerken.

Als u dit nog niet hebt nog installeren en configureren van Hallo meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login). Voer vervolgens de volgende opdracht Hallo:

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
Als Hallo VM meerdere NIC's en doorsturen via IP is ingeschakeld op Hallo NIC's, klikt u vervolgens Hallo NIC-parameter (-ik nic-id) moet worden opgegeven. Anders is optioneel.

## <a name="review-results"></a>Resultaten bekijken

Als u klaar worden Hallo resultaten geleverd. Hallo volgende hop IP-adres wordt geretourneerd en Hallo type resource is.

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

Hallo bevat volgende lijst de momenteel beschikbare NextHopType waarden Hallo:

**Volgend Hoptype**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Geen

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooreview uw netwerk groep beveiligingsinstellingen programmatisch in via [NSG controleren met de netwerk-Watcher](network-watcher-nsg-auditing-powershell.md)
