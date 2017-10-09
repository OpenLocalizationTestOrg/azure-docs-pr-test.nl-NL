---
title: aaaAzure Cosmos DB algemene distributie-zelfstudie voor tabel-API | Microsoft Docs
description: Meer informatie over hoe toosetup Azure Cosmos DB globale distributie op basis Hallo tabel-API.
services: cosmos-db
keywords: globale distributie, tabel
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>Hoe toosetup Azure Cosmos DB globale distributie op basis Hallo tabel-API

In dit artikel, laten we zien hoe toouse hello Azure portal toosetup Azure Cosmos DB globale distributie en vervolgens verbinding maken via Hallo tabel-API (preview).

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Globale distributie op basis van hello Azure-portal configureren
> * Configureren van de algemene distributie op basis van Hallo [tabel-API](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Verbinding maken met tooa voorkeursregio met Hallo tabel-API

In de volgorde tootake profiteren van [globale distributie](distribute-data-globally.md), clienttoepassingen Hallo besteld voorkeur lijst met regio's toobe gebruikte tooperform document bewerkingen kunnen opgeven. Dit kan worden gedaan door de instelling Hallo `TablePreferredLocations` configuratiewaarde in Hallo app-configuratie voor Hallo preview Azure-opslag-SDK. Op basis van hello Azure DB die Cosmos-accountconfiguratie, huidige regionale beschikbaarheid en Hallo voorkeur lijst die is opgegeven, Hallo meeste optimale eindpunt wordt gekozen door hello Azure-opslag-SDK tooperform schrijven en lees-en schrijfopdrachten.

Hallo `TablePreferredLocations` moet een door komma's gescheiden lijst met aanbevolen (multihoming) locaties bevatten voor leesbewerkingen. Elk clientexemplaar kunt u een subset van deze gebieden in volgorde van voorkeur Hallo voor lage latentie leesbewerkingen opgeven. Hallo-regio's moeten de namen van hun [weergavenamen](https://msdn.microsoft.com/library/azure/gg441293.aspx), bijvoorbeeld `West US`.

Alle leest de eerste beschikbare regio toohello verzonden in Hallo `TablePreferredLocations` lijst. Als Hallo-aanvraag is mislukt, zal Hallo client mislukken omlaag Hallo lijst toohello volgende regio, enzovoort.

Hallo SDK proberen enkel tooread uit Hallo regio's die zijn opgegeven in `TablePreferredLocations`. Dus bijvoorbeeld als Hallo databaseaccount beschikbaar in drie gebieden is, maar het Hallo-client alleen twee van bevat Hallo niet schrijven regio's voor `TablePreferredLocations`, en vervolgens geen leesbewerkingen buiten Hallo schrijven regio, zelfs in geval van Hallo van failover kunnen worden geleverd.

Hallo SDK worden automatisch alle schrijfbewerkingen toohello huidige schrijven regio verzonden.

Als hello `TablePreferredLocations` eigenschap niet is ingesteld, worden alle aanvragen worden aangeboden via Hallo huidige schrijven regio.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

Dat is, die in deze zelfstudie is voltooid. U leert hoe toomanage consistentie van uw account globaal gerepliceerde Hallo door te lezen [consistentieniveaus in Azure Cosmos DB](consistency-levels.md). En Zie voor meer informatie over hoe globale databasereplicatie in Azure Cosmos DB werkt, [gegevens globaal met Azure Cosmos DB distribueren](distribute-data-globally.md).

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Globale distributie op basis van hello Azure-portal configureren
> * Globale distributie op basis van Hallo DocumentDB APIs configureren

U kunt nu doorgaan met de volgende zelfstudie toolearn toohello hoe toodevelop lokaal via Azure Cosmos DB lokale emulator Hallo.

> [!div class="nextstepaction"]
> [Lokaal ontwikkelen met Hallo emulator](local-emulator.md)
