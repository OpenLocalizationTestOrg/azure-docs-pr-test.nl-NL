---
title: Azure Service Fabric-terminologie aaaLearn | Microsoft Docs
description: Een overzicht van de terminologie van Service Fabric. Belangrijkste termen concepten en termen die in de rest van documentatie Hallo Hallo besproken.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Overzicht van service Fabric-terminologie
Service Fabric is een platform voor gedistribueerde systemen waarmee u eenvoudig toopackage kunt, implementeren en beheren van schaalbare en betrouwbare microservices. Dit onderwerp details Hallo terminologie die wordt gebruikt door de Service Fabric toounderstand Hallo gebruikte termen in Hallo-documentatie.

Hallo concepten die worden vermeld in deze sectie worden ook besproken in Hallo Microsoft Virtual Academy video's te volgen: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">concepten Core</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">ontwerptijd concepten</a>, en <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">runtime-concepten</a>.

## <a name="infrastructure-concepts"></a>Concepten van de infrastructuur
**Cluster**: een set netwerk verbonden virtuele of fysieke machines waarin uw microservices worden geïmplementeerd en beheerd.  Clusters kunnen schalen toothousands machines.

**Knooppunt**: een machine of virtuele machine die deel uitmaakt van een cluster een knooppunt wordt aangeroepen. Elk knooppunt wordt de knooppuntnaam van een (een tekenreeks) toegewezen. Knooppunten hebben kenmerken zoals plaatsingseigenschappen. Elke computer of virtuele machine heeft een Windows-service van het automatisch starten, `FabricHost.exe`, die begint bij het opstarten worden uitgevoerd en start vervolgens twee uitvoerbare bestanden: `Fabric.exe` en `FabricGateway.exe`. Deze twee uitvoerbare bestanden vormen Hallo-knooppunt. Voor het testen van scenario's, kunt u meerdere knooppunten op een enkele computer of virtuele machine host door het uitvoeren van meerdere exemplaren van `Fabric.exe` en `FabricGateway.exe`.

## <a name="application-concepts"></a>Concepten van toepassing
**Toepassingstype**: Hallo naam/versie toegewezen tooa verzameling servicetypen. Gedefinieerd in een `ApplicationManifest.xml` bestand, de installatiekopieopslag toohello Service Fabric-cluster van ingesloten in een toepassingsmap pakket, dat vervolgens is gekopieerd. Vervolgens kunt u een toepassing met de naam van dit toepassingstype binnen Hallo cluster maken.

Lees Hallo [toepassingsmodel](service-fabric-application-model.md) artikel voor meer informatie.

**Toepassingspakket**: een map met Hallo toepassingstype `ApplicationManifest.xml` bestand. Verwijzingen Hallo servicepakketten voor elk servicetype waaruit Hallo toepassingstype. Hallo-bestanden in de toepassingsmap pakket Hallo zijn gekopieerde tooService Fabric-cluster van image store. Een toepassingspakket voor een e-mailtype toepassing kan bijvoorbeeld verwijzingen tooa wachtrij servicepakket, frontend servicepakket en servicepakket database bevatten.

**Naam Application**: nadat een toepassingspakket gekopieerd toohello image store is, u een exemplaar van de toepassing hello binnen Hallo cluster maken door te geven Hallo toepassingspakket toepassingstype (met de naam/versie). Elk type toepassingsexemplaar krijgt een URI-naam die lijkt op: `"fabric:/MyNamedApp"`. U kunt meerdere benoemde toepassingen binnen een cluster maken van een type één toepassing. U kunt ook benoemde toepassingen maken van verschillende toepassingstypen. Elke toepassing met de naam is onafhankelijk van elkaar worden beheerd en samengestelde.      

**Service Type**: Hallo naam/versie toegewezen code pakketten, gegevenspakketten en configuratiepakketten tooa-service. Gedefinieerd in een `ServiceManifest.xml` ingesloten in een pakketmap service en de pakketmap Hallo-service-bestand vervolgens naar wordt verwezen door een toepassingspakket `ApplicationManifest.xml` bestand. Binnen Hallo-cluster kunt na het maken van een toepassing met de naam, u een service met de naam van een Hallo servicetypen toepassingstype. servicetype Hallo `ServiceManifest.xml` bestand beschrijft Hallo-service.

Lees Hallo [toepassingsmodel](service-fabric-application-model.md) artikel voor meer informatie.

Er zijn twee soorten services:

