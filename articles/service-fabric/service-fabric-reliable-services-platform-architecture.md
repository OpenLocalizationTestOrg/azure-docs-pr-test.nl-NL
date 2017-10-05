---
title: Betrouwbare service-architectuur | Microsoft Docs
description: Overzicht van de architectuur van betrouwbare Service voor stateful en staatloze services
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: a00a16945356b9731485554e06df46528b5c7bb2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Architectuur voor stateful en staatloze Reliable Services
Een Azure Service Fabric betrouwbare Service mogelijk stateful of stateless. Elk type van de service wordt uitgevoerd binnen een specifieke architectuur. Deze architecturen worden beschreven in dit artikel.
Zie de [overzicht betrouwbare Service](service-fabric-reliable-services-introduction.md) voor meer informatie over de verschillen tussen stateful en staatloze services.

## <a name="stateful-reliable-services"></a>Stateful Reliable Services
### <a name="architecture-of-a-stateful-service"></a>Architectuur van een stateful service
![Architectuurdiagram van een stateful service](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Stateful betrouwbare Service
Een stateful betrouwbare Service kunnen worden afgeleid van de StatefulService of StatefulServiceBase klasse. Beide van deze basisklassen worden geleverd door de Service Fabric. Ze bieden verschillende niveaus van ondersteuning en abstractie voor de stateful service aan de Service Fabric-- en om deel te nemen als een service in het Service Fabric-cluster.

StatefulService is afgeleid van StatefulServiceBase. StatefulServiceBase-services biedt meer flexibiliteit, maar vereist meer inzicht in het inwendige van Service Fabric.
Zie de [overzicht betrouwbare Service](service-fabric-reliable-services-introduction.md) en [betrouwbare Service gebruik van geavanceerde](service-fabric-reliable-services-advanced-usage.md) voor meer informatie over de details van services met behulp van de klassen StatefulService en StatefulServiceBase schrijven.

Beide basisklassen beheren de levensduur en de rol van de service-implementatie. De service-implementatie kan virtuele methoden van een basisklasse negeren als de service-implementatie te doen op die punten in de levenscyclus van de implementatie--heeft of als u wordt gevraagd een communicatie-listener-object maken. Houd er rekening mee dat hoewel een service-implementatie mogelijk een eigen communicatieobject listener ICommunicationListener, in het bovenstaande diagram, blootstellen implementeren de communicatie-listener wordt geïmplementeerd door de Service Fabric--als de service-implementatie gebruikmaakt van een communicatie-listener die wordt geïmplementeerd met Service Fabric.

Een stateful betrouwbare Service gebruikt de betrouwbare status manager om te profiteren van betrouwbare verzamelingen. Betrouwbare verzamelingen zijn lokale gegevensstructuren die maximaal beschikbaar zijn voor de service--die, ze altijd beschikbaar zijn, ongeacht de failovers van de service. Elk type betrouwbare verzameling wordt geïmplementeerd door een betrouwbare state-provider.
Zie voor meer informatie over betrouwbare verzamelingen de [betrouwbare verzamelingen overzicht](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Statusbeheer voor betrouwbare en statusproviders
Statusbeheer voor het betrouwbare is het object dat betrouwbare statusproviders beheert. Heeft de functionaliteit voor het maken, verwijderen, opsommen en zorg ervoor dat de van betrouwbare statusproviders persistent zijn en maximaal beschikbaar zijn. Een exemplaar van de provider betrouwbare status vormt een exemplaar van een gegevensstructuur persistent zijn en maximaal beschikbare, zoals een woordenboek of een wachtrij.

Elke betrouwbare state-provider wordt een interface die wordt gebruikt door een stateful service om te communiceren met de betrouwbare state-provider. Bijvoorbeeld IReliableDictionary wordt gebruikt om een koppeling met de betrouwbare woordenlijst terwijl IReliableQueue wordt gebruikt voor de wachtrij van betrouwbare-interface. Alle betrouwbare statusproviders implementeren de IReliableState-interface.

Statusbeheer voor het betrouwbare heeft een interface met de naam IReliableStateManager waarmee u toegang krijgt tot het van een stateful service. Interfaces voor betrouwbare statusproviders worden via IReliableStateManager geretourneerd.

Statusbeheer voor het betrouwbare maakt gebruik van een invoegtoepassing architectuur zodat nieuwe typen van betrouwbare verzamelingen kunnen dynamisch worden aangesloten.

De betrouwbare woordenlijst en betrouwbare wachtrij zijn gebaseerd op de uitvoering van een krachtige, samengestelde differentiële store.

### <a name="transactional-replicator"></a>Transactionele replicatie
Het onderdeel van de transactionele replicatie is verantwoordelijk voor het garanderen dat de status van een service (dat wil zeggen, de status in de betrouwbare status manager en de betrouwbare verzamelingen) consistent is op alle replica's waarop de service wordt uitgevoerd. Ook zorgt ervoor dat de status is opgeslagen in het logboek. De betrouwbare status manager-interfaces met de transactionele replicatie via een persoonlijke mechanisme.

De transactionele replicatie gebruikt een netwerkprotocol om te communiceren staat met andere replica's van het service-exemplaar zodat alle replica's informatie over de bijgewerkte status hebben.

De transactionele replicatie maakt gebruik van een logboek om vast te leggen van informatie over de status, zodat de statusinformatie proces blijft of het knooppunt is vastgelopen. De interface in het logboek is via een persoonlijke mechanisme.

### <a name="log"></a>Logboek
Het onderdeel logboek biedt een krachtige permanente opslag die kan worden geoptimaliseerd voor het schrijven naar draaiende of SSD-schijven.  Het ontwerp van het logboek is voor de permanente opslag (dat wil zeggen, harde schijven) lokaal op de knooppunten die de stateful service wordt uitgevoerd. Hierdoor kunnen lage latentie en hoge doorvoer, in vergelijking met externe permanente opslag, niet lokaal op het knooppunt is.

Het onderdeel logboek maakt gebruik van meerdere logboekbestanden. Er is een knooppunt wide gedeelde logboekbestand dat alle replica's gebruiken als de laagste latentie en hoogste doorvoer te geven kan voor het opslaan van gegevens van de gebruikersstatus. Standaard wordt het gedeelde logboek geplaatst in de werkmap van de Service Fabric-knooppunt, maar kan ook worden geconfigureerd om te worden geplaatst op een andere locatie, bij voorkeur op een schijf gereserveerd voor alleen het gedeelde logboek. Elke replica voor de service heeft ook een specifieke logboekbestand en het toegewezen logboek in de werkmap van de service is geplaatst. Er is geen methode voor het configureren van het toegewezen logboek worden geplaatst op een andere locatie.

Het gedeelde logboek is een overgangsstatus gebied voor informatie over de status van de replica terwijl het toegewezen logboekbestand is de uiteindelijke bestemming waar deze wordt bewaard. In dit ontwerp is de statusinformatie eerst naar de gedeelde logboekbestand geschreven en traag verplaatst naar het speciale logboekbestand op de achtergrond. Op deze manier moet het schrijven naar het gedeelde logboek de laagste latentie en hoogste doorvoer waarmee de service uitgevoerd sneller maken.

Leest en schrijft naar het gedeelde logboek worden gedaan via rechtstreekse I/O naar vooraf toegewezen ruimte op de schijf voor de gedeelde logboekbestand. Als u optimaal gebruik van schijfruimte op het station met speciale Logboeken, wordt het toegewezen logboekbestand gemaakt als een NTFS-sparse bestand. Houd er rekening mee dat hierdoor meer schijfruimte en het besturingssysteem wordt weergegeven de speciale logboekbestanden met veel meer schijfruimte dan daadwerkelijk wordt gebruikt.

Het logboek is niet alleen uit een minimale gebruikersmodus interface naar het logboek geschreven als een stuurprogramma voor de kernelmodus. Als een stuurprogramma voor de kernelmodus kan worden uitgevoerd, kunt het logboek voor de beste prestaties tot alle services die gebruikmaken van deze bieden.

Zie voor meer informatie over het configureren van het logboek [configureren van stateful Reliable Services](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Staatloze betrouwbare Service
### <a name="architecture-of-a-stateless-service"></a>Architectuur van een staatloze service
![Architectuurdiagram van een staatloze service](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Staatloze betrouwbare Service
Staatloze-serverimplementaties afgeleid van de klasse StatelessService of StatelessServiceBase. De klasse StatelessServiceBase kunt meer flexibiliteit dan de StatelessService-klasse.
Beide basisklassen beheren de levensduur en de rol van een service.

De service-implementatie kan virtuele methoden van een basisklasse negeren als de service te doen op die punten in de levenscyclus van de service--heeft of als u wordt gevraagd een communicatie-listener-object maken. Houd er rekening mee dat hoewel de service kan de eigen communicatieobject listener blootstellen ICommunicationListener, in het bovenstaande diagram, implementeren de communicatie-listener wordt geïmplementeerd door de Service Fabric, aangezien deze service-implementatie gebruikmaakt van een communicatie-listener die wordt geïmplementeerd met Service Fabric.

Zie de [overzicht betrouwbare Service](service-fabric-reliable-services-introduction.md) en [betrouwbare Service gebruik van geavanceerde](service-fabric-reliable-services-advanced-usage.md) voor meer informatie over de details van services met behulp van de klassen StatelessService en StatelessServiceBase schrijven.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Service Fabric:

[Overzicht van betrouwbare service](service-fabric-reliable-services-introduction.md)

[Snel starten](service-fabric-reliable-services-quick-start.md)

[Overzicht van betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md)

[Betrouwbare service advanced gebruik](service-fabric-reliable-services-advanced-usage.md)

[Configuratie van betrouwbare service](service-fabric-reliable-services-configuration.md)  

