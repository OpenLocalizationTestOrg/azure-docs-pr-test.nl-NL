---
title: aaaRegional-failover in Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe handmatige en automatische failover werkt met Azure Cosmos DB.
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>Automatische regionale failover voor bedrijfscontinuïteit in Azure Cosmos-DB
Azure Cosmos DB vereenvoudigt Hallo globale distributie van gegevens door het aanbieden van volledig worden beheerd, [meerdere landen/regio database accounts](distribute-data-globally.md) die wissen balans vinden tussen de consistentie, beschikbaarheid en prestaties, met bijbehorende bieden gegarandeerd. Cosmos DB accounts bieden hoge beschikbaarheid, één cijfer ms latenties, [goed gedefinieerde consistentieniveaus](consistency-levels.md), transparante regionale failover met multihoming API's, en Hallo mogelijkheid tooelastically scale doorvoer en opslag over Hallo wereld. 

Cosmos DB ondersteunt zowel expliciete en failovers aangestuurd beleid waarmee u toocontrol Hallo end-to-end-systeemgedrag in Hallo-gebeurtenis van fouten. In dit artikel kijken we:

* Hoe werken handmatige failover in Cosmos-database?
* Hoe automatische failovers werk in Cosmos-DB en wat er gebeurt wanneer een data center gaan omlaag?
* Hoe kunt u een handmatige failover in toepassingsarchitecturen?

U kunt ook meer informatie over regionale failovers in deze Azure vrijdag video met Scott Hanselman en Principal Engineering Manager Karthik Raman.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>Meerdere landen/regio-toepassingen configureren
Voordat we Duik in de failover-modi, die we kijken hoe kunt u een toepassing tootake voordeel van beschikbaarheid in meerdere regio's configureren en netwerkfouten in Hallo vlak van regionale failover.

