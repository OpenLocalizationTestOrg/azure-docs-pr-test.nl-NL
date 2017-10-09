---
title: aaaIntroduction tooReliable verzamelingen in Azure Service Fabric stateful services | Microsoft Docs
description: Service Fabric stateful services bieden betrouwbare verzamelingen waarmee u de maximaal beschikbare, schaalbare en lage latentie cloudtoepassingen toowrite.
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Inleiding tooReliable verzamelingen in Azure Service Fabric stateful services
Betrouwbare verzamelingen kunnen u maximaal beschikbare, schaalbare en lage latentie cloudtoepassingen toowrite, alsof u schreef toepassingen voor één computer. klassen in Hallo Hallo **Microsoft.ServiceFabric.Data.Collections** naamruimte leveren een verzameling van verzamelingen die uw status automatisch maximaal beschikbaar maken. Ontwikkelaars moeten tooprogram alleen toohello betrouwbare verzameling API's en laat betrouwbare verzamelingen Hallo gerepliceerd en lokale status beheren.

Hallo belangrijkste verschil tussen betrouwbare verzamelingen en andere technologieën voor hoge beschikbaarheid (zoals Redis, Azure Table-service en Azure Queue-service) is dat Hallo status wordt gehandhaafd lokaal Hallo service-exemplaar tijdens ook maximaal beschikbaar gesteld. Dit betekent dat:

* Alle leesbewerkingen zijn lokaal is, wat resulteert in een lage latentie en hoge gegevensdoorvoer leest.
* Alle schrijfbewerkingen rekening worden gebracht Hallo minimum aantal IOs-netwerk, wat in een lage latentie resulteert en hoge gegevensdoorvoer schrijft.

![Afbeelding van de evolutie van verzamelingen.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Betrouwbare verzamelingen kunnen worden beschouwd als Hallo natuurlijke evolutie van Hallo **System.Collections** klassen: een nieuwe set van verzamelingen die zijn ontworpen voor cloud en meerdere computers toepassingen en Hallo zonder te verhogen complexiteit voor Hallo-ontwikkelaar. Als zodanig zijn betrouwbare verzamelingen:

* Gerepliceerd: Statuswijzigingen worden gerepliceerd voor hoge beschikbaarheid.
* Persistent: Gegevens persistente toodisk voor duurzaamheid tegen grootschalige storingen (bijvoorbeeld een datacenter stroomstoring) zijn.
* Asynchroon: API's zijn asynchrone tooensure threads worden niet geblokkeerd wanneer de i/o aangaan.
* Transactionele: API's maken gebruik van Hallo abstractie van transacties zodat u eenvoudig meerdere betrouwbare verzamelingen binnen een service kunt beheren.

Betrouwbare verzamelingen bieden sterke consistentie wordt gegarandeerd dat buiten het Hallo vak toomake redeneren over de status van de toepassing is eenvoudiger.
Sterke consistentie wordt bereikt door ervoor te zorgen transactie doorvoeracties pas nadat de hele transactie Hallo is aangemeld een quorum meerderheid van replica's, met inbegrip van de primaire Hallo voltooien.
tooachieve zwakkere consistentie toepassingen kunnen erken back toohello client/aanvrager voordat Hallo asynchrone doorvoer wordt geretourneerd.

Hallo betrouwbare verzamelingen API's vormen een evolutie van gelijktijdige verzamelingen API's (gevonden in Hallo **System.Collections.Concurrent** naamruimte):

* Asynchrone: Retourneert een taak omdat, in tegenstelling tot gelijktijdige verzamelingen Hallo bewerkingen zijn gerepliceerd en bewaard.
* Geen out-parameters: maakt gebruik van `ConditionalValue<T>` tooreturn een bool en een waarde in plaats van out-parameters. `ConditionalValue<T>`lijkt `Nullable<T>` , maar geen T toobe een struct zijn vereist.
* Transacties: Maakt gebruik van een transactie object tooenable hello toogroup acties van de gebruiker op meerdere betrouwbare verzamelingen in een transactie.

Vandaag de dag **Microsoft.ServiceFabric.Data.Collections** bevat drie verzamelingen:

* [Betrouwbare woordenlijst](https://msdn.microsoft.com/library/azure/dn971511.aspx): vertegenwoordigt een verzameling gerepliceerde transactionele en asynchrone sleutel/waarde-paren. Vergelijkbare te**ConcurrentDictionary**, beide Hallo sleutel en waarde Hallo van elk type kan zijn.
* [Betrouwbare wachtrij](https://msdn.microsoft.com/library/azure/dn971527.aspx): vertegenwoordigt een gerepliceerde transactionele en asynchrone strikte first in, First-out ' (FIFO) wachtrij. Vergelijkbare te**ConcurrentQueue**, Hallo-waarde van elk type kan zijn.
* [Betrouwbare gelijktijdige wachtrij](service-fabric-reliable-services-reliable-concurrent-queue.md): vertegenwoordigt een gerepliceerde transactionele en asynchrone best-effort ordening van wachtrij voor hoge doorvoer. Vergelijkbare toohello **ConcurrentQueue**, Hallo-waarde van elk type kan zijn.

## <a name="next-steps"></a>Volgende stappen
* [Betrouwbare verzameling richtlijnen en aanbevelingen](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Werken met betrouwbare verzamelingen](service-fabric-work-with-reliable-collections.md)
* [Transacties en vergrendelingen](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Betrouwbare status Manager en interne werking van verzameling](service-fabric-reliable-services-reliable-collections-internals.md)
* Het beheren van gegevens
  * [Back-up en herstel](service-fabric-reliable-services-backup-restore.md)
  * [Meldingen](service-fabric-reliable-services-notifications.md)
  * [Betrouwbare verzamelingserialisatie](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Serialisatie en Upgrade](service-fabric-application-upgrade-data-serialization.md)
  * [Betrouwbaar status Manager-configuratie](service-fabric-reliable-services-configuration.md)
* Andere
  * [Betrouwbare Services snel starten](service-fabric-reliable-services-quick-start.md)
  * [Referentie voor ontwikkelaars voor betrouwbare verzamelingen](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
