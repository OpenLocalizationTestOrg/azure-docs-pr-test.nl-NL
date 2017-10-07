---
title: aaaOverview van Service Fabric in Azure | Microsoft Docs
description: Een overzicht van Service Fabric, waar de toepassingen zijn samengesteld uit veel microservices tooprovide schaal en herstelmogelijkheden. Service Fabric is een platform voor gedistribueerde systemen gebruikt toobuild schaalbare, betrouwbare en toepassingen voor Hallo cloud eenvoudig worden beheerd.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Overzicht van Azure Service Fabric
Azure Service Fabric is een platform voor gedistribueerde systemen waarmee u eenvoudig toopackage kunt, implementeren en beheren van schaalbare en betrouwbare microservices en containers. Service Fabric ook een oplossing voor grote uitdagingen Hallo ontwikkelen en beheren van systeemeigen cloudtoepassingen. Ontwikkelaars en beheerders kunnen complexe infrastructuurproblemen voorkomen en zich concentreren op het implementeren van bedrijfsspecifieke, veeleisende werkbelastingen die schaalbaar, betrouwbaar en beheerbaar zijn. Service Fabric vertegenwoordigt Hallo next generation platform voor het maken en beheren van deze bedrijfsniveau, laag 1, cloud-toepassingen uitvoeren in containers.

In deze korte video introduceert Service Fabric en microservices:<center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Toepassingen bestaan uit microservices 
Service Fabric kunt u toobuild en schaalbare en betrouwbare toepassingen bestaan uit microservices dat tooas een cluster dat wordt aangeduid als u een high-density uitvoeren op een gedeelde groep machines, beheren. Het biedt een geavanceerde, lichtgewicht runtime toobuild gedistribueerd, schaalbaar, staatloze en stateful microservices uitgevoerd in de containers. Het bevat ook uitgebreide toepassing management mogelijkheden tooprovision, implementeren, bewaken, upgrade/patch en geïmplementeerde toepassingen, met inbegrip van beperkte services te verwijderen.

Service Fabric drijft veel Microsoft-services vandaag, waaronder Azure SQL Database, Azure Cosmos DB, Cortana Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Azure IoT Hub, Dynamics 365, Skype voor bedrijven en veel core Azure-services.

Service Fabric is op maat gemaakte toocreate systeemeigen cloudservices die kunnen begin klein, indien nodig en toomassive schaal met honderden of duizenden computers groeien.

De hedendaagse Internet scale services zijn opgebouwd uit microservices. Voorbeelden van microservices zijn protocol gateways, gebruikersprofielen, winkelen winkelwagentjes, inventaris verwerking, wachtrijen, en in de cache opslaat. Service Fabric is een microservices-platform die elke microservice (of de container) biedt een unieke naam op die stateless of stateful worden kan.

Service Fabric bevat uitgebreide runtime en lifecycle management mogelijkheden tooapplications die van deze microservices bestaan. Deze als host fungeert voor microservices in containers die zijn geïmplementeerd en geactiveerd via Hallo Service Fabric-cluster. Een verplaatsing van virtuele machines toocontainers maakt mogelijk een orde van grootte toename in dichtheid. Op deze manier wordt een andere orde van grootte in dichtheid mogelijk wanneer u van containers toomicroservices in deze containers verplaatst. Één cluster voor Azure SQL Database omvat bijvoorbeeld honderden computers met tienduizenden containers die als host fungeren voor een totaal van honderden of duizenden databases. Elke database is een stateful Service Fabric-microservice. 

