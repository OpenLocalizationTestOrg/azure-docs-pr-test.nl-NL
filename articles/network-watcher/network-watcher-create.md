---
title: een exemplaar van Azure-netwerk-Watcher aaaCreate | Microsoft Docs
description: Deze pagina bevat Hallo stappen toocreate een exemplaar van netwerk-Watcher met Hallo-portal en Azure REST-API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Maak een instantie van de Azure-netwerk-Watcher

Netwerk-Watcher is een regionale service waarmee u toomonitor en onderzoeken van voorwaarden op een netwerk scenario niveau in, en naar Azure. Niveau bewaking scenario kunt u problemen toodiagnose op een niveau weergeven voor end tooend netwerk. Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure.

> [!NOTE]
> Zoals netwerk-Watcher momenteel alleen CLI 1.0 ondersteunt, Hallo instructies toocreate een nieuw netwerk-Watcher-exemplaar is beschikbaar voor CLI 1.0.

## <a name="create-a-network-watcher-in-hello-portal"></a>Maken van een netwerk-Watcher in Hallo-portal

Navigeer te**meer Services** > **Networking** > **netwerk-Watcher**. U kunt alle Hallo-abonnementen die u wilt dat tooenable netwerk-Watcher selecteren voor. Deze actie wordt een netwerk-Watcher in elke regio die beschikbaar is gemaakt.

![maken van een netwerk-watcher][1]

Wanneer u de netwerk-Watcher met Hallo Portal inschakelt, wordt Hallo-naam van exemplaar van de netwerk-Watcher hello automatisch ingesteld tooNetworkWatcher_region_name waarbij region_name overeenkomt met toohello Azure-regio waar Hallo-exemplaar is ingeschakeld.  Een netwerk-Watcher ingeschakeld in de regio West-Centraal VS wordt bijvoorbeeld de naam NetworkWatcher_westcentralus

Hallo netwerk-Watcher-exemplaar wordt daarnaast automatisch worden toegevoegd aan een resourcegroep NetworkWatcherRG aangeroepen.  Deze resourcegroep wordt gemaakt als deze niet al bestaat.

U kunt eventueel toocustomize Hallo-naam van een exemplaar van de netwerk-Watcher en Hallo resourcegroep wordt deze geplaatst in, kunt u Powershell, Hallo REST-API of ARMClient methoden die hieronder worden beschreven.  Bij elke optie worden de Hallo resourcegroep moet bestaan voordat u Hallo netwerk-Watcher erin plaatsen.  

## <a name="create-a-network-watcher-with-powershell"></a>Maken van een netwerk-Watcher met PowerShell

toocreate een exemplaar van netwerk-Watcher Hallo volgt uitgevoerd:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Maken van een netwerk-Watcher Hello REST-API

ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell. ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)

### <a name="log-in-with-armclient"></a>Meld u aan met ARMClient

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Hallo netwerk-watcher maken

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Volgende stappen

Nu dat u een exemplaar van netwerk-Watcher hebt, kunt u informatie over Hallo functies beschikbaar:

* [Topologie](network-watcher-topology-overview.md)
* [Pakketopname](network-watcher-packet-capture-overview.md)
* [IP-stroomverificatie](network-watcher-ip-flow-verify-overview.md)
* [Volgende hop](network-watcher-next-hop-overview.md)
* [Beveiligingsgroepweergave](network-watcher-security-group-view-overview.md)
* [NSG stroom logboekregistratie](network-watcher-nsg-flow-logging-overview.md)
* [Virtuele netwerkgateway probleemoplossing](network-watcher-troubleshoot-overview.md)

Zodra een netwerk-Watcher-exemplaar is gemaakt, pakket vastleggen kan worden geconfigureerd door de volgende Hallo-artikel: [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