* **Stateless:** een stateless service gebruiken als de permanente status Hallo-service is opgeslagen in een service voor externe opslag zoals Azure Storage, Azure SQL Database of Azure Cosmos DB. Gebruik een stateless service wanneer Hallo-service geen permanente opslag helemaal heeft. Bijvoorbeeld, een rekenmachine service waarbij waarden worden doorgegeven toohello service, een berekening wordt uitgevoerd met deze waarden en een resultaat geretourneerd.
* **Stateful:** gebruik van een stateful service als u de status van uw service via de betrouwbare verzamelingen of Reliable Actors programming modellen voor Service Fabric toomanage wilt. Geef het aantal partities toospread uw status via (voor schaalbaarheid) wanneer gewenste een benoemde service maken. Ook opgeven hoe vaak tooreplicate uw status op de knooppunten (voor betrouwbaarheid). Elke benoemde service heeft een enkele primaire replica en meerdere secundaire replica's. U wijzigen uw benoemde servicestatus door de primaire replica toohello schrijven. Service Fabric repliceert vervolgens deze status tooall Hallo secundaire replica's uw status synchroon te houden. Service Fabric wordt automatisch gedetecteerd wanneer een primaire replica is mislukt en bijdraagt aan een bestaande primaire replica van de secundaire replica-tooa. Service Fabric maakt vervolgens een nieuwe secundaire replica.  

**Servicepakket**: een map met Hallo servicetype `ServiceManifest.xml` bestand. Dit bestand verwijst naar Hallo code, statische gegevens en configuratiepakketten voor het servicetype Hallo. Hallo-bestanden in de pakketmap Hallo-service wordt verwezen door Hallo toepassingstype `ApplicationManifest.xml` bestand. Een servicepakket kan bijvoorbeeld verwijzen toohello code, statische gegevens en configuratiepakketten die gezamenlijk een database-service.

**Service met de naam**: na het maken van een benoemde toepassing, kunt u een exemplaar van een van de servicetypen binnen Hallo cluster door te geven Hallo servicetype (met de naam/versie). Elk service type-exemplaar is de naam van een URI die onder de URI van de toepassing van het benoemde bereik toegewezen. Bijvoorbeeld, als u een service binnen een toepassing met de naam 'MyNamedApp' met de naam 'MijnDatabase' maakt, Hallo URI eruit: `"fabric:/MyNamedApp/MyDatabase"`. In een toepassing met de naam, kunt u verschillende benoemde services maken. Elke benoemde service kan de eigen partitieschema en exemplaar/replica telt.

**Pakket code**: een map met Hallo servicetype uitvoerbare bestanden (meestal EXE/DLL-bestanden). Hallo-bestanden in de pakketmap Hallo-code wordt verwezen door Hallo servicetype `ServiceManifest.xml` bestand. Wanneer een benoemde service hebt gemaakt, is het Hallo-codepakket gekopieerde toohello knooppunt of knooppunten geselecteerde toorun Hallo service met de naam. Vervolgens start Hallo code uitgevoerd. Er zijn twee soorten code pakket uitvoerbare bestanden:

* **Uitvoerbare bestanden Gast**: uitvoerbare bestanden die worden uitgevoerd als-is op Hallo hostbesturingssysteem (Windows of Linux). Dat wil zeggen, deze uitvoerbare bestanden komen niet tooor koppelingsverwijzing alle Service Fabric-runtime-bestanden en daarom een Service Fabric programming modellen niet gebruiken. Deze uitvoerbare bestanden zijn toouse die sommige Service Fabric-functies zoals Hallo naming service voor de detectie van het eindpunt. Gast uitvoerbare bestanden kan niet rapporteren load metrische gegevens specifieke tooeach service-exemplaar.
* **Service Host uitvoerbare bestanden**: uitvoerbare bestanden die gebruikmaken van Service Fabric modellen programming koppelt tooService Fabric-runtime-bestanden, Service Fabric-functies inschakelen. Bijvoorbeeld, een benoemd exemplaar eindpunten kunt registreren met Naming Service-Fabric-Service en load metrische gegevens ook kan rapporteren.      

**Gegevenspakket**: een map met de Hallo servicetype statische, alleen-lezen gegevensbestanden (meestal foto Beeld en geluid). Hallo-bestanden in Hallo gegevensdirectory van het pakket wordt verwezen door Hallo servicetype `ServiceManifest.xml` bestand. Wanneer een benoemde service hebt gemaakt, is het gegevenspakket Hallo gekopieerde toohello knooppunt of knooppunten geselecteerde toorun Hallo service met de naam.  Hallo-code wordt gestart en hebben nu toegang tot gegevensbestanden Hallo.

**Configuratiepakket**: een map met de Hallo servicetype statisch, de configuratie alleen-lezen-bestanden (meestal tekst). Hallo-bestanden in de configuratiemap pakket hello wordt verwezen door Hallo servicetype `ServiceManifest.xml` bestand. Wanneer een service met de naam wordt gemaakt, bestanden in het configuratiepakket Hallo Hallo zijn gekopieerde toohello een of meer knooppunten geselecteerde toorun Hallo benoemde service. Vervolgens Hallo code wordt gestart en hebben nu toegang tot de configuratiebestanden Hallo.

