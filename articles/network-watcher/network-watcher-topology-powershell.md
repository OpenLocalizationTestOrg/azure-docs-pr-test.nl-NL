---
title: aaaView Azure-netwerk-Watcher-topologie - PowerShell | Microsoft Docs
description: In dit artikel wordt beschreven hoe toouse PowerShell tooquery topologie van uw netwerk.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>Netwerk-Watcher-topologie met PowerShell weergeven

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

Hallo-topologie-functie van netwerk-Watcher biedt een visuele representatie van Hallo netwerkbronnen in een abonnement. In de portal Hallo is deze visualisatie opgenomen tooyou automatisch. Hallo gegevens achter Hallo Topologieweergave in de portal Hallo kan worden opgehaald via PowerShell.
Hierdoor kunt u meer mogelijkheden zoals Hallo gegevens kunnen worden gebruikt door andere hulpprogramma's voor toobuild uit Hallo visualisatie Hallo topologische informatie.

Hallo-koppeling is gemodelleerd onder twee-relaties.

- **Containment** -voorbeeld: VNet bevat een Subnet bevat een NIC
- **Gekoppeld** -voorbeeld: NIC is gekoppeld aan een virtuele machine

Hallo bevat volgende lijst eigenschappen die worden geretourneerd bij het opvragen van Hallo topologie REST-API.

* **naam** - hello naam van het Hallo-resource
* **id** -uri van de resource Hallo Hallo.
* **locatie** -Hallo locatie waar Hallo resource is opgeslagen.
* **koppelingen** -een lijst met koppelingen toohello verwijst naar object.
    * **naam** -naam Hallo Hallo waarnaar wordt verwezen resource.
    * **resourceId** -Hallo resourceId Hallo-uri van Hallo resource waarnaar wordt verwezen in Hallo-koppeling is.
    * **associationType** -Hallo relatie tussen Hallo onderliggend object en de bovenliggende Hallo wordt verwezen naar deze waarde. Geldige waarden zijn **bevat** of **gekoppelde**.

## <a name="before-you-begin"></a>Voordat u begint

In dit scenario gebruikt u Hallo `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve Hallo topologische informatie. Er is ook een artikel over het te[ophalen netwerktopologie met REST-API](network-watcher-topology-rest.md).

Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.

## <a name="scenario"></a>Scenario

Hallo scenario beschreven in dit artikel wordt antwoord van de Hallo-topologie voor een opgegeven resourcegroep opgehaald.

## <a name="retrieve-network-watcher"></a>Ophalen van netwerk-Watcher

de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar. Hallo `$networkWatcher` variabele is doorgegeven toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>Topologie ophalen

Hallo `Get-AzureRmNetworkWatcherTopology` cmdlet haalt Hallo-topologie voor een opgegeven resourcegroep.

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>Resultaten

Hallo resultaten hebben een eigenschap name 'Resources', waarin Hallo json antwoordtekst voor Hallo `Get-AzureRmNetworkWatcherTopology` cmdlet.  Hallo-antwoord bevat Hallo bronnen Hallo Netwerkbeveiligingsgroep en de bijbehorende koppelingen (dat wil zeggen, bevat, gekoppelde).

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


