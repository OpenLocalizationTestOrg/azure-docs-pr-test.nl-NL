---
title: meer informatie over Azure Service Fabric aaaLearn | Microsoft Docs
description: Meer informatie over Hallo belangrijkste concepten en belangrijke gebieden van Azure Service Fabric. Biedt een uitgebreid overzicht van Service Fabric en hoe toocreate microservices.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>Daarom wilt u toolearn over Service Fabric?
Azure Service Fabric is een platform voor gedistribueerde systemen waarmee u eenvoudig toopackage kunt, implementeren en beheren van schaalbare en betrouwbare microservices.  Service Fabric heeft een groot oppervlak echter en er veel toolearn.  In dit artikel biedt een overzicht van Service Fabric en Hallo belangrijkste concepten, modellen, de levenscyclus van de toepassing, testen, clusters en statuscontrole programming beschrijft. Lees Hallo [overzicht](service-fabric-overview.md) en [wat zijn microservices?](service-fabric-overview-microservices.md) voor een inleiding en hoe Service Fabric gebruikte toocreate microservices kunt worden. In dit artikel bevat een uitgebreide lijst van de inhoud niet, maar koppelen toooverview en ophalen van gestarte artikelen voor elk gebied van Service Fabric. 

## <a name="core-concepts"></a>Basisconcepten
[Service Fabric-terminologie](service-fabric-technical-overview.md), [toepassingsmodel](service-fabric-application-model.md), en [ondersteund programmeermodellen](service-fabric-choose-framework.md) bieden meer concepten en beschrijvingen, maar hier vindt u basisprincipes Hallo.

<table><tr><th>Basisconcepten</th><th>Ontwerptijd</th><th>Tijdens het gebruik</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Ontwerptijd: toepassingstype, servicetype, toepassingspakket en manifest, servicepakket en manifest
Een toepassingstype is Hallo naam/versie tooa verzameling servicetype toegewezen. Dit is gedefinieerd in een *ApplicationManifest.xml* bestand, dat is ingesloten in een pakket toepassingsmap. Hallo-toepassingspakket wordt vervolgens gekopieerd toohello Service Fabric-cluster van image store. Vervolgens kunt u een toepassing met de naam van dit toepassingstype, die vervolgens wordt uitgevoerd binnen Hallo cluster maken. 

Een servicetype is Hallo naam/versie toegewezen code pakketten, gegevenspakketten en configuratiepakketten tooa-service. Dit is gedefinieerd in een bestand ServiceManifest.xml, die is ingesloten in een pakket servicemap. Hallo pakketmap service wordt gebruikt door een toepassingspakket *ApplicationManifest.xml* bestand. Binnen Hallo-cluster kunt na het maken van een toepassing met de naam, u een service met de naam van een Hallo servicetypen toepassingstype. Een servicetype is beschreven door de *ServiceManifest.xml* bestand. Hallo servicetype van uitvoerbare code service configuratie-instellingen, die worden geladen tijdens runtime, en statische gegevens dat wordt gebruikt door het Hallo-service bestaat.

![Service Fabric-toepassing waardetypen en servicetypen][cluster-imagestore-apptypes]

Hallo toepassingspakket is een map met Hallo toepassingstype *ApplicationManifest.xml* bestand, dat verwijst naar Hallo servicepakketten voor elk servicetype waaruit Hallo toepassingstype. Een toepassingspakket voor een e-mailtype toepassing kan bijvoorbeeld verwijzingen tooa wachtrij servicepakket, frontend servicepakket en servicepakket database bevatten. Hallo-bestanden in de toepassingsmap pakket Hallo zijn gekopieerde toohello Service Fabric-cluster van image store. 

Een servicepakket is een map met Hallo servicetype *ServiceManifest.xml* bestand, dat verwijst naar Hallo code, statische gegevens en configuratiepakketten voor het servicetype Hallo. Hallo-bestanden in de pakketmap Hallo-service wordt verwezen door Hallo toepassingstype *ApplicationManifest.xml* bestand. Een servicepakket kan bijvoorbeeld verwijzen toohello code, statische gegevens en configuratiepakketten die gezamenlijk een database-service.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>Uitvoeringstijd: clusters en knooppunten, toepassingen, services, partities en replica's met de naam met de naam
Een [Service Fabric-cluster](service-fabric-deploy-anywhere.md) is een met het netwerk verbonden reeks virtuele of fysieke machines waarop uw microservices worden geïmplementeerd en beheerd. Clusters kunnen schalen toothousands machines.