**Containers**: standaard, Service Fabric worden geïmplementeerd en wordt geactiveerd services als processen. Service Fabric kunnen ook services implementeren in container-installatiekopieën. Containers zijn een virtualisatietechnologie die Hallo onderliggende besturingssysteem van toepassingen virtualiseert. Een toepassing en de runtime, afhankelijkheden en system-bibliotheken worden uitgevoerd binnen een container met volledige, persoonlijke toegang toohello container eigen geïsoleerde weergave van besturingssysteem constructies. Service Fabric ondersteunt Docker-containers voor Linux en Windows Server-containers.  Lees voor meer informatie [Service Fabric en containers](service-fabric-containers-overview.md).

**Partitie-schema**: bij het maken van een benoemde service u een partitieschema opgeven. Hallo data Services met grote hoeveelheden status verdelen over partities Hallo status verspreid over Hallo clusterknooppunten. Hierdoor kan uw benoemde service status tooscale. Binnen een partitie hebben staatloze benoemde services de exemplaren stateful benoemde services replica's. Normaal gesproken staatloze benoemde services ooit slechts één partitie hebben omdat ze geen interne status hebben. Hallo partitie exemplaren bieden voor beschikbaarheid; Als één exemplaar is mislukt, andere exemplaren toooperate gewoon doorgaan en het Service Fabric maakt een nieuw exemplaar. Stateful services met de naam behouden hun status binnen de replica's en elke partitie heeft een eigen replicaset met alle Hallo status synchroon wordt gehouden. Moet een replica mislukken, Service Fabric-bouwt voort op een nieuwe replica van Hallo bestaande replica's.

Lees Hallo [partitie Service Fabric betrouwbare services](service-fabric-concepts-partitioning.md) artikel voor meer informatie.

## <a name="system-services"></a>Systeemservices
Er zijn systeemservices die zijn gemaakt in elk cluster waarmee Hallo platformmogelijkheden van Service Fabric.

**Naming Service**: elke Service Fabric-cluster heeft een Naming service, die wordt omgezet namen tooa servicelocatie in Hallo-cluster. U beheert Hallo servicenamen en eigenschappen, vergelijkbare tooan internet Service DNS (Domain Name) voor Hallo-cluster. Clients veilig te communiceren met een willekeurig knooppunt in het Hallo-cluster Hallo Naming Service tooresolve met de naam van een service en de locatie ervan.  Toepassingen verplaatsen binnen Hallo cluster bijvoorbeeld vanwege toofailures, resource netwerktaakverdeling of Hallo vergroten of verkleinen van Hallo cluster. U kunt ontwikkelen services en clients die de huidige netwerklocatie Hallo oplossen. Clients ophalen Hallo werkelijke machine IP-adres en poort waar deze momenteel wordt uitgevoerd.

Lees [communiceren met services](service-fabric-connect-and-communicate-with-services.md) voor meer informatie over Hallo client en service communicatie API's die met Hallo Naming service werken.

**Image Store-Service**: elke Service Fabric-cluster heeft een Image Store-service waarop de geïmplementeerde, samengestelde toepassingspakketten worden bewaard. Kopiëren van een toepassing pakket toohello Image Store en registreer Hallo toepassingstype is opgenomen in deze toepassingspakket. Nadat Hallo toepassingstype is ingericht, maakt u een toepassing met de naam ervan. U kunt registratie van een toepassingstype van Hallo Image Store-service nadat alle benoemde toepassingen zijn verwijderd.

Lees [hello ImageStoreConnectionString instelling begrijpen](service-fabric-image-store-connection-string.md) voor meer informatie over Hallo Image Store-service.

Lees Hallo [implementeren van een toepassing](service-fabric-deploy-remove-applications.md) artikel voor meer informatie over het implementeren van toepassingen toohello Image store-service.

## <a name="built-in-programming-models"></a>Ingebouwde programmeermodellen
.NET Framework-programmeermodellen zijn beschikbaar voor u toobuild Service Fabric-services:

**Reliable Services**: een API toobuild staatloze en stateful services. Stateful service voor het opslaan van hun status in betrouwbare verzamelingen (zoals een woordenboek of een wachtrij). U kunt ook tooplug ophalen in verschillende communicatie stapels zoals Web-API en Windows Communication Foundation (WCF).

**Reliable Actors**: een API toobuild staatloze en stateful-objecten via Hallo virtuele Actor programmeermodel. Dit model kan nuttig zijn wanneer er veel onafhankelijke eenheden van de berekening status. Omdat dit model een threadmodel Schakel gebaseerde gebruikt, is het aanbevolen tooavoid-code die illustreert tooother actoren of services omdat andere binnenkomende aanvragen door een afzonderlijke actor kan niet worden verwerkt totdat alle uitgaande aanvragen hebt voltooid.

Lees Hallo [een Programming Model voor uw service kiezen](service-fabric-choose-framework.md) artikel voor meer informatie.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
meer informatie over Service Fabric toolearn:

* [Overzicht van Service Fabric](service-fabric-overview.md)
* [Waarom een microservices benadering toobuilding toepassingen?](service-fabric-overview-microservices.md)
* [Toepassingsscenario's](service-fabric-application-scenarios.md)