* Implementeer eerst uw toepassing in meerdere regio 's
* tooensure lage latentie toegang vanaf elke regio uw toepassing wordt geïmplementeerd, configureert Hallo overeenkomt [lijst met aanbevolen regio's](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) voor elke regio via een Hallo SDK's ondersteunde.

Hallo volgende codefragment bevat hoe tooinitialize een toepassing met meerdere landen/regio. Hier hello Azure Cosmos DB account `contoso.documents.azure.com` is geconfigureerd met twee gebieden - VS-West en Noord-Europa. 

* Hallo-toepassing wordt geïmplementeerd in de regio VS-West hello (met behulp van Azure App Services bijvoorbeeld) 
* Met geconfigureerd `West US` leest als de eerste voorkeursregio Hallo voor lage latentie
* Met geconfigureerd `North Europe` als de tweede voorkeursregio hello (voor hoge beschikbaarheid tijdens regionale fouten)

In DocumentDB API hello ziet deze configuratie Hallo codefragment te volgen:

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

Hallo-toepassing wordt ook geïmplementeerd in Hallo Noord-Europa regio met Hallo volgorde van voorkeur gebieden omgekeerd. Dat wil zeggen, is de regio Noord-Europa Hallo eerst opgegeven voor leesbewerkingen lage latentie. Vervolgens is Hallo VS-West regio opgegeven als de tweede voorkeursregio Hallo voor hoge beschikbaarheid tijdens regionale fouten.

Hallo volgende Architectuurdiagram toont een implementatie voor meerdere landen/regio waar Cosmos DB en toepassing hello geconfigureerde toobe in vier Azure geografische regio's beschikbaar zijn.  

![Globaal gedistribueerde toepassingsimplementatie met Azure Cosmos-DB](./media/regional-failover/app-deployment.png)

Nu gaan we kijken hoe Hallo Cosmos DB service regionale fouten via automatische failovers verwerkt. 

## <a id="AutomaticFailovers"></a>Automatische Failovers
In zeldzame geval van een Azure regionale uitval of datacentrum Hallo Cosmos DB automatisch geactiveerd failovers van alle Cosmos-DB-accounts met een aanwezigheid in Hallo van invloed op een regio. 

**Wat gebeurt er als een lezen regio een storing heeft?**

Cosmos DB accounts met een regio lezen in een Hallo van invloed op een regio's worden automatisch losgekoppeld van hun regio schrijven en gemarkeerd offline. Hallo Cosmos DB SDK's implementeren een regionale discovery-protocol waarmee ze tooautomatically detecteren wanneer een regio beschikbaar is en omleiding aanroepen toohello volgende beschikbare regio in de lijst van de gewenste regio Hallo gelezen. Als geen van Hallo gebieden in Hallo regio beschikbaar is voorkeurslijst, terugvallen aanroepen automatisch toohello huidige schrijven regio. Er zijn geen wijzigingen vereist zijn in uw toepassing code toohandle regionale failovers. Tijdens dit proces gehele blijven consistentie wordt gegarandeerd toobe Cosmos DB gehonoreerd.

![Lees regio fouten in Azure Cosmos-DB](./media/regional-failover/read-region-failures.png)

Wanneer Hallo van invloed op een regio vanuit Hallo onderbreking herstelt, worden alle Hallo van invloed op een Cosmos-DB-accounts in Hallo regio automatisch hersteld door Hallo-service. Cosmos DB accounts waarop een lezen regio in Hallo van invloed op een regio wordt vervolgens automatisch synchroniseren met de huidige schrijven gebied en online inschakelen. Hallo Cosmos DB SDK's Hallo beschikbaarheid van nieuwe gebied Hallo detecteren en evalueren of Hallo regio als Hallo huidige lezen regio op basis van Hallo voorkeursregio lijst geconfigureerd door de toepassing hello moet worden geselecteerd. Opeenvolgende leesbewerkingen zijn omgeleide toohello herstelde regio zonder eventuele wijzigingen tooyour-toepassingscode.

**Wat gebeurt er als een regio schrijven een storing heeft?**

Als betrokken regio Hallo Hallo huidige schrijven gebied voor een opgegeven Cosmos-DB-account is, worden klikt u vervolgens Hallo regio automatisch gemarkeerd als offline. Een andere regio wordt vervolgens gepromoveerd Hallo schrijven regio elk betrokken Cosmos-DB-account. U kunt volledig Hallo regio selectie om uw accounts Cosmos DB via hello Azure-portal beheren of [programmatisch](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange). 

![Failover prioriteiten voor het Azure Cosmos-DB](./media/regional-failover/failover-priorities.png)

Tijdens automatische failovers Cosmos DB automatisch gekozen Hallo volgende schrijven gebied voor een opgegeven Cosmos-DB-account op basis van Hallo opgegeven volgorde van prioriteit. 

![Schrijffouten regio in Azure Cosmos-DB](./media/regional-failover/write-region-failures.png)

Wanneer Hallo van invloed op een regio vanuit Hallo onderbreking herstelt, worden alle Hallo van invloed op een Cosmos-DB-accounts in Hallo regio automatisch hersteld door Hallo-service. 

* Cosmos DB accounts op hun vorige schrijven regio in Hallo van invloed op een regio blijft in de offlinemodus met lezen beschikbaarheid zelfs na het herstel van Hallo regio Hallo. 
* U kunt een query deze regio toocompute er niet-gerepliceerde schrijfbewerkingen tijdens Hallo onderbreking door te vergelijken met het Hallo-gegevens die beschikbaar zijn in de huidige schrijven regio Hallo. Op basis van de behoeften van uw toepassing hello, kunt u samenvoegen en/of het conflict oplossen en schrijf Hallo uiteindelijke set wijzigingen back toohello huidige schrijven regio. 
* Nadat u samenvoegen wijzigingen hebt voltooid, kunt u Hallo van invloed op een regio terug online brengt door te verwijderen en readding Hallo regio tooyour Cosmos-DB-account. Wanneer Hallo regio weer is toegevoegd, kunt u deze weer als Hallo schrijven regio configureren voor het uitvoeren van een handmatige failover via hello Azure-portal of [programmatisch](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).

## <a id="ManualFailovers"></a>Handmatige failover

Bovendien schrijven tooautomatic failovers, huidige Hallo regio van een opgegeven Cosmos-DB-account kan handmatig dynamisch worden gewijzigd tooone van Hallo bestaande lezen regio's. Handmatige failover kan worden gestart via hello Azure-portal of [programmatisch](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate). 

Handmatige failover zorg **nul gegevensverlies** en **nul beschikbaarheid** verlies en probleemloos schrijven Overdrachtsstatus van oude Hallo schrijven regio toohello nieuwe voor Hallo Cosmos-DB-account opgegeven. Zoals in automatische failover automatisch Cosmos DB SDK Hallo schrijven ingangen regio wijzigingen tijdens handmatige failovers en zorgt ervoor dat oproepen automatisch omgeleid toohello nieuwe schrijven regio zijn. Er zijn geen wijzigingen code of configuratie vereist zijn in uw toepassing toomanage failovers. 

![Handmatige failover in Azure Cosmos-DB](./media/regional-failover/manual-failovers.png)

Enkele Hallo algemene scenario's waarbij handmatige failover kan nuttig zijn, zijn:

**Ga als volgt Hallo klok model**: als uw toepassingen voorspelbare verkeerspatronen op basis van tijd van de dag Hallo Hallo hebt, kunt u periodiek Hallo schrijven status toohello Actiefste geografische regio op basis van tijd van de dag Hallo wijzigen.

**Service-update**: de implementatie van bepaalde globaal gedistribueerde toepassing dient u mogelijk het omleiden van verkeer toodifferent regio via het traffic manager tijdens de geplande service-update. Nu de implementatie van deze toepassing kunt handmatige failover tookeep Hallo schrijven status toohello regio waar er toobe active verkeer tijdens venster Hallo service-update gaat.

**Bedrijfscontinuïteit en herstel na noodgevallen (BCDR) en High Availability and Disaster Recovery (HADR) zoomt**: bedrijfstoepassingen in de meeste zakelijke continuïteit tests opnemen als onderdeel van het proces voor ontwikkeling en release. BCDR- en HADR testen is vaak een belangrijke stap in de naleving certificeringen en aansprakelijke servicebeschikbaarheid in geval van regionale uitval Hallo. U kunt Hallo BCDR gereedheid van uw toepassingen die gebruikmaken van de Cosmos-database voor opslag door de activering van een handmatige failover van de Cosmos-DB-account en/of toevoegen en verwijderen van een regio dynamisch testen.

In dit artikel bekeken we hoe handmatige en automatische failovers werk in Cosmos-database en hoe u uw Cosmos-DB-accounts en -toepassingen toobe algemeen beschikbaar kunt configureren. U kunt met behulp van de globale Replicatieondersteuning Cosmos-database, end-to-end-latentie verbeteren en ervoor te zorgen dat ze maximaal beschikbaar, zelfs in geval van storingen regio Hallo. 

## <a id="NextSteps"></a>Volgende stappen
* Meer informatie over hoe Cosmos DB ondersteunt [globale distributie](distribute-data-globally.md)
* Meer informatie over [globale consistentie met Azure Cosmos-DB](consistency-levels.md)
* Ontwikkelen met meerdere regio's met behulp van Azure Cosmos DB [DocumentDB-API](../cosmos-db/tutorial-global-distribution-documentdb.md)
* Meer informatie over hoe toobuild [meerdere landen/regio writer architecturen](multi-region-writers.md) met Azure DocumentDB

