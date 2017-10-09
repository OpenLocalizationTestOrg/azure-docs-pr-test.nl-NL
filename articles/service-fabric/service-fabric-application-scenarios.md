---
title: aaaApplication scenario's en ontwerpen | Microsoft Docs
description: "Overzicht van categorieën van cloud-toepassingen in Service Fabric. Ontwerp van de toepassing die gebruikmaakt van services voor stateful en staatloze besproken."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Service Fabric toepassingsscenario 's
Azure Service Fabric biedt een betrouwbare en flexibele platform waarmee u toowrite en tal van zakelijke toepassingen en services worden uitgevoerd. Deze toepassingen en microservices kan stateless of stateful, en ze resource verdeeld zijn over virtuele machines toomaximize efficiëntie. Hallo unieke architectuur van Service Fabric kunt u tooperform bijna realtime gegevensanalyse, in het geheugen berekening, parallelle transacties en gebeurtenisverwerking in uw toepassingen. U kunt eenvoudig uw toepassingen omhoog of omlaag schalen (echt inkomend of uitgaand), afhankelijk van uw veranderende resourcevereisten.

Hallo Service Fabric-platform in Azure is ideaal voor Hallo categorieën van toepassingen te volgen:

* **Maximaal beschikbare services**: Service Fabric-services bieden snelle failover met meerdere service secundaire replica's maken. Als een knooppunt, een proces of een afzonderlijke service uitgeschakeld vanwege toohardware of een andere storing wordt, is een secundaire replica's Hallo gepromoveerde tooa primaire replica met minimale verlies van service.
* **Schaalbare services**: afzonderlijke services kunnen worden gepartitioneerd, waardoor het status toobe uitgebreid over Hallo-cluster. Bovendien kunnen afzonderlijke services worden gemaakt en verwijderd op Hallo snel. Services kunnen snel en eenvoudig uitgebreid van enkele exemplaren op een paar knooppunten toothousands van exemplaren op veel knooppunten en vervolgens geschaald in, afhankelijk van uw resourcebehoeften. U kunt Service Fabric toobuild gebruik van deze services en hun volledige levenscyclus beheren.
* **Berekening van niet-statische gegevens**: Service Fabric kunt u gegevens toobuild, invoer/uitvoer en compute geheugenintensieve stateful toepassingen. Service Fabric kunnen Hallo onderbrengen van de verwerking van (berekening) en gegevens in toepassingen. Normaal gesproken wanneer uw toepassing toegang toodata vereist, is dit netwerklatentie die zijn gekoppeld aan een externe gegevensbron cache of storage-laag. Met stateful Service Fabric-services, is dat latentie geëlimineerd, waardoor meer zodat leest en schrijft. Stel bijvoorbeeld dat er een toepassing die wordt uitgevoerd in de buurt van realtime aanbeveling selecties voor klanten met een vereiste round trip-tijd van minder dan 100 milliseconden. Hallo-latentie en prestatiekenmerken van Service Fabric-services (waarbij Hallo berekening van de aanbeveling selectie worden samengevoegd met Hallo gegevens en regels) biedt een responsief ervaring toohello gebruiker vergeleken met de Hallo standaardimplementatie model van toofetch Hallo nodig gegevens uit de externe opslag.  
* **Interactieve toepassingen op basis van sessies**: Service Fabric is handig als uw toepassingen, zoals online gaming of chatberichten, lage latentie lees- en schrijfbewerkingen zijn vereist. Service Fabric kunt u toobuild deze interactieve, stateful toepassingen zonder toocreate een afzonderlijk archief of een cache, zoals is vereist voor stateless apps. (Dit verhoogt de latentie en mogelijk introduceert consistentieproblemen.).
* **Gegevensanalyse en werkstromen**: Hallo snelle leesbewerkingen en schrijfbewerkingen van Service Fabric kunnen toepassingen betrouwbaar gebeurtenissen of gegevensstromen moeten verwerken. Service Fabric kunnen ook toepassingen die worden beschreven verwerking pijplijnen, waarbij de resultaten betrouwbaar en doorgegeven zijn moeten op toohello van de volgende fase zonder gegevensverlies verwerking. Het gaat hierbij om transactionele en financiële systemen, waarbij gegevens consistentie en berekeningen garanties essentieel zijn.
* **Gegevens die zijn verzameld, verwerkt en IoT**: omdat Service Fabric grote schaal worden verwerkt en lage latentie via de stateful services heeft, is het ideaal voor gegevensverwerking op miljoenen apparaten wanneer gegevens Hallo Hallo-apparaat en Hallo berekening zijn CO-locaties.
Wij hebben verschillende klanten die IoT systemen, met inbegrip van Service Fabric hebt gebouwd [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [Schneider elektrische](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) en [systemen net](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Casestudy voor ontwerp toepassing
Een aantal casestudy's die laat zien hoe Service Fabric is gebruikte toodesign toepassingen worden gepubliceerd op Hallo [Service Fabric-teamblog](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) en Hallo [microservices oplossingen site](https://azure.microsoft.com/solutions/microservice-applications/).

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Toepassingen bestaan uit staatloze en stateful microservices ontwerpen
Toepassingen maken met Azure Cloud Service-werkrollen is een voorbeeld van een staatloze service. Daarentegen behouden stateful microservices hun gezaghebbende status buiten Hallo-aanvraag en het antwoord. Dit biedt hoge beschikbaarheid en consistentie van Hallo status via eenvoudige API's die transactionele garanties die worden ondersteund door replicatie bieden. Service-Fabric stateful services democratize hoge beschikbaarheid, dat de toepassing tooall typen toepassingen, niet alleen databases en andere gegevensarchieven. Dit is een natuurlijke voortgang. Toepassingen hebt al verplaatst puur relationele databases voor hoge beschikbaarheid tooNoSQL databases te gebruiken. Hallo-toepassingen zelf kunnen nu hun 'hot' status en gegevens die worden beheerd in deze voor de prestaties verbeteren zonder verlies van betrouwbaarheid, consistentiecontrole of beschikbaarheid hebben.

Tijdens het bouwen van toepassingen die bestaan uit microservices, hebt u doorgaans een combinatie van staatloze web-apps (ASP.NET, Node.js, enz.) op staatloze en stateful Bedrijfsservices van middelste laag aanroept, alle geïmplementeerd in Hallo dezelfde Service Fabric-cluster Hallo-opdrachten voor het implementeren van Service Fabric gebruikt. Elk van deze services is niet afhankelijk met inachtneming van tooscale, betrouwbaarheid en resource gebruik, aanzienlijk verbeterd flexibiliteit in ontwikkeling levenscyclusbeheer.

Stateful microservices vereenvoudigen toepassing ontwerpen, omdat ze Hallo behoefte aanvullende wachtrijen Hallo verwijderen en caches die vereist tooaddress oudsher zijn Hallo beschikbaarheid en latentie vereisten van puur staatloze toepassingen. Aangezien stateful services natuurlijk maximaal beschikbare en lage latentie, betekent dit dat er minder bewegende delen toomanage beschikbaar in uw toepassing als geheel zijn. Hallo diagrammen hieronder illustreren Hallo verschillen tussen het ontwerpen van een toepassing die staatloze en een stateful. Door gebruik te maken van Hallo [Reliable Services](service-fabric-reliable-services-introduction.md) en [Reliable Actors](service-fabric-reliable-actors-introduction.md) programming modellen, stateful services complexiteit te verminderen toepassing bij het bereiken van maximale doorvoer en lage latentie.

## <a name="an-application-built-using-stateless-services"></a>Een toepassing die is gebouwd met behulp van stateless services
![Toepassing met behulp van staatloze service][Image1]

## <a name="an-application-built-using-stateful-services"></a>Een toepassing die is gebouwd met behulp van stateful services
![Toepassing met behulp van staatloze service][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen

* Te luisteren[casestudy's van klanten](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* Meer informatie over [casestudy's van klanten](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* Meer informatie over [patronen en scenario's](service-fabric-patterns-and-scenarios.md)

* Aan de slag ontwikkelen staatloze en stateful services met Service Fabric Hallo [betrouwbare services](service-fabric-reliable-services-quick-start.md) en [betrouwbare actoren](service-fabric-reliable-actors-get-started.md) programming modellen.
* Zie ook de volgende onderwerpen Hallo:
  * [Meer informatie over microservices](service-fabric-overview-microservices.md)
  * [Definiëren en beheren van de status van service](service-fabric-concepts-state.md)
  * [Beschikbaarheid van Service Fabric-services](service-fabric-availability-services.md)
  * [Schaal Service Fabric-services](service-fabric-concepts-scalability.md)
  * [Partitie Service Fabric-services](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
