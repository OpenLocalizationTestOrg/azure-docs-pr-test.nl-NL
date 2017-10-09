---
title: aaaActors diagnostische gegevens en controle | Microsoft Docs
description: Dit artikel wordt beschreven Hallo diagnostische gegevens en functies in Hallo Service Fabric Reliable Actors runtime, met inbegrip van Hallo gebeurtenissen en prestatiemeteritems die zijn verzonden door het bewaken van de prestaties.
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Diagnose- en prestatiecontrole voor betrouwbare actoren
Hallo Reliable Actors runtime verzendt [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) gebeurtenissen en [prestatiemeteritems](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Deze biedt mogelijk inzicht in hoe Hallo runtime functioneert en helpt bij het oplossen van problemen en de bewaking van toepassingsprestaties.

## <a name="eventsource-events"></a>EventSource gebeurtenissen
Hallo EventSource providernaam voor Hallo Reliable Actors runtime is 'Microsoft-ServiceFabric-Actors'. Gebeurtenissen van de bron van deze gebeurtenissen worden weergegeven in Hallo [diagnostische gebeurtenissen](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) venster wanneer Hallo actor-toepassing wordt [fouten worden opgespoord in Visual Studio](service-fabric-debugging-your-application.md).

Voorbeelden van hulpprogramma's en -technologieën die helpen bij het verzamelen en/of het bekijken van EventSource gebeurtenissen zijn [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md), [semantische logboekregistratie](https://msdn.microsoft.com/library/dn774980.aspx), en Hallo [ Bibliotheek van Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Trefwoorden
Alle gebeurtenissen die deel uitmaken van toohello betrouwbare actoren EventSource zijn gekoppeld aan een of meer trefwoorden. Hierdoor kunnen voor het filteren van gebeurtenissen die worden verzameld. Hallo na sleutelwoord bits worden gedefinieerd.

| bits | Beschrijving |
| --- | --- |
| 0x1 |Instellen van belangrijke gebeurtenissen om samen te vatten Hallo-bewerking van Hallo actoren Fabric-runtime. |
| 0x2 |Verzameling van gebeurtenissen die actor methodeaanroepen beschrijven. Zie voor meer informatie, Hallo [inleidende informatie over actoren](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Verzameling van gebeurtenissen gerelateerde tooactor staat. Zie voor meer informatie Hallo onderwerp op [actor statusbeheer](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Het aantal gebeurtenissen gerelateerde tooturn gebaseerde gelijktijdigheid in Hallo actor. Zie voor meer informatie Hallo onderwerp op [gelijktijdigheid](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Prestatiemeteritems
Hallo Reliable Actors runtime definieert Hallo categorieën voor prestatiemeteritems te volgen.

| Category | Beschrijving |
| --- | --- |
| Service Fabric Actor |Prestatiemeteritems van specifieke tooAzure Service Fabric actoren, bijvoorbeeld tijd toosave actorstatus |
| Service Fabric-Actormethode |Prestatiemeteritems van de specifieke toomethods geïmplementeerd door de Service Fabric actoren, bijvoorbeeld hoe vaak een actormethode wordt aangeroepen |

Elk Hallo boven de categorieën heeft een of meer items.

Hallo [Windows Prestatiemeter](https://technet.microsoft.com/library/cc749249.aspx) toepassing die beschikbaar zijn in de Windows-besturingssysteem Hallo standaard gebruikte toocollect en bekijk prestatiemeteritemgegevens kan zijn. [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) is een andere optie voor het verzamelen van gegevens van prestatiemeteritems en uploaden tooAzure tabellen.

### <a name="performance-counter-instance-names"></a>Namen van prestatiemeteritems exemplaar
Een cluster met een groot aantal actorservices of actor-partities heeft een groot aantal actor prestaties teller exemplaren. Hallo exemplaarnamen van prestatiemeteritems helpen bij het identificeren van specifieke Hallo [partitie](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) en actormethode (indien van toepassing) die Hallo exemplaar van prestatiemeteritem is gekoppeld.

#### <a name="service-fabric-actor-category"></a>Service Fabric Actor-categorie
Voor Hallo categorie `Service Fabric Actor`, Hallo teller exemplaarnamen worden in de volgende indeling Hallo:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* Hallo tekenreeksweergave van Hallo Service Fabric-partitie-ID die Hallo exemplaar van prestatiemeteritem gekoppeld is. Hallo partitie-ID is een GUID en de tekenreeksvoorstelling wordt gegenereerd via Hallo [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) methode met indelingsopgave "D".

*ActorRuntimeInternalID* Hallo tekenreeksweergave van een 64-bits geheel getal dat wordt gegenereerd door Hallo actoren Fabric-runtime voor intern gebruik. Dit is opgenomen in het exemplaar van prestatiemeteritem Hallo tooensure Uniekheid van de naam en te voorkomen dat veroorzaken een conflict met andere exemplaarnamen van prestatiemeteritems. Gebruikers moeten toointerpret niet proberen deze deel van naam exemplaar Prestatiemeter Hallo.

Hallo Hieronder volgt een voorbeeld van een naam van het exemplaar voor een item die deel uitmaakt van toohello `Service Fabric Actor` categorie:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

In vorige Hallo voorbeeld `2740af29-78aa-44bc-a20b-7e60fb783264` Hallo tekenreeksweergave van Hallo Service Fabric partitie-ID en `635650083799324046` Hallo 64-bits-ID die is gegenereerd voor Hallo runtime interne's gebruiken.

#### <a name="service-fabric-actor-method-category"></a>Service Fabric-Actormethode categorie
Voor Hallo categorie `Service Fabric Actor Method`, Hallo teller exemplaarnamen worden in de volgende indeling Hallo:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* is Hallo-naam van Hallo actor-methode die een exemplaar van prestatiemeteritem Hallo is gekoppeld. Hallo-indeling van de naam van de methode hello wordt bepaald op basis van bepaalde logica in Hallo actoren Fabric-runtime die een compromis tussen de leesbaarheid van Hallo-naam met beperkingen op Hallo maximale lengte van namen exemplaar Hallo van prestatiemeteritems voor Windows hello.

*ActorsRuntimeMethodId* Hallo tekenreeksweergave van een 32-bits geheel getal dat wordt gegenereerd door Hallo actoren Fabric-runtime voor intern gebruik. Dit is opgenomen in het exemplaar van prestatiemeteritem Hallo tooensure Uniekheid van de naam en te voorkomen dat veroorzaken een conflict met andere exemplaarnamen van prestatiemeteritems. Gebruikers moeten toointerpret niet proberen deze deel van naam exemplaar Prestatiemeter Hallo.

*ServiceFabricPartitionID* Hallo tekenreeksweergave van Hallo Service Fabric-partitie-ID die Hallo exemplaar van prestatiemeteritem gekoppeld is. Hallo partitie-ID is een GUID en de tekenreeksvoorstelling wordt gegenereerd via Hallo [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) methode met indelingsopgave "D".

*ActorRuntimeInternalID* Hallo tekenreeksweergave van een 64-bits geheel getal dat wordt gegenereerd door Hallo actoren Fabric-runtime voor intern gebruik. Dit is opgenomen in het exemplaar van prestatiemeteritem Hallo tooensure Uniekheid van de naam en te voorkomen dat veroorzaken een conflict met andere exemplaarnamen van prestatiemeteritems. Gebruikers moeten toointerpret niet proberen deze deel van naam exemplaar Prestatiemeter Hallo.

Hallo Hieronder volgt een voorbeeld van een naam van het exemplaar voor een item die deel uitmaakt van toohello `Service Fabric Actor Method` categorie:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

In vorige Hallo voorbeeld `ivoicemailboxactor.leavemessageasync` Hallo methodenaam is `2` Hallo 32-bits-ID die is gegenereerd voor Hallo runtime interne's gebruikt, is `89383d32-e57e-4a9b-a6ad-57c6792aa521` Hallo tekenreeksweergave van Hallo Service Fabric partitie-ID en `635650083804480486` Hallo 64-bits-id gegenereerd voor intern gebruik Hallo-runtime.

## <a name="list-of-events-and-performance-counters"></a>Lijst met gebeurtenissen en prestatiemeters
### <a name="actor-method-events-and-performance-counters"></a>Acteur methode gebeurtenissen en prestatiemeteritems
Hallo Reliable Actors runtime verzendt Hallo-gebeurtenissen te volgen[actor methoden](service-fabric-reliable-actors-introduction.md).

| De naam van gebeurtenis | Gebeurtenis-ID | Niveau | Sleutelwoord | Beschrijving |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Uitgebreide |0x2 |Er is een actoren runtime over tooinvoke een actormethode. |
| ActorMethodStop |8 |Uitgebreide |0x2 |Uitvoering van een actormethode is voltooid. Dat wil zeggen, Hallo-runtime asynchrone aanroep toohello actormethode heeft geretourneerd en geretourneerd door actormethode Hallo Hallo-taak is voltooid. |
| ActorMethodThrewException |9 |Waarschuwing |0x3 |Er is een uitzondering opgetreden tijdens het uitvoeren van een actormethode Hallo van tijdens het Hallo-runtime asynchrone aanroep toohello actormethode of tijdens het uitvoeren van taak Hallo Hallo geretourneerd door Hallo actor-methode. Deze gebeurtenis geeft aan dat sommige sorteren van de fout in Hallo actor-code die onderzoek behoeften. |

Hallo Reliable Actors runtime publiceert Hallo prestaties tellers gerelateerde toohello uitvoering van actor methoden te volgen.

| Categorienaam | Naam van het meteritem | Beschrijving |
| --- | --- | --- |
| Service Fabric-Actormethode |Aanroepen per seconde |Aantal keren dat Hallo actorservicemethode wordt aangeroepen per seconde |
| Service Fabric-Actormethode |Gemiddeld aantal milliseconden per aanroep |Gebruikte tijd tooexecute hello actorservicemethode in milliseconden |
| Service Fabric-Actormethode |Opgetreden uitzonderingen per seconde |Aantal keren dat Hallo actorservicemethode uitzondering een gegenereerd per seconde |

### <a name="concurrency-events-and-performance-counters"></a>Gelijktijdigheid van gebeurtenissen en prestatiemeteritems
Hallo Reliable Actors runtime verzendt Hallo-gebeurtenissen te volgen[gelijktijdigheid](service-fabric-reliable-actors-introduction.md#concurrency).

| De naam van gebeurtenis | Gebeurtenis-ID | Niveau | Sleutelwoord | Beschrijving |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Uitgebreide |0x8 |Deze gebeurtenis wordt geschreven aan Hallo begin van elke nieuwe inschakelen in een actor. Het bevat aantal in behandeling zijnde actoraanroepen die wachten tooacquire Hallo afzonderlijke actorvergrendeling die wordt afgedwongen op basis van Schakel gelijktijdigheid Hallo. |

Hallo Reliable Actors runtime publiceert Hallo prestaties tellers gerelateerde tooconcurrency te volgen.

| Categorienaam | Naam van het meteritem | Beschrijving |
| --- | --- | --- |
| Service Fabric Actor |Aantal actoraanroepen die wachten op een actorvergrendeling |Aantal in behandeling zijnde actoraanroepen die wachten op tooacquire Hallo afzonderlijke actorvergrendeling die wordt afgedwongen op basis van Schakel gelijktijdigheid van taken |
| Service Fabric Actor |Gemiddeld aantal milliseconden wachttijd per vergrendeling |Tijd (in milliseconden) genomen tooacquire Hallo afzonderlijke actorvergrendeling die wordt afgedwongen op basis van Schakel gelijktijdigheid van taken |
| Service Fabric Actor |Gemiddeld aantal milliseconden actorvergrendeling vastgehouden |Tijd (in milliseconden) voor welke Hallo afzonderlijke actorvergrendeling wordt vastgehouden |

### <a name="actor-state-management-events-and-performance-counters"></a>Acteur status management gebeurtenissen en prestatiemeteritems
Hallo Reliable Actors runtime verzendt Hallo-gebeurtenissen te volgen[actor statusbeheer](service-fabric-reliable-actors-state-management.md).

| De naam van gebeurtenis | Gebeurtenis-ID | Niveau | Sleutelwoord | Beschrijving |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Uitgebreide |0x4 |Actoren runtime is over toosave hello actorstatus. |
| ActorSaveStateStop |11 |Uitgebreide |0x4 |Actoren runtime is klaar met het opslaan van de actorstatus Hallo. |

Hallo Reliable Actors runtime publiceert Hallo prestatiebeheer tellers gerelateerde tooactor status te volgen.

| Categorienaam | Naam van het meteritem | Beschrijving |
| --- | --- | --- |
| Service Fabric Actor |Gemiddeld aantal milliseconden per bewerking voor het opslaan van de status |Tijd van de actorstatus toosave in milliseconden |
| Service Fabric Actor |Gemiddeld aantal milliseconden per bewerking voor het laden van de status |Tijd van de actorstatus tooload in milliseconden |

### <a name="events-related-tooactor-replicas"></a>Gebeurtenissen gerelateerde tooactor replica 's
Hallo Reliable Actors runtime verzendt Hallo-gebeurtenissen te volgen[actor replica's](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| De naam van gebeurtenis | Gebeurtenis-ID | Niveau | Sleutelwoord | Beschrijving |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Informatief |0x1 |Acteur replica rol tooPrimary gewijzigd. Dit betekent dat Hallo actoren voor deze partitie binnen deze replica wordt gemaakt. |
| ReplicaChangeRoleFromPrimary |2 |Informatief |0x1 |Acteur replica gewijzigd toonon primaire rol. Dit betekent dat Hallo actoren voor deze partitie niet meer worden gemaakt binnen deze replica. Er zijn geen nieuwe aanvragen worden geleverd tooactors al in deze replica is gemaakt. Hallo actoren wordt verwijderd nadat alle aanvragen in uitvoering zijn voltooid. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Acteur activering en deactivering van gebeurtenissen en prestatiemeteritems
Hallo Reliable Actors runtime verzendt Hallo-gebeurtenissen te volgen[actor activering en deactivering](service-fabric-reliable-actors-lifecycle.md).

| De naam van gebeurtenis | Gebeurtenis-ID | Niveau | Sleutelwoord | Beschrijving |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Informatief |0x1 |Een actor is geactiveerd. |
| ActorDeactivated |6 |Informatief |0x1 |Een actor is gedeactiveerd. |

Hallo Reliable Actors runtime publiceert Hallo prestatiemeteritems te volgen verwante tooactor activering en deactivering.

| Categorienaam | Naam van het meteritem | Beschrijving |
| --- | --- | --- |
| Service Fabric Actor |Gemiddeld aantal milliseconden op OnActivateAsync |De methode OnActivateAsync tooexecute voor tijd in milliseconden |

### <a name="actor-request-processing-performance-counters"></a>Aanvraagverwerking actor-prestatiemeteritems
Wanneer een client een methode via een proxy actor object aanroept, resulteert dit in een bericht wordt verzonden via toohello Hallo-actor netwerkservice. Hallo-service verwerkt aanvraag het Hallo-bericht en stuurt een reactie terug toohello-client. Hallo Reliable Actors runtime publiceert Hallo prestaties tellers gerelateerde tooactor aanvraagverwerking te volgen.

| Categorienaam | Naam van het meteritem | Beschrijving |
| --- | --- | --- |
| Service Fabric Actor |Aantal openstaande aanvragen |Het aantal aanvragen in Hallo-service wordt verwerkt |
| Service Fabric Actor |Gemiddeld aantal milliseconden per aanvraag |Gebruikte tijd (in milliseconden) door Hallo service tooprocess een aanvraag |
| Service Fabric Actor |Gemiddeld aantal milliseconden voor de deserialisatie van aanvragen |Tijd (in milliseconden) genomen toodeserialize actor aanvraagbericht wanneer het is ontvangen door het Hallo-service |
| Service Fabric Actor |Gemiddeld aantal milliseconden voor de serialisatie van reacties |Tijd (in milliseconden) genomen tooserialize Hallo actor-antwoordbericht op Hallo service voordat antwoord Hallo toohello client wordt verzonden |

## <a name="next-steps"></a>Volgende stappen
* [Hoe Reliable Actors Hallo Service Fabric-platform gebruiken](service-fabric-reliable-actors-platform.md)
* [Acteur API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Voorbeeldcode](https://github.com/Azure/servicefabric-samples)
* [EventSource providers op PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
