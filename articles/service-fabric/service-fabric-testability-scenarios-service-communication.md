---
title: 'Testbaarheid: Service communicatie | Microsoft Docs'
description: Service to service-communicatie is een kritieke integratie van een Service Fabric-toepassing. Dit artikel worden de overwegingen bij het ontwerpen en testen technieken.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Service Fabric-testbaarheid scenario's: Service-communicatie
Microservices en architectuur stijlen service oriented vlak natuurlijk in Azure Service Fabric. In deze soorten architecturen voor gedistribueerde, samengestelde microservice toepassingen doorgaans bestaan uit meerdere services die tootalk tooeach andere moeten. In het eenvoudigste gevallen zelfs hello, in het algemeen hebt u ten minste een stateless webservice en een stateful data storage-service die toocommunicate nodig.

Service to service-communicatie is een kritieke integratie van een toepassing, omdat elke service een API-services voor externe tooother beschrijft. Werken met een reeks API grenzen waarbij i/o over het algemeen moet zorgvuldig te werk gaan, met een goede hoeveelheid testen en valideren.

Er zijn talrijke overwegingen toomake wanneer deze servicegrenzen samen in een gedistribueerde systeem zijn bekabelde:

* *Transportprotocol*. Wilt u HTTP voor verbeterde interoperabiliteit of een aangepaste binaire protocol gebruiken voor maximale doorvoer?
* *Foutafhandeling*. Hoe wordt permanent en tijdelijke fouten worden verwerkt? Wat er gebeurt als een service tooa ander knooppunt verplaatst?
* *Time-outs en latentie*. In een toepassingen, hoe elke servicelaag omgaan latentie via Hallo-netwerkstack en toohello gebruiker?

Of u een communicatie-onderdelen voor Hallo ingebouwde service is geleverd door de Service Fabric gebruiken of u uw eigen bouwt, is testen van Hallo interacties tussen uw services kritieke tooensuring tolerantie in uw toepassing.

## <a name="prepare-for-services-toomove"></a>Voorbereiden op services toomove
Service-exemplaren kunnen navigeren gedurende een bepaalde periode. Dit geldt met name wanneer ze zijn geconfigureerd met metrische gegevens load balancing optimale resource aangepaste afgestemd. Service Fabric verplaatst uw service-exemplaren toomaximize hun beschikbaarheid zelfs tijdens upgrades, failovers, scale-out en andere situaties die zich tijdens Hallo levensduur van een gedistribueerde systeem voordoen.

Als services Hallo-cluster navigeren, uw clients en andere services worden voorbereid toohandle twee scenario's wanneer ze tooa service communiceren:

* Hallo-service-exemplaar of partitie replica is sinds de laatste keer dat er tooit is besproken Hallo verplaatst. Dit is een normaal onderdeel van de levensduur van een service en het verwachte toohappen moet tijdens de levensduur van uw toepassing hello.
* Hallo-service-exemplaar of partitie replica wordt Hallo-proces voor de upgrade. Hoewel de failover van een service vanuit één knooppunt tooanother wordt zeer snel in Service Fabric mogelijk zijn er een vertraging in de beschikbaarheid als onderdeel van de Hallo communicatie van uw service toostart traag is.

Afhandeling van deze scenario's zonder problemen is belangrijk voor een systeem vloeiend worden uitgevoerd. toodo, houd er rekening mee dat:

* Alle services die verbonden toohas worden kan een *adres* die deze luistert op (bijvoorbeeld HTTP of WebSockets). Als u een service-exemplaar of de partitie worden verplaatst, verandert de adres-eindpunt. (Deze verplaatst tooa ander knooppunt met een ander IP-adres). Als u Hallo ingebouwde communicatie-onderdelen, worden ze opnieuw het omzetten van adressen van de service voor u verwerken.
* Er is mogelijk een tijdelijke toename in latentie van de service als Hallo het starten van service-exemplaar van de listener opnieuw. Dit is afhankelijk van hoe snel Hallo service Hallo-listener opent nadat Hallo service-exemplaar is verplaatst.
* De bestaande verbindingen moeten toobe gesloten en heropend nadat het Hallo-service op een nieuw knooppunt wordt geopend. Kan de tijd voor bestaande verbindingen toobe afsluiten een correcte knooppunt afsluiten of opnieuw opstarten.

### <a name="test-it-move-service-instances"></a>Het testen: service-exemplaren verplaatsen
Met behulp van Service Fabric-testbaarheid hulpprogramma's, kunt u schrijven een test scenario tootest deze situaties op verschillende manieren:

1. Verplaats de primaire replica van een stateful service.
   
    Hallo kan primaire replica van een partitie stateful service worden verplaatst voor een aantal redenen. Gebruik deze tootarget Hallo primaire replica van een specifieke partitie toosee hoe uw toohello van services reageren op een zeer gecontroleerde manier verplaatsen.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. Een knooppunt stoppen.
   
    Wanneer een knooppunt is gestopt, Hallo Service Fabric-verplaatst alle Hallo service-exemplaren of partities die zich op dat knooppunt tooone van andere beschikbare knooppunten in cluster Hallo. Gebruik deze tootest een situatie waarbij een knooppunt van het cluster verloren en alle Hallo service-exemplaren en replica's op dat knooppunt toomove zijn.
   
    U kunt een knooppunt met behulp van PowerShell Hallo stoppen **Stop ServiceFabricNode** cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>Beschikbaarheid van Services onderhouden
Als een platform is Service Fabric ontworpen tooprovide hoge beschikbaarheid van uw services. Maar in uitzonderlijke gevallen onderliggende infrastructuurproblemen kunnen nog steeds niet beschikbaar zijn. Het is belangrijk tootest voor deze scenario's te.

De status van een quorum-systeem tooreplicate stateful services gebruiken voor hoge beschikbaarheid. Dit betekent dat een quorum van replica's toobe beschikbaar tooperform schrijfbewerkingen moet. In zeldzame gevallen, zoals een wijdverbreid hardwarefout een quorum van replica's mogelijk niet beschikbaar. In dergelijke gevallen kunnen tooperform schrijfbewerkingen u niet meer worden, maar u zich nog steeds kunnen tooperform leesbewerkingen.

### <a name="test-it-write-operation-unavailability"></a>Het testen: bewerking onbeschikbaarheid schrijven
Met Hallo testbaarheid hulpprogramma's in Service Fabric, kunt u een fout die quorumverlies als test induceert invoeren. Hoewel dit scenario zeldzame, is het belangrijk dat clients en -services die afhankelijk van een stateful service zijn toohandle situaties waar ze geen aanbrengen aanvragen tooit schrijven worden voorbereid. Het is ook belangrijk dat Hallo stateful service zelf op de hoogte van deze mogelijkheid is en probleemloos toocallers communiceren kan.

U kunt quorumverlies veroorzaken met behulp van PowerShell Hallo **Invoke-ServiceFabricPartitionQuorumLoss** cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

In dit voorbeeld wordt ingesteld `QuorumLossMode` te`QuorumReplicas` tooindicate die we tooinduce quorumverlies willen zonder omlaag alle replica's. Op deze manier leesbewerkingen zijn nog steeds mogelijk. tootest een scenario waarbij een volledige partitie niet beschikbaar is, u kunt deze schakeloptie te instellen`AllReplicas`.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over testbaarheid acties](service-fabric-testability-actions.md)

[Meer informatie over testbaarheid scenario 's](service-fabric-testability-scenarios.md)

