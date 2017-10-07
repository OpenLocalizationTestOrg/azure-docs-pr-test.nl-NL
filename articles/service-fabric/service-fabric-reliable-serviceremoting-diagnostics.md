---
title: aaaAzure ServiceFabric diagnostische gegevens en controle | Microsoft Docs
description: Dit artikel wordt beschreven Hallo prestaties bewakingsfuncties in Hallo betrouwbare ServiceRemoting van Service Fabric-runtime, zoals die door deze prestatiemeteritems.
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Diagnostische gegevens en Prestatiebewaking voor betrouwbare Service voor externe toegang
Hallo betrouwbare ServiceRemoting runtime verzendt [prestatiemeteritems](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Deze biedt mogelijk inzicht in hoe Hallo ServiceRemoting functioneert en helpt bij het oplossen van problemen en de bewaking van toepassingsprestaties.


## <a name="performance-counters"></a>Prestatiemeteritems
Hallo betrouwbare ServiceRemoting runtime definieert Hallo categorieën voor prestatiemeteritems te volgen:

| Category | Beschrijving |
| --- | --- |
| Service Fabric-Service |Prestatiemeteritems van de specifieke tooAzure Service Fabric-Service voor externe toegang, bijvoorbeeld de gemiddelde tijd tooprocess aanvragen |
| Service Fabric-Service-methode |Specifieke toomethods tellers geïmplementeerd door de Service Fabric Remoting Service, bijvoorbeeld hoe vaak een servicemethode wordt aangeroepen |

Elk Hallo categorieën voorafgaand aan heeft een of meer items.

Hallo [Windows Prestatiemeter](https://technet.microsoft.com/library/cc749249.aspx) toepassing die beschikbaar zijn in de Windows-besturingssysteem Hallo standaard gebruikte toocollect en bekijk prestatiemeteritemgegevens kan zijn. [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) is een andere optie voor het verzamelen van gegevens van prestatiemeteritems en uploaden tooAzure tabellen.

### <a name="performance-counter-instance-names"></a>Namen van prestatiemeteritems exemplaar
Een cluster met een groot aantal ServiceRemoting services of partities hebben een groot aantal exemplaren van prestaties teller. Hallo exemplaar van prestatiemeteritem namen helpen kunnen bij het identificeren van specifieke partitie Hallo en Service-methode (indien van toepassing) die Hallo exemplaar van prestatiemeteritem is gekoppeld.

#### <a name="service-fabric-service-category"></a>Service Fabric-Service-categorie
Voor Hallo categorie `Service Fabric Service`, Hallo teller exemplaarnamen worden in de volgende indeling Hallo:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* Hallo tekenreeksweergave van Hallo Service Fabric-partitie-ID die Hallo exemplaar van prestatiemeteritem gekoppeld is. Hallo partitie-ID is een GUID en de tekenreeksvoorstelling wordt gegenereerd via Hallo [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) methode met indelingsopgave "D".

*ServiceReplicaOrInstanceId* Hallo tekenreeksweergave van Hallo Service Fabric Replica/exemplaar-ID die Hallo exemplaar van prestatiemeteritem is gekoppeld.

*ServiceRuntimeInternalID* Hallo tekenreeksweergave van een 64-bits geheel getal dat wordt gegenereerd door Hallo Service Fabric-runtime voor intern gebruik. Dit is opgenomen in het exemplaar van prestatiemeteritem Hallo tooensure Uniekheid van de naam en te voorkomen dat veroorzaken een conflict met andere exemplaarnamen van prestatiemeteritems. Gebruikers moeten toointerpret niet proberen deze deel van naam exemplaar Prestatiemeter Hallo.

Hallo Hieronder volgt een voorbeeld van een naam van het exemplaar voor een item die deel uitmaakt van toohello `Service Fabric Service` categorie:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

In het voorgaande voorbeeld Hallo `2740af29-78aa-44bc-a20b-7e60fb783264` Hallo tekenreeksweergave van Hallo Service Fabric partitie-ID `635650083799324046` tekenreeksweergave van Replica/exemplaar-id en `5008379932` is Hallo 64-bits-ID die is gegenereerd voor Hallo runtime interne's gebruik.

#### <a name="service-fabric-service-method-category"></a>Methode voor de Service Fabric-categorie
Voor Hallo categorie `Service Fabric Service Method`, Hallo teller exemplaarnamen worden in de volgende indeling Hallo:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* is Hallo-naam van Hallo methode die een exemplaar van prestatiemeteritem Hallo is gekoppeld. Hallo-indeling van de naam van de methode hello wordt bepaald op basis van bepaalde logica in Service Fabric-runtime voor Hallo die een compromis tussen de leesbaarheid van Hallo-naam met beperkingen op Hallo maximale lengte van namen exemplaar Hallo van prestatiemeteritems voor Windows hello.

*ServiceRuntimeMethodId* Hallo tekenreeksweergave van een 32-bits geheel getal dat wordt gegenereerd door Hallo Service Fabric-runtime voor intern gebruik. Dit is opgenomen in het exemplaar van prestatiemeteritem Hallo tooensure Uniekheid van de naam en te voorkomen dat veroorzaken een conflict met andere exemplaarnamen van prestatiemeteritems. Gebruikers moeten toointerpret niet proberen deze deel van naam exemplaar Prestatiemeter Hallo.

*ServiceFabricPartitionID* Hallo tekenreeksweergave van Hallo Service Fabric-partitie-ID die Hallo exemplaar van prestatiemeteritem gekoppeld is. Hallo partitie-ID is een GUID en de tekenreeksvoorstelling wordt gegenereerd via Hallo [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) methode met indelingsopgave "D".

*ServiceReplicaOrInstanceId* Hallo tekenreeksweergave van Hallo Service Fabric Replica/exemplaar-ID die Hallo exemplaar van prestatiemeteritem is gekoppeld.

*ServiceRuntimeInternalID* Hallo tekenreeksweergave van een 64-bits geheel getal dat wordt gegenereerd door Hallo Service Fabric-runtime voor intern gebruik. Dit is opgenomen in het exemplaar van prestatiemeteritem Hallo tooensure Uniekheid van de naam en te voorkomen dat veroorzaken een conflict met andere exemplaarnamen van prestatiemeteritems. Gebruikers moeten toointerpret niet proberen deze deel van naam exemplaar Prestatiemeter Hallo.

Hallo Hieronder volgt een voorbeeld van een naam van het exemplaar voor een item die deel uitmaakt van toohello `Service Fabric Service Method` categorie:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

In het voorgaande voorbeeld Hallo `ivoicemailboxservice.leavemessageasync` Hallo methodenaam is `2` Hallo 32-bits-ID die is gegenereerd voor Hallo runtime interne's gebruikt, is `89383d32-e57e-4a9b-a6ad-57c6792aa521` Hallo tekenreeksweergave van Hallo Service Fabric partitie-ID`635650083804480486` Hallo tekenreeks weergave van Hallo Service Fabric-Replica-exemplaar-ID en `5008380` Hallo 64-bits-ID die is gegenereerd voor Hallo runtime interne's gebruiken.

## <a name="list-of-performance-counters"></a>Lijst met prestatiemeteritems
### <a name="service-method-performance-counters"></a>Prestatiemeteritems voor service-methode

Hallo betrouwbare Service runtime publiceert Hallo prestaties tellers gerelateerde toohello uitvoering van de methoden te volgen.

| Categorienaam | Naam van het meteritem | Beschrijving |
| --- | --- | --- |
| Service Fabric-Service-methode |Aanroepen per seconde |Aantal keren dat Hallo servicemethode wordt aangeroepen per seconde |
| Service Fabric-Service-methode |Gemiddeld aantal milliseconden per aanroep |Gebruikte tijd tooexecute Hallo servicemethode in milliseconden |
| Service Fabric-Service-methode |Opgetreden uitzonderingen per seconde |Aantal keren dat Hallo servicemethode heeft een uitzondering gegenereerd per seconde |

### <a name="service-request-processing-performance-counters"></a>Prestatiemeteritems voor service-aanvraag verwerken
Wanneer een client een methode via een proxy serviceobject aanroept, resulteert dit in een bericht wordt verzonden via Hallo netwerk toohello remoting service. Hallo-service verwerkt aanvraag het Hallo-bericht en stuurt een reactie terug toohello-client. Hallo betrouwbare ServiceRemoting runtime publiceert Hallo prestaties tellers gerelateerde tooservice aanvraagverwerking te volgen.

| Categorienaam | Naam van het meteritem | Beschrijving |
| --- | --- | --- |
| Service Fabric-Service |Aantal openstaande aanvragen |Het aantal aanvragen in Hallo-service wordt verwerkt |
| Service Fabric-Service |Gemiddeld aantal milliseconden per aanvraag |Gebruikte tijd (in milliseconden) door Hallo service tooprocess een aanvraag |
| Service Fabric-Service |Gemiddeld aantal milliseconden voor de deserialisatie van aanvragen |Tijd (in milliseconden) genomen toodeserialize service request-bericht wanneer het is ontvangen door het Hallo-service |
| Service Fabric-Service |Gemiddeld aantal milliseconden voor de serialisatie van reacties |Tijd (in milliseconden) genomen tooserialize Hallo service-antwoordbericht op Hallo service voordat antwoord Hallo toohello client wordt verzonden |

## <a name="next-steps"></a>Volgende stappen
* [Voorbeeldcode](https://github.com/Azure/servicefabric-samples)
* [EventSource providers op PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
