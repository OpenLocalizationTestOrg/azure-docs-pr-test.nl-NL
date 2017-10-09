---
title: aaaDifferences tussen Cloud Services en de Service Fabric | Microsoft Docs
description: Conceptueel overzicht voor het migreren van toepassingen van Cloudservices tooService Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>Meer informatie over Hallo verschillen tussen Cloudservices en Service Fabric voordat het migreren van toepassingen.
Microsoft Azure Service Fabric is Hallo next generation toepassing cloudplatform voor een zeer schaalbaar, maximaal betrouwbare gedistribueerde toepassingen. Het geeft veel nieuwe functies voor verpakking, implementeren, bijwerken en beheren van gedistribueerde cloud-toepassingen. 

Dit is een inleidende handleiding toomigrating-toepassingen van Cloudservices tooService Fabric. Het richt zich voornamelijk op architectuur en verschillen tussen Cloudservices en Service Fabric ontwerpen.

## <a name="applications-and-infrastructure"></a>Toepassingen en infrastructuur
Een fundamentele verschil tussen Cloudservices en Service Fabric is Hallo relatie tussen virtuele machines, workloads en toepassingen. Hier een werkbelasting wordt gedefinieerd als Hallo code u schrijft tooperform een bepaalde taak of een service leveren.

* **Er is een cloud-Services over het implementeren van toepassingen als virtuele machines.** Hallo-code die u schrijft is nauw gekoppeld tooa VM-instantie, zoals een webservice of de Werkrol. toodeploy een workload in de Cloud-Services is toodeploy een of meer VM-exemplaren uitvoeren Hallo werkbelasting. Er is geen scheiding van toepassingen en virtuele machines en dus er is geen formele definitie van een toepassing. Een toepassing worden beschouwd als een reeks Web- of Werkrol-exemplaren in een Cloud Services-implementatie of als een volledige Cloud Services-implementatie. In dit voorbeeld wordt een toepassing worden weergegeven als een reeks rolinstanties.

![Cloud Services-toepassingen en -topologie][1]

* **Er is een service Fabric over implementatie toepassingen tooexisting virtuele machines of machines Service Fabric op Windows of Linux.** Hallo-services die u schrijft zijn volledig ontkoppelde van Hallo onderliggende infrastructuur, die beschouwing weg door Hallo Service Fabric-toepassingsplatform, zodat een toepassing geïmplementeerd toomultiple omgevingen worden kan. Een workload in Service Fabric is een 'service' genoemd en een of meer services zijn gegroepeerd in een formeel gedefinieerde toepassing die wordt uitgevoerd op Hallo Service Fabric-toepassing-platform. Meerdere toepassingen kunnen worden geïmplementeerd tooa één Service Fabric-cluster.

![Service Fabric-toepassingen en -topologie][2]

Service Fabric zelf is een platform toepassingslaag die wordt uitgevoerd op Windows of Linux, terwijl Cloud Services een systeem is voor het implementeren van beheerde Azure VM's met de werkbelastingen die zijn gekoppeld.
Hallo Service Fabric-toepassingsmodel heeft een aantal voordelen:

* Snelle implementatietijden. VM-instanties maken kan enige tijd duren. In Service Fabric worden virtuele machines alleen geïmplementeerd als een cluster die als host fungeert voor tooform Hallo Service Fabric-toepassingsplatform. Vanaf dat moment op toepassingspakketten zeer snel geïmplementeerde toohello cluster worden.
* High-density hosten. In de Cloud-Services, een werknemer rol virtuele machine fungeert als host een werkbelasting. Toepassingen zijn in Service Fabric gescheiden van Hallo virtuele machines die worden uitgevoerd, wat betekent dat u een groot aantal toepassingen tooa klein aantal virtuele machines, die de totale kosten voor grotere implementaties kunt verlagen kunt implementeren.
* Hallo Service Fabric-platform van een willekeurige plaats die uitvoeren kunt is Windows Server of Linux-machines of Azure of on-premises. Hallo-platform biedt een abstractielaag over Hallo onderliggende infrastructuur, zodat uw toepassing op verschillende omgevingen uitvoeren kunt. 
* Beheer van gedistribueerde toepassingen. Service Fabric is een platform dat niet alleen hosts toepassingen gedistribueerde, maar ook helpt bij het beheren van hun levensduur onafhankelijk van Hallo die als host fungeert voor VM of de levenscyclus van de computer.

## <a name="application-architecture"></a>Toepassingsarchitectuur
Hallo architectuur van een Cloud Services-toepassing omvat gewoonlijk talrijke externe service-afhankelijkheden, zoals Service Bus, Azure Table en Blob Storage, SQL, Redis en anderen toomanage Hallo status en gegevens van een toepassing en de communicatie tussen Web en werkrollen in een Cloud Services-implementatie. Een voorbeeld van een volledige Cloud Services-toepassing uitzien als volgt:  