Een machine of virtuele machine die deel uitmaakt van een cluster wordt een knooppunt genoemd. Elk knooppunt wordt de knooppuntnaam van een (een tekenreeks) toegewezen. Knooppunten hebben kenmerken zoals plaatsingseigenschappen. Elke computer of virtuele machine heeft een Windows-service van het automatisch starten, `FabricHost.exe`, die begint bij het opstarten worden uitgevoerd en start vervolgens twee uitvoerbare bestanden: `Fabric.exe` en `FabricGateway.exe`. Deze twee uitvoerbare bestanden vormen Hallo-knooppunt. Voor ontwikkeling of Testscenario's, kunt u meerdere knooppunten op een enkele computer of virtuele machine host door het uitvoeren van meerdere exemplaren van `Fabric.exe` en `FabricGateway.exe`.

Een toepassing met de naam is een verzameling van benoemde services die een bepaalde functie of functies uitvoert. Een service vervult een functie volledig en zelfstandig (kunt starten en onafhankelijk van andere services worden uitgevoerd) en bestaat uit code, configuratie en gegevens. Nadat een toepassingspakket gekopieerd toohello image store is, kunt u een exemplaar van de toepassing hello binnen Hallo cluster maken door op te geven Hallo toepassingspakket toepassingstype (met de naam/versie). Elk type toepassingsexemplaar krijgt een URI-naam die lijkt op *fabric: / MyNamedApp*. U kunt meerdere benoemde toepassingen binnen een cluster maken van een type één toepassing. U kunt ook benoemde toepassingen maken van verschillende toepassingstypen. Elke toepassing met de naam is onafhankelijk van elkaar worden beheerd en samengestelde.

Na het maken van een benoemde toepassing, kunt u een exemplaar van een van de servicetypen (een benoemde service) binnen Hallo cluster door te geven Hallo servicetype (met de naam/versie). Elk service type-exemplaar is de naam van een URI die onder de URI van de toepassing van het benoemde bereik toegewezen. Bijvoorbeeld, als u een service binnen een toepassing met de naam 'MyNamedApp' met de naam 'MijnDatabase' maakt, Hallo URI eruit: *fabric: / MyNamedApp/MijnDatabase*. In een toepassing met de naam, kunt u een of meer benoemde services maken. Elke benoemde service kan de eigen partitieschema en exemplaar/replica telt. 

Er zijn twee soorten services: staatloze en stateful. Stateless services kunnen permanente status opslaan in een service voor externe opslag zoals Azure Storage, Azure SQL Database of Azure Cosmos DB. Gebruik een stateless service wanneer Hallo-service geen permanente opslag helemaal heeft. Een stateful service gebruikt Service Fabric toomanage status van uw service via de betrouwbare verzamelingen of Reliable Actors programming modellen. 

Bij het maken van een benoemde service, kunt u een partitieschema opgeven. Services met grote hoeveelheden status splitsen Hallo gegevens meerdere partities. Elke partitie is verantwoordelijk voor een deel van de volledige staat Hallo van Hallo-service, die wordt verspreid over Hallo clusterknooppunten. Binnen een partitie hebben staatloze benoemde services de exemplaren stateful benoemde services replica's. Normaal gesproken staatloze benoemde services ooit slechts één partitie hebben omdat ze geen interne status hebben. Stateful services met de naam behouden hun status binnen de replica's en elke partitie heeft een eigen replicaset. Lezen en schrijven bewerkingen worden uitgevoerd op één replica (Hallo primaire genoemd). Wijzigingen toostate van schrijven bewerkingen zijn gerepliceerd toomultiple andere replica's (actieve secundaire replica's genoemd). 

Hallo toont volgende diagram Hallo relatie tussen toepassingen en service-exemplaren, partities en replica's.

