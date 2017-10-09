---
title: aaaOverview van Hallo levenscyclus van Azure Service Fabric Reliable Services | Microsoft Docs
description: Meer informatie over Hallo levenscyclus van andere gebeurtenissen in betrouwbare Service Fabric-services
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Overzicht van de levenscyclus van betrouwbare services
> [!div class="op_single_selector"]
> * [C# op Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java op Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Wanneer u nadenkt over Hallo levenscycli van Reliable Services, zijn Hallo basisprincipes van de levenscyclus van Hallo Hallo belangrijkste. In het algemeen:

* Tijdens het opstarten
  * Services zijn gebouwd
  * Ze hebben een kans tooconstruct en nul of meer listeners retourneren
  * Elke geretourneerde luisteraars worden geopend, zodat de communicatie met de Hallo-service
  * Hallo-Service runAsync-methode wordt aangeroepen, toe te staan Hallo service toodo langlopende of werk op de achtergrond
* Tijdens het afsluiten
  * Hallo annulering token doorgegeven toorunAsync wordt geannuleerd en Hallo-listeners zijn gesloten
  * Eenmaal is voltooid, wordt Hallo serviceobject zelf destructed

Er zijn details rond Hallo exacte ordening van deze gebeurtenissen. Hallo-volgorde van gebeurtenissen mogelijk in het bijzonder enigszins, afhankelijk van Hallo betrouwbare Service Stateless of Stateful wijzigen. Daarnaast hebben we voor stateful services toodeal met Hallo primaire wisselen scenario. Tijdens deze reeks Hallo-functie van primaire replica is overgedragen tooanother (of terugkomt) zonder Hallo-service is afgesloten. Ten slotte hebben we toothink over fout of storing voorwaarden.

## <a name="stateless-service-startup"></a>Staatloze service is gestart
levenscyclus van een staatloze service Hallo is zeer eenvoudig. Hier volgt Hallo volgorde van gebeurtenissen:

1. Hallo wordt Service samengesteld
2. Klik in de parallelle twee dingen gebeuren:
    - `StatelessService.createServiceInstanceListeners()`wordt aangeroepen en elke geretourneerde luisteraars worden geopend (`CommunicationListener.openAsync()` is aangeroepen voor elke listener)
    - Hallo van service runAsync-methode (`StatelessService.runAsync()`) wordt genoemd
3. Indien aanwezig, Hallo van service onOpenAsync methode is aangeroepen (in het bijzonder `StatelessService.onOpenAsync()` wordt aangeroepen. Dit is een onderdrukking ongewoon maar deze beschikbaar is).

Het is belangrijk toonote of er is geen ordening tussen Hallo aanroepen toocreate en open Hallo listeners en runAsync. Hallo-listeners geopend voordat runAsync wordt gestart. Op deze manier runAsync mogelijk uiteindelijk aangeroepen voordat de communicatielisteners Hallo geopend zijn of zelfs is samengesteld. Als geen synchronisatie vereist is, is het een oefening toohello implementeerder gehandhaafd. Algemene oplossingen:

* Soms werkt listeners alleen als andere informatie is gemaakt of gewerkte. Voor stateless services die werk meestal kan worden uitgevoerd in de constructor Hallo-service tijdens het Hallo `createServiceInstanceListeners()` aanroepen, of als onderdeel van het Hallo-constructie van Hallo-listener zelf.
* Soms wil hello code in runAsync niet toostart totdat het Hallo-listeners zijn geopend. In dit geval is aanvullende coördinatie nodig. Een veelgebruikte oplossing is een aantal markering binnen Hallo-listeners die aangeeft wanneer ze hebt voltooid, die wordt gecontroleerd in runAsync voordat u doorgaat tooactual werk.

## <a name="stateless-service-shutdown"></a>Afsluiten van de staatloze service
Wanneer een stateless service wordt afgesloten, wordt hello hetzelfde patroon gevolgd, alleen in omgekeerde volgorde:

1. Parallel
    - Alle open listeners zijn gesloten (`CommunicationListener.closeAsync()` is aangeroepen voor elke listener)
    - Hallo annulering token doorgegeven te`runAsync()` is geannuleerd (Hallo annulering token controleren `isCancelled` eigenschap true retourneert, en als het Hallo-token aangeroepen `throwIfCancellationRequested` methode er wordt een `CancellationException`)
2. Eenmaal `closeAsync()` is voltooid op elke listener en `runAsync()` ook is voltooid, Hallo-service `StatelessService.onCloseAsync()` methode wordt aangeroepen, indien aanwezig (opnieuw dit is een ongewoon onderdrukking).
3. Na `StatelessService.onCloseAsync()` is voltooid, Hallo serviceobject wordt destructed

## <a name="notes-on-service-lifecycle"></a>Opmerkingen bij de levenscyclus van de service
* Beide Hallo `runAsync()` methode en Hallo `createServiceInstanceListeners` aanroepen zijn optioneel. Een service kan één van deze beide of geen van beide hebben. Bijvoorbeeld, als het Hallo-service alle zijn werk in het antwoord toouser aanroepen doet, hoeft niet voor tooimplement `runAsync()`. Alleen Hallo communicatielisteners en hun bijbehorende code zijn nodig. Op deze manier maken communicatielisteners retourneren is optioneel, want het Hallo-service mogelijk alleen de achtergrond toodo werken en hoeft dus alleen tooimplement`runAsync()`
* Is geldig voor een service-toocomplete `runAsync()` is en dat het resultaat van deze. Dit wordt niet beschouwd als een voorwaarde is mislukt en zou vertegenwoordigen achtergrondwerk Hallo Hallo service om te voltooien. Voor stateful betrouwbare services `runAsync()` opnieuw zou worden aangeroepen als Hallo service werden gedegradeerd van primaire en vervolgens back tooprimary gepromoveerd.
* Als een service afsluit `runAsync()` door er een onverwachte uitzondering is opgetreden, dit is een fout en Hallo serviceobject wordt afgesloten en een statusfout gemeld.
* Hoewel er geen tijdslimiet bij het retourneren van deze methoden, kunt u onmiddellijk verliezen Hallo mogelijkheid toowrite en daarom echte werk niet voltooien. Het is raadzaam dat u zo snel mogelijk na ontvangst van de annuleringsaanvraag Hallo terugkeren. Als uw service toothese API-aanroepen niet reageert binnen een redelijk tijdsbestek die service Fabric mogelijk geforceerd uw service beëindigen. Meestal gebeurt dit alleen tijdens toepassingsupgrades of wanneer een service wordt verwijderd. Deze time-out is 15 minuten standaard.
* Fouten in Hallo `onCloseAsync()` pad leiden tot een `onAbort()` wordt aangeroepen dit is een kans van de laatste kans best-effort voor Hallo tooclean up service en laat alle bronnen die ze hebben aangevraagd.

> [!NOTE]
> Stateful betrouwbare services worden nog niet ondersteund in java.
>
>

## <a name="next-steps"></a>Volgende stappen
* [Inleiding tooReliable Services](service-fabric-reliable-services-introduction.md)
* [Betrouwbare Services snel starten](service-fabric-reliable-services-quick-start.md)
* [Reliable Services geavanceerde gebruik](service-fabric-reliable-services-advanced-usage.md)