Lees voor meer informatie over Hallo microservices benadering [waarom een microservices benadering toobuilding toepassingen?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Implementatie van de container en orchestration
Service Fabric is van Microsoft [container orchestrator](service-fabric-cluster-resource-manager-introduction.md) microservices implementeert in een cluster van machines. Microservices kunnen worden ontwikkeld in tal van manieren met behulp van Hallo [Service Fabric modellen programming](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [code van uw keuze](service-fabric-deploy-existing-app.md). Belangrijker nog, kunt u beide services in processen en -services in containers in Hallo elkaar dezelfde toepassing. Als u alleen te wilt[implementeren en beheren van containers](service-fabric-containers-overview.md), Service Fabric is een ideale keuze als een container orchestrator.

## <a name="any-os-any-cloud"></a>Een besturingssysteem in een cloud
Service Fabric kan overal worden uitgevoerd. In veel omgevingen, waaronder Azure of on-premises, op Windows Server of op Linux, kunt u clusters voor Service Fabric. U kunt zelfs clusters maken op andere openbare clouds. Hallo-ontwikkelomgeving in Hallo SDK is bovendien **identieke** toohello productie-omgeving met geen emulators die betrokken zijn. Met andere woorden, implementeert wat wordt uitgevoerd op uw lokaal ontwikkelcluster toohello clusters in andere omgevingen.

![Service Fabric-platform][Image1]

Lees voor meer informatie over het maken van clusters met lokale [maken van een cluster op Windows Server- of Linux](service-fabric-deploy-anywhere.md) of voor Azure maken van een cluster [via hello Azure-portal](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Staatloze en stateful microservices voor Service Fabric
Service Fabric kunt u toobuild toepassingen die bestaan uit microservices of containers. Staatloze microservices (zoals protocol gateways en webproxy) gedurende niet een veranderlijke status buiten een aanvraag en de reactie van Hallo-service. Azure Cloud Services-werkrollen zijn een voorbeeld van een staatloze service. Stateful microservices (zoals gebruikersaccounts, databases, apparaten, on en wachtrijen) onderhouden de status van een veranderlijke, gezaghebbende buiten Hallo-aanvraag en het antwoord. De hedendaagse Internet-toepassingen bestaan uit een combinatie van staatloze en stateful microservices. 

Een sleutel differentation met Service Fabric wordt de nadruk op het ontwikkelen van stateful services, hetzij met Hallo [ingebouwde programmeermodellen ](service-fabric-choose-framework.md) of met beperkte stateful services. Hallo [toepassingsscenario's](service-fabric-application-scenarios.md) beschrijven Hallo scenario's waar stateful services worden gebruikt.


## <a name="application-lifecycle-management"></a>De levenscyclus van Toepassingsbeheer
Service Fabric biedt ondersteuning voor de levenscyclus van de volledige toepassing hello en CI/CD van cloudtoepassingen, met inbegrip van containers. Deze levenscyclus beheren bevat ontwikkeling tot implementatie, dagelijkse beheer en onderhoud tooeventual buiten gebruik stellen.

Beheermogelijkheden voor service Fabric-toepassing lifecycle toepassingsbeheerders en IT-operators toouse eenvoudige, lage-touch werkstromen tooprovision inschakelen, implementeren, patch en controleren van toepassingen. Deze ingebouwde werkstromen minder aanzienlijk Hallo last van de IT-operators tookeep toepassingen die continu beschikbaar zijn.

De meeste toepassingen bestaan uit een combinatie van staatloze en stateful microservices containers en andere uitvoerbare bestanden die samen zijn geïmplementeerd. Doordat de sterke-typen op Hallo toepassingen, kunnen Service Fabric Hallo-implementatie van meerdere exemplaren van een toepassing. Elk exemplaar wordt beheerd en onafhankelijk bijgewerkt. Houd voor ogen dat Service Fabric implementeren containers of alle uitvoerbare bestanden en zodat ze betrouwbaar. Service Fabric kan bijvoorbeeld .NET, ASP.NET Core, node.js, Windows containers, Linux-containers, Java virtuele machines, scripts, Angular of elke willekeurige waarmee u uw toepassing implementeren.

Service Fabric is geïntegreerd met CI/CD-hulpprogramma's zoals [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html), en [Octopus implementeren](https://octopus.com/) en kan worden gebruikt met een ander populaire CI/CD-hulpprogramma.

Lees voor meer informatie over de levenscyclus van Toepassingsbeheer [toepassing lifecycle](service-fabric-application-lifecycle.md). Voor meer informatie over hoe toodeploy code, Zie [implementeren van een gast uitvoerbaar bestand](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Belangrijkste mogelijkheden
U kunt met behulp van Service Fabric:

* Implementeer tooAzure of tooon-premises datacenters waarop Windows of Linux wordt uitgevoerd met nul codewijzigingen. Eenmalig schrijven en vervolgens implementeren overal tooany Service Fabric-cluster.
* Schaalbare toepassingen ontwikkelen die bestaan uit een van de microservices via Hallo Service Fabric-programmeermodellen, containers of code.
* Maximaal betrouwbare microservices voor staatloze en stateful ontwikkelen. Hallo-ontwerp van uw toepassing met behulp van stateful microservices vereenvoudigen. 
* Gebruik Hallo nieuwe Reliable Actors programming model toocreate cloudobjecten met zelfstandige code en status.
* Implementeren en te organiseren containers die containers voor Windows en Linux-containers zijn. Service Fabric is een container op de hoogte, stateful is, gegevens orchestrator.
* Toepassingen implementeren in seconden, op high-density met honderden of duizenden toepassingen of containers per computer.
* Verschillende versies van Hallo dezelfde toepassing zijde elkaar en elke toepassing onafhankelijk werk implementeren.
* Hallo levenscyclus van uw toepassingen zonder uitvaltijd, met inbegrip van breken en vaste upgrades beheren.
* Uitbreiden of schalen in Hallo aantal knooppunten in een cluster. Als u knooppunten schalen, is uw toepassingen automatisch schalen.
* Bewaken en onderzoeken Hallo status van uw toepassingen en beleidsregels voor het uitvoeren van automatische reparaties instellen.
* Bekijkt hello resource balancer indelen Hallo herdistributie van toepassingen over Hallo-cluster. Service Fabric vanuit fouten herstelt en optimaliseert de Hallo-verdeling van de belasting op basis van beschikbare resources.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
* Voor meer informatie:
  * [Waarom een microservices benadering toobuilding toepassingen?](service-fabric-overview-microservices.md)
  * [Overzicht van de terminologie](service-fabric-technical-overview.md)
* Instellen van uw Service Fabric [ontwikkelomgeving](service-fabric-get-started.md)  
* Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