![Partities en replica's binnen een service][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Partitioneren, schaalbaarheid en beschikbaarheid
[Partitioneren](service-fabric-concepts-partitioning.md) is niet uniek tooService Fabric. Een bekende vorm van partitioneren is partitioneren van gegevens of sharding. Stateful services met grote hoeveelheden status splitsen Hallo gegevens meerdere partities. Elke partitie is verantwoordelijk voor een deel van de volledige status Hallo van Hallo-service. 

Hallo-replica's van elke partitie worden verdeeld over Hallo van clusterknooppunten te kunnen de status van de benoemde service[scale](service-fabric-concepts-scalability.md). Wanneer gegevens Hallo groeien behoeften, groeien partities en Service Fabric rebalances partities tussen knooppunten toomake efficiënt gebruik van de hardwarebronnen. Als u nieuwe knooppunten toohello cluster toevoegt, opnieuw Service Fabric Hallo partitie replica's verdelen over het aantal knooppunten Hallo verhoogd. De algemene verbetert de prestaties van toepassingen en conflicten over toegang toomemory verkleint. Als het Hallo-knooppunten in cluster Hallo niet efficiënt worden gebruikt, kunt u het aantal knooppunten in cluster Hallo Hallo verminderen. Service Fabric rebalances Hallo partitie replica's opnieuw over het aantal knooppunten toomake beter gebruik van hardware op elk knooppunt Hallo Hallo verlaagd.

Binnen een partitie hebben staatloze benoemde services de exemplaren stateful benoemde services replica's. Normaal gesproken staatloze benoemde services ooit slechts één partitie hebben omdat ze geen interne status hebben. Hallo partitie exemplaren bieden voor [beschikbaarheid](service-fabric-availability-services.md). Als één exemplaar is mislukt, andere exemplaren toooperate gewoon doorgaan en het Service Fabric maakt vervolgens een nieuw exemplaar. Stateful services met de naam behouden hun status binnen de replica's en elke partitie heeft een eigen replicaset. Lezen en schrijven bewerkingen worden uitgevoerd op één replica (Hallo primaire genoemd). Wijzigingen toostate van schrijven bewerkingen zijn gerepliceerd toomultiple andere replica's (actieve secundaire replica's genoemd). Moet een replica mislukken, Service Fabric-bouwt voort op een nieuwe replica van Hallo bestaande replica's.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Staatloze en stateful microservices voor Service Fabric
Service Fabric kunt u toobuild toepassingen die bestaan uit microservices of containers. Staatloze microservices (zoals protocol gateways en webproxy) gedurende niet een veranderlijke status buiten een aanvraag en de reactie van Hallo-service. Azure Cloud Services-werkrollen zijn een voorbeeld van een staatloze service. Stateful microservices (zoals gebruikersaccounts, databases, apparaten, on en wachtrijen) onderhouden de status van een veranderlijke, gezaghebbende buiten Hallo-aanvraag en het antwoord. De hedendaagse Internet-toepassingen bestaan uit een combinatie van staatloze en stateful microservices. 