![Cloud Services-architectuur][9]

Service Fabric-toepassingen kunt toouse Hallo dezelfde externe services in een volledige toepassing. Hallo eenvoudigste migratiepad van Cloudservices tooService Fabric is het volgende voorbeeld Cloud Services-architectuur tooreplace Hallo Cloud Services-implementatie met een Service Fabric-toepassing hello houden algehele architectuur Hallo dezelfde. Hello Web- en werkrollen mag overbrengen tooService Fabric stateless services met minimale codewijzigingen.

![Service Fabric-architectuur na de migratie van eenvoudige][10]

In deze fase Hallo systeem moet blijven toowork Hallo hetzelfde als voorheen. Voordeel te halen van de Service-Fabric stateful functies, externe status winkels kan worden internalized als stateful services indien van toepassing. Dit is meer betrokken dan een eenvoudige migratie van Web- en werkrollen tooService Fabric stateless services, zoals vereist voor het schrijven van aangepaste services die bieden dezelfde functionaliteit tooyour toepassing hello externe services voorheen. Hallo voordelen hiervan zijn: 

* Externe afhankelijkheden verwijderen 
* Hallo-implementatie, beheer en de upgrade modellen samen te voegen. 

Een voorbeeld van de resulterende architectuur van deze services internalizing kan er als volgt uitzien:

![Service Fabric-architectuur na volledige migratie][11]

## <a name="communication-and-workflow"></a>Werkstroom en communicatie
De meeste Service in de Cloud-toepassingen bestaan uit meer dan één laag. Op deze manier wordt een Service Fabric-toepassing bestaat uit meer dan één service (meestal veel services). Twee algemene communicatie-modellen zijn rechtstreekse communicatie en via een externe duurzame opslag.

### <a name="direct-communication"></a>Rechtstreekse communicatie
Met directe communicatie communiceren lagen rechtstreeks via eindpunt die worden weergegeven door elke laag. In staatloze omgevingen zoals Cloud Services, dit betekent dat een exemplaar van een VM-rol, ofwel willekeurig selecteren of round robin toobalance laden en rechtstreeks verbinden tooits-eindpunt.

![Cloud Services rechtstreekse communicatie][5]

 Rechtstreekse communicatie is een algemene communicatiemodel in Service Fabric. Hallo belangrijkste verschil tussen Service Fabric en Cloud-Services is dat in de Cloud Services u verbinding tooa VM maakt, terwijl in Service Fabric u tooa service verbinding maken. Dit is een belangrijk verschil voor een aantal oorzaken hebben:

* Services in Service Fabric is niet gebonden toohello virtuele machines die als host fungeren. Services Hallo cluster kunnen verplaatsen en in feite verwachte toomove rond zijn voor verschillende oorzaken hebben: Resource balancing, failover, toepassingen en infrastructuur upgrades en plaatsing of load-beperkingen. Dit betekent dat het dat adres van een service-exemplaar op elk gewenst moment kunt wijzigen. 
* Een virtuele machine in Service Fabric kan meerdere services, elk met unieke eindpunten hosten.

Service Fabric biedt een service discovery mechanisme, Hallo Naming Service, die gebruikte tooresolve endpoint-adressen van services kan worden aangeroepen. 

![Service Fabric rechtstreekse communicatie][6]

### <a name="queues"></a>Wachtrijen
Een algemene mechanisme voor communicatie tussen lagen in staatloze omgevingen zoals Cloud Services is een externe opslag wachtrij toodurably toouse Werktaken van één laag tooanother opslaan. Een veelvoorkomend scenario is een weblaag die taken tooan Azure Queue verzendt of de Service Bus waarbij Werkrol exemplaren in wachtrij kunnen worden en verwerkt Hallo taken.

![Cloud Services wachtrij communicatie][7]

Hallo hetzelfde communicatiemodel kan worden gebruikt in Service Fabric. Dit kan nuttig zijn bij het migreren van een bestaande toepassing Cloud Services-tooService Fabric. 

![Service Fabric rechtstreekse communicatie][8]

## <a name="next-steps"></a>Volgende stappen
Hallo eenvoudigste migratiepad van Cloud Services-tooService Fabric is tooreplace alleen hello Cloud Services-implementatie met een Service Fabric-toepassing te houden Hallo algehele architectuur van uw toepassing ongeveer Hallo dezelfde. Hallo volgende artikel biedt een handleiding toohelp converteren een Web- of Werkrol tooa staatloze Service Fabric-service.

* [Eenvoudige migratie: converteren van een Web- of Werkrol tooa staatloze Service Fabric-service](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
