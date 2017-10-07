---
title: aaaGuidelines & aanbevelingen voor betrouwbare verzamelingen in Azure Service Fabric | Microsoft Docs
description: Richtlijnen en aanbevelingen voor het gebruik van betrouwbare Service Fabric-verzamelingen
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
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Richtlijnen en aanbevelingen voor betrouwbare verzamelingen in Azure Service Fabric
Deze sectie bevat richtlijnen voor het gebruik van betrouwbare statusbeheer en betrouwbare verzamelingen. Hallo-doel is niet voor verrassingen toohelp gebruikers.

Hallo richtlijnen zijn ingedeeld als eenvoudige aanbevelingen die worden voorafgegaan door Hallo voorwaarden *doen*, *Overweeg*, *Vermijd* en *niet*.

* Een object van het aangepaste type dat wordt geretourneerd door leesbewerkingen mag niet worden gewijzigd (bijvoorbeeld `TryPeekAsync` of `TryGetValueAsync`). Betrouwbare verzamelingen, net als bij gelijktijdige verzamelingen, een toohello reference-objecten en geen kopie geretourneerd.
* Doe diepe kopie Hallo object van een aangepast type geretourneerd voordat u deze wijzigt. Aangezien structs en ingebouwde typen pass-by-value, hoeft u niet toodo een diepe kopie op deze.
* Gebruik geen `TimeSpan.MaxValue` voor time-outs. Time-outs moet gebruikte toodetect impassen.
* Gebruik een transactie niet nadat deze is toegewezen, is afgebroken, of verwijderd.
* Gebruik een opsomming niet buiten Hallo transactiebereik die is gemaakt in.
* Maak een transactie in een andere transactie geen `using` instructie omdat dit ertoe leiden impassen dat kan.
* Kan ervoor zorgen dat uw `IComparable<TKey>` implementatie juist is. Hallo system neemt afhankelijkheid `IComparable<TKey>` voor het samenvoegen van controlepunten en rijen.
* Gebruik vergrendeling tijdens bijwerken bij het lezen van een item met een tooupdate bedoeling deze tooprevent een bepaalde klasse impassen.
* Overweeg te houden van uw objecten (bijvoorbeeld TKey + TValue voor betrouwbare woordenlijst) lager dan 80 kB: kleinere Hallo beter. Dit vermindert Hallo hoeveelheid Heap voor grote objecten gebruik, evenals de schijf en netwerk i/o-vereisten. Vaak vermindert dubbele gegevens repliceren wanneer er slechts één klein onderdeel van het Hallo-waarde wordt bijgewerkt. Algemene manier tooachieve dit betrouwbare woordenlijst is toobreak uw rijen in toomultiple rijen.
* Overweeg het gebruik van back-up en herstel na noodgevallen van functionaliteit toohave herstellen.
* Voorkomen dat de combinatie van één entiteit operations en bewerkingen voor meerdere entiteiten (bijvoorbeeld `GetCountAsync`, `CreateEnumerableAsync`) in Hallo dezelfde transactie vanwege de verschillende isolatieniveaus toohello.
* InvalidOperationException worden verwerkt. Door Hallo-systeem voor het aantal redenen kunnen gebruikerstransacties worden afgebroken. Bijvoorbeeld, blokkeert wanneer Hallo betrouwbare status Manager de rol buiten-primaire wordt gewijzigd of wanneer een transactie langlopende afkappen van Hallo transactionele logboek. In dergelijke gevallen ontvangt gebruiker InvalidOperationException die aangeeft dat de transactie al is beëindigd. Ervan uitgaande dat, Hallo beëindiging van het Hallo-transactie is niet aangevraagd door gebruiker Hallo, de aanbevolen manier toohandle deze uitzondering is toodispose Hallo transactie, Controleer of Hallo annulering token zijn gesignaleerd (of Hallo-rol van Hallo replica is gewijzigd), en als dat niet Maak een nieuwe transactie en probeer het opnieuw.  

Hier volgen enkele dingen tookeep rekening:

* Hallo standaardtime-out is vier seconden voor alle Hallo betrouwbare verzameling API's. De meeste gebruikers gebruik Hallo standaardtime-out.
* Hallo standaard annulering token is `CancellationToken.None` in alle betrouwbare verzamelingen-API's.
* Hallo sleuteltype-parameter (*TKey*) voor een betrouwbare woordenlijst correct moet implementeren `GetHashCode()` en `Equals()`. Sleutels moeten niet-wijzigbaar.
* tooachieve hoge beschikbaarheid voor Hallo betrouwbare verzamelingen, elke service moet hebben ten minste een doel en de minimale grootte van 3 replicaset.
* Leesbewerkingen op Hallo secundaire versies die niet doorgevoerd quorum zijn mag worden gelezen.
  Dit betekent dat een versie van de gegevens die worden gelezen van een enkel secundaire ONWAAR kan worden gevorderd.
  Leesbewerkingen van primaire zijn altijd stabiele: kan nooit worden false gevorderd.

### <a name="next-steps"></a>Volgende stappen
* [Werken met betrouwbare verzamelingen](service-fabric-work-with-reliable-collections.md)
* [Transacties en vergrendelingen](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Betrouwbare status Manager en interne werking van verzameling](service-fabric-reliable-services-reliable-collections-internals.md)
* Het beheren van gegevens
  * [Back-up en herstel](service-fabric-reliable-services-backup-restore.md)
  * [Meldingen](service-fabric-reliable-services-notifications.md)
  * [Serialisatie en Upgrade](service-fabric-application-upgrade-data-serialization.md)
  * [Betrouwbaar status Manager-configuratie](service-fabric-reliable-services-configuration.md)
* Andere
  * [Betrouwbare Services snel starten](service-fabric-reliable-services-quick-start.md)
  * [Referentie voor ontwikkelaars voor betrouwbare verzamelingen](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