Een sleutel differentation met Service Fabric wordt de nadruk op het ontwikkelen van stateful services, hetzij met Hallo [gebouwd voor het programmeren van modellen ](service-fabric-choose-framework.md) of met beperkte stateful services. Hallo [toepassingsscenario's](service-fabric-application-scenarios.md) beschrijven Hallo scenario's waar stateful services worden gebruikt.

Waarom er stateful microservices samen met staatloze die zijn? Hallo van de twee belangrijkste redenen zijn:

* U kunt met een hoge gegevensdoorvoer, lage latentie, fout fouttolerante online transaction processing (OLTP) services door code te houden en sluiten gegevens op dezelfde machine Hallo opbouwen. Voorbeelden zijn interactieve winkelobjecten, zoeken, Internet der dingen (IoT)-systemen, handelssystemen, creditcard verwerking en fraude detectie systemen en persoonlijke record management.
* Het ontwerp van toepassing, kunt u vereenvoudigen. Stateful microservices Verwijder Hallo behoefte aanvullende wachtrijen en caches die traditioneel tooaddress Hallo beschikbaarheid en latentie vereisten van een zuiver stateless toepassing vereist. Stateful services zijn natuurlijk hoge beschikbaarheid en lage latentie, waardoor Hallo aantal bewegende delen toomanage in uw toepassing als geheel.

## <a name="supported-programming-models"></a>Ondersteunde programmeermodellen
Service Fabric biedt meerdere manieren toowrite en beheren van uw services. Services kunnen Hallo Service Fabric-API's tootake volledig gebruikmaken van de functies en toepassingsframeworks Hallo-platform gebruiken. Services kunnen ook worden alle gecompileerde uitvoerbaar programma geschreven in elke taal en gehost op een Service Fabric-cluster. Zie voor meer informatie [programmeermodellen ondersteund](service-fabric-choose-framework.md).

### <a name="containers"></a>Containers
Standaard wordt Service Fabric implementeert en services als processen wordt geactiveerd. Service Fabric kunnen ook services implementeren in [containers](service-fabric-containers-overview.md). Belangrijker nog, kunt u services in processen en services in containers in Hallo elkaar dezelfde toepassing. Service Fabric ondersteunt de implementatie van Linux-containers Windows containers op Windows Server 2016. U kunt bestaande toepassingen, stateless services of stateful services in containers implementeren. 

### <a name="reliable-services"></a>Reliable Services
[Reliable Services](service-fabric-reliable-services-introduction.md) is een lichtgewicht framework voor het schrijven van services die integreren met Hallo Service Fabric-platform en profiteren van de volledige set Hallo van platformfuncties. Reliable Services kunnen worden staatloze (vergelijkbaar toomost service platformen, zoals webservers of werkrollen in Azure Cloud Services), waarbij de status is opgeslagen in een externe oplossing, zoals Azure DB of Azure Table Storage. Reliable Services kunnen ook stateful, worden waar status rechtstreeks in het Hallo-service zelf betrouwbare verzamelingen is opgeslagen. Staat worden gesteld [maximaal beschikbare](service-fabric-availability-services.md) door middel van replicatie en gedistribueerde via [partitioneren](service-fabric-concepts-partitioning.md), alle beheerde automatisch door de Service Fabric.

### <a name="reliable-actors"></a>Reliable Actors
Gebouwd op Reliable Services, Hallo [betrouwbare Actor](service-fabric-reliable-actors-introduction.md) framework is een toepassingsframework dat Hallo virtuele Actor patroon, op basis van Hallo actor ontwerppatroon implementeert. onafhankelijke eenheden van de berekenings- en status Hallo betrouwbare Actor-framework gebruikt met één thread uitvoering actoren aangeroepen. Hallo betrouwbare Actor framework biedt ingebouwde communicatie voor actoren en vooraf ingestelde status persistentie en scale-out-configuraties.

### <a name="aspnet-core"></a>ASP.NET Core
Service Fabric kan worden geïntegreerd met [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) als een eerste-klas programmeermodel voor het bouwen van websites en toepassingen van de API

### <a name="guest-executables"></a>Gast uitvoerbare bestanden
Een [Gast uitvoerbaar bestand](service-fabric-deploy-existing-app.md) is een bestaande, willekeurige uitvoerbaar bestand (geschreven in een andere taal) die worden gehost op een Service Fabric-cluster goed samen met andere services. Uitvoerbare bestanden Gast kan niet rechtstreeks te integreren met Service Fabric-API's. Maar ze nog steeds profiteren van functies Hallo platform biedt, zoals aangepaste gezondheid en laden reporting en zichtbaarheid service door het aanroepen van REST-API's. Ze hebben ook de volledige toepassing lifecycle ondersteuning. 

## <a name="application-lifecycle"></a>Toepassingslevenscyclus
Zoals met andere platforms wordt een toepassing op Service Fabric meestal doorloopt Hallo volgende fasen: ontwerpen, ontwikkelen, testen, implementatie, upgrade, onderhoud en verwijderen. Service Fabric biedt uitstekende ondersteuning voor de levenscyclus van de volledige toepassing hello van cloud-toepassingen van ontwikkeling tot implementatie, dagelijkse beheer en onderhoud tooeventual buiten gebruik stellen. Hallo-servicemodel kan verschillende tooparticipate voor verschillende rollen in de levenscyclus van de toepassing hello onafhankelijk. [De levenscyclus van de service Fabric-toepassing](service-fabric-application-lifecycle.md) biedt een overzicht van Hallo API's en hoe ze worden gebruikt door verschillende rollen in de gehele Hallo fasen van de levenscyclus van Hallo Service Fabric-toepassing hello. 

de volledige levenscyclus Hallo kan worden beheerd via [PowerShell-cmdlets](/powershell/module/ServiceFabric/), [C#-API's](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [Java-API's](/java/api/system.fabric._application_management_client), en [REST-API's](/rest/api/servicefabric/). U kunt ook continue integratie/continue implementatie pijplijnen met hulpprogramma's zoals instellen [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) of [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Hallo volgende Microsoft Virtual Academy video wordt beschreven hoe toomanage de levenscyclus van uw toepassing:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Testtoepassingen en -services
toocreate echt cloud scale-services is kritieke tooverify uw toepassingen en services echte fouten kunnen tolereren. Hallo-fout Analysis Services is ontworpen voor het testen van de services die zijn gebouwd op Service Fabric. Hello [fout Analysis Service](service-fabric-testability-overview.md), kunt u zinvolle fouten veroorzaken en volledige Testscenario's uitvoeren op uw toepassingen. Deze fouten en scenario's uitoefenen en valideren Hallo talrijke statussen en overgangen die een service in een gecontroleerde, veilige en consistente manier tijdens de levensduur krijgen.

[Acties](service-fabric-testability-actions.md) doel van een service voor het testen met behulp van de afzonderlijke fouten. Een ontwikkelaar van de service kunt deze als bouwstenen toowrite ingewikkeld scenario's gebruiken. Voorbeelden van gesimuleerde fouten zijn:

* Start opnieuw op een knooppunt toosimulate een willekeurig aantal situaties waarbij een computer of virtuele machine opnieuw is opgestart.
* Verplaatsen van een replica van de stateful service toosimulate load balancing, failover of upgrade van de toepassing.
* Quorumverlies op een stateful service toocreate een situatie waarin schrijfbewerkingen kunnen niet doorgaan omdat er niet voldoende 'back-up' of 'secundair' replica's tooaccept nieuwe gegevens worden aangeroepen.
* Verlies van gegevens op een stateful service toocreate een situatie waarin alle geheugenstatus volledig wordt gewist uit worden aangeroepen.

[Scenario's](service-fabric-testability-scenarios.md) complexe bewerkingen bestaan uit een of meer acties. Hallo-fout Analysis Service biedt twee ingebouwde voltooien van scenario's:

* [Chaos scenario](service-fabric-controlled-chaos.md)-continue, interleaved fouten (correcte en geforceerde afsluiting) in de cluster Hallo simuleert gedurende langere perioden.
* [Failover-scenario](service-fabric-testability-scenarios.md#failover-test)-een versie van Hallo chaos Testscenario die gericht is op een specifieke service partitie terwijl andere services niet is beïnvloed.

## <a name="clusters"></a>Clusters
Een [Service Fabric-cluster](service-fabric-deploy-anywhere.md) is een met het netwerk verbonden reeks virtuele of fysieke machines waarop uw microservices worden geïmplementeerd en beheerd. Clusters kunnen schalen toothousands machines. Een machine of virtuele machine die deel uitmaakt van een cluster wordt een clusterknooppunt genoemd. Elk knooppunt wordt de knooppuntnaam van een (een tekenreeks) toegewezen. Knooppunten hebben kenmerken zoals plaatsingseigenschappen. Elke computer of virtuele machine heeft een service automatisch starten, `FabricHost.exe`, die begint bij het opstarten worden uitgevoerd en start vervolgens twee uitvoerbare bestanden: Fabric.exe en FabricGateway.exe. Deze twee uitvoerbare bestanden vormen Hallo-knooppunt. Voor het testen van scenario's, kunt u meerdere knooppunten op een enkele computer of virtuele machine host door het uitvoeren van meerdere exemplaren van `Fabric.exe` en `FabricGateway.exe`.

Service Fabric-clusters kunnen worden gemaakt op virtuele of fysieke machines met Windows Server- of Linux. U kunt toodeploy en Service Fabric-toepassingen uitvoeren in een omgeving waarin u een set van Windows Server of Linux-computers die onderling verbonden hebben: on-premises op Microsoft Azure of op elke cloudprovider.

Hallo beschrijving volgende Microsoft Virtual Academy video van Service Fabric-clusters:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Clusters op Azure
Service Fabric-clusters biedt op Azure integratie met andere Azure-functies en services, waardoor bewerkingen en het beheer van Hallo cluster eenvoudiger en betrouwbaarder. Een cluster is een Azure Resource Manager-bron, waarmee u model kunt clusters zoals elke andere resources in Azure. Resource Manager biedt ook eenvoudig beheer van alle resources die worden gebruikt door Hallo cluster als één eenheid. Clusters op Azure zijn geïntegreerd met Azure diagnoses en Log Analytics. Knooppunttypen cluster zijn [virtuele-machineschaalsets](/azure/virtual-machine-scale-sets/index), zodat de functionaliteit voor automatisch schalen is ingebouwd in.

U kunt een cluster maken op Azure via Hallo [Azure-portal](service-fabric-cluster-creation-via-portal.md), van een [sjabloon](service-fabric-cluster-creation-via-arm.md), of van [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

Hallo-evaluatieversie van Service Fabric op Linux kunt u toobuild, implementeren en beheren van maximaal beschikbare, sterk schaalbare toepassingen op Linux, net zoals u zou in Windows doen. Hallo Service Fabric frameworks (Reliable Services en Reliable Actors) zijn beschikbaar in Java op Linux, in aanvulling tooC # (.NET Core). U kunt ook samenstellen [uitvoerbare gastservices](service-fabric-deploy-existing-app.md) met elke taal of elk framework. Bovendien ondersteunt Hallo preview Docker-containers organiseren. Docker-containers kunnen worden uitgevoerd Gast uitvoerbare bestanden of systeemeigen Service Fabric-services, die Service Fabric-frameworks hello gebruiken. Lees voor meer informatie [Service Fabric op Linux](service-fabric-linux-overview.md).

Omdat Service Fabric in Linux een preview-versie is, zijn er enkele functies die wel worden ondersteund in Windows, maar niet in Linux. toolearn meer lezen [verschillen tussen Service Fabric op Linux en Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Zelfstandige clusters
Service Fabric bevat een installatiepakket voor u toocreate zelfstandige Service Fabric-clusters on-premises of op elke cloudprovider. Zelfstandige clusters geven u Hallo vrijheid toohost een cluster elke gewenste locatie. Als uw gegevens onderwerp toocompliance of voorschriften is; of u uw lokale gegevens tookeep wilt, kunt u uw eigen cluster en de toepassingen hosten. Service Fabric-toepassingen kunnen worden uitgevoerd in omgevingen met meerdere hosting zonder wijzigingen, zodat uw kennis van het bouwen van toepassingen van één hosting omgeving tooanother weerspiegelt. 

[Uw eerste Service Fabric zelfstandige cluster maken](service-fabric-get-started-standalone-cluster.md)

Linux-clusters voor zelfstandige zijn nog niet ondersteund.

### <a name="cluster-security"></a>Clusterbeveiliging
Clusters moet beveiligde tooprevent niet-geautoriseerde gebruikers verbinding maken met cluster tooyour, vooral wanneer er productieworkloads uitgevoerd. Hoewel het mogelijk toocreate een niet-beveiligde cluster, Hierdoor kunnen de anonieme gebruikers tooconnect tooit als eindpunten voor beheer zijn blootgesteld toohello openbare internet. Het is niet mogelijk toolater inschakelen beveiliging op een niet-beveiligde cluster: clusterbeveiliging van het is ingeschakeld tijdens het maken van een cluster.

Hallo cluster security scenario's:
* Knooppunt naar beveiliging
* Beveiliging van de client-naar-knooppunt
* Op rollen gebaseerde toegangsbeheer (RBAC)

Lees voor meer informatie [beveiligen van een cluster](service-fabric-cluster-security.md).

### <a name="scaling"></a>Schalen
Als u nieuwe knooppunten toohello cluster toevoegt, rebalances Service Fabric Hallo partitie replica's en -exemplaren over het aantal knooppunten Hallo verhoogd. De algemene verbetert de prestaties van toepassingen en conflicten over toegang toomemory verkleint. Als het Hallo-knooppunten in cluster Hallo niet efficiënt worden gebruikt, kunt u het aantal knooppunten in cluster Hallo Hallo verminderen. Service Fabric rebalances opnieuw Hallo partitie replica's en exemplaren over Hallo afgenomen aantal knooppunten toomake beter gebruik van Hallo hardware op elk knooppunt. U kunt ofwel clusters op Azure schalen [handmatig](service-fabric-cluster-scale-up-down.md) of [programmatisch](service-fabric-cluster-programmatic-scaling.md). Zelfstandige clusters kunnen worden geschaald [handmatig](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Cluster-upgrades
Periodiek worden nieuwe versies van de Service Fabric-runtime Hallo gepubliceerd. Runtime of fabric, upgrades uitvoeren op uw cluster zodat u altijd uitvoert een [ondersteunde versie](service-fabric-support.md). Bovendien toofabric upgrades, u kunt ook de configuratie van het cluster zoals certificaten of poorten van de toepassing bijwerken.

Een Service Fabric-cluster is een resource die u bezit, maar gedeeltelijk wordt beheerd door Microsoft. Microsoft is verantwoordelijk voor de toepassing van patches Hallo onderliggende besturingssysteem en het uitvoeren van fabric-upgrades op uw cluster. U kunt uw cluster tooreceive automatische fabric ingesteld upgrades, wanneer Microsoft een nieuwe versie is vrijgegeven of kies tooselect een ondersteunde fabric-versie die u wilt. Fabric- en configuratie-upgrades kunnen worden ingesteld via hello Azure-portal of via Resource Manager. Lees voor meer informatie [upgraden van een Service Fabric-cluster](service-fabric-cluster-upgrade.md). 

Een zelfstandige cluster is een resource die u hebt volledig zelf. U bent zelf verantwoordelijk voor de toepassing van patches Hallo onderliggende besturingssysteem en het starten van de fabric-upgrades. Als uw cluster te verbinding kunt maken[https://www.microsoft.com/download](https://www.microsoft.com/download), kunt u uw cluster tooautomatically download instellen en inrichten van nieuwe Service Fabric Hallo runtime-pakket. U zou vervolgens Hallo upgrade initiëren. Als uw cluster heeft geen toegang tot [https://www.microsoft.com/download](https://www.microsoft.com/download), kunt u handmatig Hallo nieuwe runtime-pakket te downloaden van een internet verbonden machine en vervolgens Hallo-upgrade initiëren. Lees voor meer informatie [upgraden van een zelfstandige Service Fabric-cluster](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Statuscontrole
Service Fabric introduceert een [statusmodel](service-fabric-health-introduction.md) ontworpen tooflag slecht cluster en de voorwaarden van toepassing op specifieke entiteiten (zoals clusterknooppunten en service-replica's). Hallo-statusmodel maakt gebruik van health-rapporteurs (onderdelen van het systeem en watchdogs). Hallo-doel is snel en gemakkelijk diagnose en herstel. Schrijvers van de service moeten toothink tevoren over status en hoe te[ontwerpen health reporting](service-fabric-report-health.md#design-health-reporting). Een voorwaarde die van invloed kan status moet worden gerapporteerd, vooral als vlag problemen sluiten toohello root kunt u. Hallo statusgegevens kunt tijd en moeite besparen op foutopsporing en onderzoek zodra het Hallo-service is en die wordt uitgevoerd op de gewenste schaal in productie.

Hallo Service Fabric-rapporteurs monitor geïdentificeerd voorwaarden van belang. Ze een rapport over deze voorwaarden op basis van hun lokale weergave. Hallo [health store](service-fabric-health-introduction.md#health-store) aggregeert statusgegevens verzonden door alle rapporteurs toodetermine of entiteiten globaal in orde zijn. Hallo-model is beoogde toobe uitgebreide, flexibele en eenvoudige toouse. Hallo kwaliteit van statusrapporten Hallo bepaalt Hallo nauwkeurig Hallo health weergave van Hallo-cluster. Fout-positieven waarin ten onrechte slecht problemen weergegeven kunnen nadelig upgrades of andere services die gebruikmaken van statusgegevens. Voorbeelden van dergelijke services zijn reparatie en waarschuwen mechanismen. Voorzichtig is daarom benodigde tooprovide rapporten die voorwaarden van interesse in Hallo vastleggen best mogelijke manier.

Rapportage kan worden gedaan via:
* Hallo bewaakte Service Fabric-service replica of het exemplaar.
* Interne watchdogs geïmplementeerd als een Service Fabric-service (bijvoorbeeld een Service Fabric staatloze service dat wordt bewaakt voorwaarden en rapporten). Hallo watchdogs kunnen worden geïmplementeerd op alle knooppunten of stelt toohello bewaakte service kunnen zijn.
* Interne watchdogs die worden uitgevoerd op Hallo Service Fabric-knooppunten, maar niet als Service Fabric-services worden geïmplementeerd.
* Externe watchdogs die test Hallo-bron van de buitenste Hallo Service Fabric-cluster (bijvoorbeeld bewaking service zoals Gomez).

Out of box hello, een Service Fabric-onderdelen health rapport over alle entiteiten in Hallo-cluster. [Systeemstatusrapporten](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) bieden inzicht in het cluster en de toepassing functionaliteit en vlag problemen via health. Voor toepassingen en services controleren systeemstatusrapporten of entiteiten worden geïmplementeerd en correct vanuit het perspectief van de Service Fabric-runtime Hallo Hallo van zich gedragen. Hallo-rapporten geen bieden een statuscontrole van de bedrijfslogica Hallo van Hallo service of vastgelopen processen te detecteren. tooadd informatie specifieke tooyour statusservice van logica [implementeren aangepaste health reporting](service-fabric-report-health.md) in uw services.

Service Fabric bevat verschillende manieren te[statusrapporten weergeven](service-fabric-view-entities-aggregated-health.md) geaggregeerd in Hallo health store:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) of andere visualisatie hulpprogramma's.
* Statusquery's (via [PowerShell](/powershell/module/ServiceFabric/), Hallo [C# FabricClient APIs](/api/system.fabric.fabricclient.healthclient) en [Java FabricClient APIs](/java/api/system.fabric._health_client), of [REST-API's](/rest/api/servicefabric)).
* Algemene query's die resulteren in een lijst van de entiteiten die zijn status als een van de eigenschappen hello (via PowerShell, Hallo API of REST).

Hallo die volgende Microsoft Virtual Academy video beschrijft Hallo Service Fabric-statusmodel en hoe deze wordt gebruikt:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe toocreate een [cluster in Azure](service-fabric-cluster-creation-via-portal.md) of een [zelfstandige cluster op Windows](service-fabric-cluster-creation-for-windows-server.md).
* Proberen te maken van een service met Hallo [Reliable Services](service-fabric-reliable-services-quick-start.md) of [Reliable Actors](service-fabric-reliable-actors-get-started.md) programming modellen.
* Meer informatie over hoe te[migreren van Cloudservices](service-fabric-cloud-services-migration-differences.md).
* Meer informatie over te[controle en diagnose van services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Meer informatie over te[testen van uw apps en services](service-fabric-testability-overview.md).
* Meer informatie over te[beheren en te organiseren clusterbronnen](service-fabric-cluster-resource-manager-introduction.md).
* Bekijkt hello [Service Fabric-voorbeelden](http://aka.ms/servicefabricsamples).
* Meer informatie over [Service Fabric-ondersteuningsopties](service-fabric-support.md).
* Lees Hallo [teamblog](https://blogs.msdn.microsoft.com/azureservicefabric/) voor artikelen en aankondigingen.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
