---
title: aaaTransactions en modi in Azure Service Fabric betrouwbare verzamelingen | Microsoft Docs
description: Azure Service Fabric betrouwbare status Manager en betrouwbare verzamelingen transacties en vergrendelen.
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
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Transacties en -modi in Azure Service Fabric betrouwbare verzamelingen

## <a name="transaction"></a>Transactie
Een transactie is een reeks bewerkingen die worden uitgevoerd als één logische eenheid van het werk.
Een transactie moet vertonen Hallo ACID-eigenschappen te volgen. (Zie: https://technet.microsoft.com/en-us/library/ms190612)
* **Atomisch**: een transactie moet een atomic-eenheid van het werk. Met andere woorden, de gegevenswijzigingen worden uitgevoerd of geen van beide wordt uitgevoerd.
* **Consistentie**: wanneer voltooid, een transactie moet laten staan alle gegevens in een consistente status. Alle interne gegevensstructuren moet juist achter Hallo Hallo transactie.
* **Isolatie**: wijzigingen aangebracht door gelijktijdige transacties worden geïsoleerd van Hallo-wijzigingen die zijn aangebracht door andere gelijktijdige transacties. Hallo-isolatieniveau gebruikt voor een bewerking binnen een ITransaction wordt bepaald door Hallo IReliableState presterende Hallo-bewerking.
* **Duurzaamheid**: nadat een transactie is voltooid, de gevolgen ervan permanent aanwezig zijn in Hallo-systeem. Hallo wijzigingen behouden blijven zelfs in geval van een systeemfout Hallo.

### <a name="isolation-levels"></a>Isolatieniveaus
Isolatieniveau definieert Hallo mate toowhich Hallo transactie worden geïsoleerd van wijzigingen aangebracht door andere transacties.
Er zijn twee isolatieniveaus die worden ondersteund in betrouwbare verzamelingen:

* **Herhaalbare leesbewerking**: Hiermee geeft u de instructies kunnen gegevens die zijn gewijzigd, maar nog niet zijn doorgevoerd door andere transacties worden gelezen en dat er geen andere transacties gegevens die is gelezen door de huidige transactie Hallo totdat de huidige Hallo kunnen wijzigen transactie is voltooid. Zie voor meer informatie [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).
* **Momentopname**: geeft aan dat gegevens gelezen door een instructie in een transactie Hallo transactioneel consistent versie van Hallo-gegevens die beschikbaar op Hallo Hallo transactie is gestart waren.
  Hallo transactie herkent alleen gegevenswijzigingen die zijn toegewezen voordat Hallo Hallo transactie is gestart.
  Gegevenswijzigingen na Hallo starten van de huidige transactie Hallo aangebracht door andere transacties zijn niet zichtbaar toostatements wordt uitgevoerd in de huidige transactie Hallo.
  Hallo effect is als Hallo-instructies in een transactie ophalen van een momentopname van Hallo doorgevoerd gegevens zoals deze bestond op Hallo Hallo transactie is gestart.
  Momentopnamen zijn consistent in betrouwbare verzamelingen.
  Zie voor meer informatie [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).

Betrouwbare verzamelingen kiezen automatisch Hallo isolatie niveau toouse voor een bepaalde leesbewerking afhankelijk van Hallo bewerking en Hallo-rol van Hallo replica Hallo gelijktijdig met het maken van de transactie.
Hieronder volgt Hallo tabel ziet u standaardwaarden op siteniveau isolatie voor betrouwbare woordenlijst en wachtrij-bewerkingen.

| Bewerking \ rol | Primair | Secundair |
| --- |:--- |:--- |
| Één entiteit lezen |Herhaalbare lezen |Momentopname |
| Opsomming, aantal |Momentopname |Momentopname |

> [!NOTE]
> Algemene voorbeelden voor één entiteit bewerkingen zijn `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.
> 

Hallo betrouwbare woordenlijst zowel Hallo betrouwbare wachtrij ondersteuning voor lezen uw schrijft.
Met andere woorden, een schrijven binnen een transactie worden zichtbaar tooa volgende gelezen die toohello behoort dezelfde transactie.

## <a name="locks"></a>Vergrendelingen
In betrouwbare verzamelingen alle transacties implementeren strengere twee fase vergrendelen: een transactie komt niet vergrendelingen Hallo deze totdat Hallo transactie wordt beëindigd met een afbreking of een doorvoer heeft verkregen.

Betrouwbare woordenlijst gebruikt rijniveau vergrendelen voor alle bewerkingen van één entiteit.
Betrouwbare wachtrij, ruilt gelijktijdigheid van taken voor strikte transactionele FIFO-eigenschap.
Betrouwbare wachtrij maakt gebruik van bewerking niveau vergrendelingen zodat één transactie met `TryPeekAsync` en/of `TryDequeueAsync` en één transactie met `EnqueueAsync` tegelijk.
Houd er rekening mee dat toopreserve FIFO, als een `TryPeekAsync` of `TryDequeueAsync` ooit toetsenbordinvoer dat Hallo betrouwbare wachtrij leeg is, wordt ook vergrendeld `EnqueueAsync`.

Schrijven operations altijd exclusieve vergrendelingen overnemen.
Voor leesbewerkingen afhankelijk Hallo vergrendelen van een aantal factoren.
Een leesbewerking uitgevoerd met behulp van Snapshot-isolatie is vergrendelingsvrije.
Een herhaalbare leesbewerking standaard duurt gedeelde vergrendelingen.
Voor een leesbewerking die ondersteuning biedt voor herhaalbare leesbewerking wordt de gebruiker Hallo kunt vragen voor een vergrendeling Update in plaats van Hallo gedeelde vergrendeling.
Een Update-vergrendeling is dat een asymmetrische vergrendeling gebruikt tooprevent een gemeenschappelijk model impasse dat zich voordoet wanneer meerdere transacties resources voor mogelijke updates op een later tijdstip vergrendelen.

Hallo vergrendeling compatibiliteit matrix vindt u in de volgende tabel Hallo:

| Aanvragen \ verleend | Geen | Gedeeld | Update | Exclusieve |
| --- |:--- |:--- |:--- |:--- |
| Gedeeld |Er is geen conflict |Er is geen conflict |Conflict |Conflict |
| Update |Er is geen conflict |Er is geen conflict |Conflict |Conflict |
| Exclusieve |Er is geen conflict |Conflict |Conflict |Conflict |

Time-argument in Hallo betrouwbare verzamelingen-API's wordt gebruikt voor deadlock-detectie.
Bijvoorbeeld twee transacties (T1 en T2) probeert tooread en K1 bijwerken.
Het is mogelijk dat zij toodeadlock, omdat ze beide vergrendeling Hallo hebben gedeeld.
In dit geval wordt een of beide Hallo operations time-out.

Dit scenario impasse is een goed voorbeeld van hoe een vergrendeling Update impassen kunt voorkomen.

## <a name="next-steps"></a>Volgende stappen
* [Werken met betrouwbare verzamelingen](service-fabric-work-with-reliable-collections.md)
* [Betrouwbare Services meldingen](service-fabric-reliable-services-notifications.md)
* [Betrouwbare Services back-up en herstel (herstel na noodgevallen)](service-fabric-reliable-services-backup-restore.md)
* [Betrouwbaar status Manager-configuratie](service-fabric-reliable-services-configuration.md)
* [Referentie voor ontwikkelaars voor betrouwbare verzamelingen](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

