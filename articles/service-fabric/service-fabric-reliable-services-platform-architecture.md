---
title: architectuur van de service aaaReliable | Microsoft Docs
description: Overzicht van architectuur van Hallo betrouwbare Service voor stateful en staatloze services
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
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Architectuur voor stateful en staatloze Reliable Services
Een Azure Service Fabric betrouwbare Service mogelijk stateful of stateless. Elk type van de service wordt uitgevoerd binnen een specifieke architectuur. Deze architecturen worden beschreven in dit artikel.
Zie Hallo [overzicht betrouwbare Service](service-fabric-reliable-services-introduction.md) voor meer informatie over Hallo verschillen tussen stateful en staatloze services.

## <a name="stateful-reliable-services"></a>Stateful Reliable Services
### <a name="architecture-of-a-stateful-service"></a>Architectuur van een stateful service
![Architectuurdiagram van een stateful service](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Stateful betrouwbare Service
Een stateful betrouwbare Service kunnen worden afgeleid van StatefulService Hallo of StatefulServiceBase-klasse. Beide van deze basisklassen worden geleverd door de Service Fabric. Ze bieden verschillende niveaus van ondersteuning en abstractie voor Hallo stateful service toointerface met Service Fabric-- en tooparticipate als een service binnen Hallo Service Fabric-cluster.

StatefulService is afgeleid van StatefulServiceBase. StatefulServiceBase-services biedt meer flexibiliteit, maar vereist meer inzicht in Hallo inwendige van Service Fabric.
Zie Hallo [overzicht betrouwbare Service](service-fabric-reliable-services-introduction.md) en [betrouwbare Service gebruik van geavanceerde](service-fabric-reliable-services-advanced-usage.md) voor meer informatie over specificaties hello om services te schrijven met behulp van de klassen StatefulService en StatefulServiceBase Hallo .

Beide basisklassen beheren Hallo levensduur en rol van de implementatie van Hallo. Hallo service-implementatie kan virtuele methoden van een basisklasse negeren als Hallo service-implementatie heeft werk toodo op die punten in de levenscyclus van Hallo service-implementatie-- of als deze wil toocreate een communicatie-listener-object. Opmerking dat hoewel een service-implementatie mogelijk een eigen communicatieobject listener ICommunicationListener, blootstellen in Hallo bovenstaande diagram, geïmplementeerd Hallo communicatie-listener wordt geïmplementeerd door Service Fabric--zoals Hallo service-implementatie maakt gebruik van een communicatie-listener die wordt geïmplementeerd met Service Fabric.

Een stateful betrouwbare Service gebruikt Hallo betrouwbare status manager tootake profiteren van betrouwbare verzamelingen. Betrouwbare verzamelingen zijn lokale gegevensstructuren die maximaal beschikbare toohello service--die zijn, ze altijd beschikbaar zijn, ongeacht de failovers van de service. Elk type betrouwbare verzameling wordt geïmplementeerd door een betrouwbare state-provider.
Zie voor meer informatie over betrouwbare verzamelingen Hallo [betrouwbare verzamelingen overzicht](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Statusbeheer voor betrouwbare en statusproviders
Hallo betrouwbare status manager is Hallo-object dat betrouwbare statusproviders beheert. Hallo functionaliteit toocreate, verwijderen, opsommen en ervoor te zorgen dat de betrouwbare statusproviders Hallo persistent zijn en maximaal beschikbaar is. Een exemplaar van de provider betrouwbare status vormt een exemplaar van een gegevensstructuur persistent zijn en maximaal beschikbare, zoals een woordenboek of een wachtrij.

Elke betrouwbare state-provider wordt een interface die wordt gebruikt door een stateful service toointeract met Hallo betrouwbare state-provider. IReliableDictionary is bijvoorbeeld gebruikte toointerface Hallo betrouwbare woordenlijst, terwijl IReliableQueue gebruikte toointerface met betrouwbare Hallo-wachtrij. Alle betrouwbare statusproviders implementeren hello IReliableState-interface.

Hallo betrouwbare status manager heeft een interface met de naam IReliableStateManager waarmee toegang tooit van een stateful service. Interfaces tooreliable statusproviders worden via IReliableStateManager geretourneerd.

Hallo betrouwbare status manager maakt gebruik van een invoegtoepassing architectuur zodat nieuwe typen van betrouwbare verzamelingen kunnen dynamisch worden aangesloten.

Hallo betrouwbare woordenlijst en betrouwbare wachtrij zijn gebaseerd op Hallo uitvoering van een krachtige, samengestelde differentiële store.

### <a name="transactional-replicator"></a>Transactionele replicatie
het onderdeel transactionele replicatie Hallo is verantwoordelijk voor het garanderen dat Hallo status van een service (dat wil zeggen, Hallo status binnen Hallo betrouwbare statusbeheer en betrouwbare verzamelingen Hallo) consistent is op alle replica's waarop Hallo-service wordt uitgevoerd. Ook zorgt ervoor dat Hallo status is opgeslagen in Hallo logboek. Hallo betrouwbare status manager interfaces met de Hallo transactionele replicatie via een persoonlijke mechanisme.

Hallo transactional replicator gebruikt een netwerk protocol toocommunicate staat met andere replica's van de service-exemplaar Hallo zodat alle replica's informatie over de bijgewerkte status hebben.

Hallo transactional replicator wordt informatie over de status van een logboek toopersist, zodat informatie over de status van de Hallo proces blijft of het knooppunt is vastgelopen. Hallo interface toohello logboek is via een persoonlijke mechanisme.

### <a name="log"></a>Logboek
Hallo logboek onderdeel biedt een krachtige permanente opslag die kan worden geoptimaliseerd voor het schrijven van toospinning of SSD-schijven.  Hallo-ontwerp van Hallo-logboek is voor Hallo permanente opslag (dat wil zeggen, harde schijven) toobe lokale toohello knooppunten of Hallo stateful service is gestart. Hierdoor kunnen lage latenties en hoge doorvoersnelheid als vergeleken tooremote permanente opslag, geen lokale toohello knooppunt is.

Hallo logboek onderdeel meerdere logboekbestanden gebruikt. Er is een knooppunt wide gedeelde logboekbestand dat alle replica's gebruiken als de laagste latentie Hallo en hoogste doorvoer te geven kan voor het opslaan van gegevens van de gebruikersstatus. Standaard gedeelde logboek Hallo in Hallo Service Fabric-knooppunt werk directory is geplaatst, maar mogelijk ook geconfigureerde toobe aan een andere locatie, bij voorkeur op een schijf gereserveerd voor alleen Hallo gedeelde logboek geplaatst. Elke replica voor Hallo-service heeft ook een specifieke logboekbestand en speciale Hallo-logboek in Hallo werk servicemap is geplaatst. Er is geen mechanisme tooconfigure Hallo dedicated logboek toobe geplaatst op een andere locatie.

Hallo gedeelde logboek is een overgangsstatus gebied voor informatie over de status van de replica van de hello, tijdens het Hallo toegewezen logboekbestand Hallo eindbestemming waar deze wordt bewaard. In dit ontwerp Hallo statusinformatie eerste geschreven toohello gedeelde logboekbestand en vervolgens toohello toegewezen logboekbestand op de achtergrond Hallo traag verplaatst. Op deze manier zou hello schrijven toohello gedeelde logboek hebben de laagste latentie Hallo en hoogste doorvoer waarmee Hallo service toomake voortgang sneller.

Leest en schrijft toohello gedeelde logboek via directe i/o toopreallocated ruimte op schijf voor de gedeelde logboekbestand Hallo Hallo klaar bent. tooallow optimaal gebruik van schijfruimte op station Hallo met speciale Logboeken, Hallo toegewezen logboekbestand gemaakt als een NTFS-sparse-bestand. Houd er rekening mee dat hierdoor meer schijfruimte vrij en Hallo OS Hallo dedicated logboekbestanden met veel meer schijfruimte ziet dan daadwerkelijk wordt gebruikt.

Hallo-logboek is niet alleen uit een minimale gebruikersmodus interface toohello-logboek geschreven als een stuurprogramma voor de kernelmodus. Uitgevoerd als een stuurprogramma voor de kernelmodus, kunt Hallo logboek bieden de beste prestaties Hallo tooall-services die worden gebruikt.

Zie voor meer informatie over het configureren van Hallo logboek [configureren van stateful Reliable Services](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Staatloze betrouwbare Service
### <a name="architecture-of-a-stateless-service"></a>Architectuur van een staatloze service
![Architectuurdiagram van een staatloze service](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Staatloze betrouwbare Service
Staatloze-serverimplementaties worden afgeleid van Hallo StatelessService of StatelessServiceBase-klasse. Hallo StatelessServiceBase klasse kunt meer flexibiliteit dan Hallo StatelessService klasse.
Beide basisklassen beheren Hallo levensduur en functie van een service.

Hallo service-implementatie kan virtuele methoden van een basisklasse negeren als Hallo service werk toodo op die punten in de levenscyclus van de service Hallo--heeft of als deze wil toocreate een communicatie-listener-object. Houd er rekening mee dat hoewel Hallo-service kan de eigen communicatieobject listener ICommunicationListener, blootstellen in Hallo bovenstaande diagram, implementeren Hallo communicatie-listener wordt geïmplementeerd door de Service Fabric, aangezien deze service-implementatie gebruikmaakt van een communicatie listener die wordt geïmplementeerd met Service Fabric.

Zie Hallo [overzicht betrouwbare Service](service-fabric-reliable-services-introduction.md) en [betrouwbare Service gebruik van geavanceerde](service-fabric-reliable-services-advanced-usage.md) voor meer informatie over specificaties Hallo van services met behulp van de klassen StatelessService en StatelessServiceBase Hallo schrijven .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Service Fabric:

[Overzicht van betrouwbare service](service-fabric-reliable-services-introduction.md)

[Snel starten](service-fabric-reliable-services-quick-start.md)

[Overzicht van betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md)

[Betrouwbare service advanced gebruik](service-fabric-reliable-services-advanced-usage.md)

[Configuratie van betrouwbare service](service-fabric-reliable-services-configuration.md)  

