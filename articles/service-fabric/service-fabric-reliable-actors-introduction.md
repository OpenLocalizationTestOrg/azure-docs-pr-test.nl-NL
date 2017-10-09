---
title: aaaService Fabric betrouwbare actoren overzicht | Microsoft Docs
description: Inleiding toohello Service Fabric model voor Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>Inleiding tooService Fabric Reliable Actors
Reliable Actors is een Service Fabric-toepassingsframework op basis van Hallo [virtuele Actor](http://research.microsoft.com/en-us/projects/orleans/) patroon. Hallo betrouwbare actoren API biedt een single thread-programmeermodel die gebouwd op Hallo schaalbaarheid en betrouwbaarheid garanties geleverd door de Service Fabric.

## <a name="what-are-actors"></a>Wat zijn Actors?
Een actor is een eenheid geïsoleerd, onafhankelijk van de berekenings- en staat met één thread worden uitgevoerd. Hallo [actor patroon](https://en.wikipedia.org/wiki/Actor_model) is een rekenkundige model gelijktijdige of gedistribueerde systemen in die een groot aantal deze actoren kunt tegelijkertijd uitvoeren en onafhankelijk van elkaar. Actoren kunnen communiceren met elkaar en meer actoren te maken.

### <a name="when-toouse-reliable-actors"></a>Wanneer toouse Reliable Actors
Service Fabric Reliable Actors is een implementatie van Hallo actor ontwerppatroon. Net als bij een ontwerppatroon software past Hallo besluit of toouse een specifiek patroon wordt gemaakt op basis van het al dan niet de probleem voor het ontwerpen van een software Hallo-patroon.

Hoewel Hallo actor ontwerppatroon een goede aanpassen tooa aantal gedistribueerde systemen problemen en scenario's, zorgvuldige overweging van Hallo beperkingen van Hallo patroon en implementeren van Hallo-framework die moet worden gemaakt is. Algemene richtlijnen, moet u overwegen Hallo actor patroon toomodel uw probleem of scenario als:

* De ruimte van uw probleem betrekking heeft op een groot aantal (duizendtallen of meer) van kleine, onafhankelijke en geïsoleerde eenheden van de status en logica.
* U toowork met één thread-objecten die geen aanzienlijke interactie met externe onderdelen, waaronder status opvragen van een set die vereist is.
* Uw actor-exemplaren niet aanroepfuncties met onvoorspelbare vertragingen worden geblokkeerd door uitgifte van i/o-bewerkingen.

## <a name="actors-in-service-fabric"></a>Actoren in Service Fabric
In Service Fabric actoren zijn geïmplementeerd in Hallo Reliable Actors framework: een toepassing op basis van actor-patroon framework gebouwd boven [Service Fabric Reliable Services](service-fabric-reliable-services-introduction.md). Elke betrouwbare Actor-service die u schrijft is daadwerkelijk een gepartitioneerde, stateful betrouwbare Service.

Elke actor is gedefinieerd als een exemplaar van een actortype, identieke toohello manier .NET-object is een exemplaar van een .NET-type. Bijvoorbeeld, kan er een actortype dat Hallo-functionaliteit van een rekenmachine implementeert en er zijn veel actoren van dat type die worden gedistribueerd op verschillende knooppunten in een cluster. Elke dergelijke actor wordt uniek geïdentificeerd door een actor-ID.

### <a name="actor-lifetime"></a>Actor-levensduur
Service Fabric actoren zijn virtueel, wat betekent dat hun levensduur is niet gebonden tootheir in het geheugen weergave. Hierdoor kunnen hoeven ze niet toobe expliciet gemaakt of vernietigd. Hallo Reliable Actors runtime activeert automatisch een Hallo actor eerst die een aanvraag voor die actor-ID ontvangt. Als een actor niet voor een bepaalde periode gebruikt wordt, Hallo Reliable Actors runtime garbagecollection-verzamelt Hallo in het geheugen-object. Ook blijven kennis van de Hallo actor bestaan mocht toobe geactiveerd later nodig. Zie voor meer informatie [Actor lifecycle en garbage collection](service-fabric-reliable-actors-lifecycle.md).

Deze virtuele actor levensduur abstractie voert enkele waarschuwingen als gevolg van Hallo virtuele actor model en in feite Hallo Reliable Actors uitvoering op tijdstippen afwijkt van dit model.

* Een actor wordt automatisch geactiveerd (waardoor een actor object toobe samengesteld) Hallo eerst een bericht verzonden tooits actor-ID. Hallo actor-object is na een bepaalde tijd, garbage collector zijn verzameld. In Hallo toekomst Hallo actor-ID opnieuw gebruiken, wordt een nieuwe actor object toobe samengesteld. Status van een actor outlives levensduur van het Hallo-object als opgeslagen in Hallo status manager.
* Een actormethode aanroepen voor een actor-ID activeert die actor. Om deze reden hebben acteur types hun constructor impliciet door Hallo runtime worden aangeroepen. Daarom clientcode die parameters toohello actor constructor van het type, niet doorgeven, hoewel parameters mag van toohello actor-constructor worden doorgegeven door Hallo-service zelf. Hallo-resultaat is dat actoren kunnen worden geconstrueerd in een status gedeeltelijk geïnitialiseerd door Hallo tijd die andere methoden worden genoemd, als Hallo actor initialisatieparameters van Hallo-client vereist. Er is geen één toegangspunt voor de Hallo activering van een actor van Hallo-client.
* Hoewel Reliable Actors impliciet actor-objecten maken. u hebt Hallo mogelijkheid tooexplicitly een actor en de status verwijderd.

### <a name="distribution-and-failover"></a>Distributie en failover
tooprovide schaalbaarheid en betrouwbaarheid, Service Fabric actoren in Hallo-cluster en automatisch distribueert ze migreert van knooppunten toohealthy waarden zoals vereist. Dit is een abstractie via een [betrouwbare gepartitioneerde stateful Service](service-fabric-concepts-partitioning.md). Distributie, schaalbaarheid, betrouwbaarheid en automatische failover zijn alle opgegeven grond Hallo feit die actoren worden uitgevoerd binnen een stateful betrouwbare Service met de naam van Hallo *Actor Service*.

Actors zijn verdeeld over Hallo partities Hallo Actor-Service en deze partities zijn verdeeld over Hallo knooppunten in een Service Fabric-cluster. Elke partitie service bevat een set van actoren. Service Fabric beheert distributie en failover van Hallo-partities.

Bijvoorbeeld, een actor-service met negen partities geïmplementeerd toothree knooppunten Hallo standaard actor partitie plaatsing gebruikt thusly zou worden gedistribueerd:

![Betrouwbare actoren distributie][2]

Hallo Actor Framework beheert partitie schema en de sleutel bereik-instellingen voor u. Dit vereenvoudigt enkele mogelijkheden, maar ook een nadelige invloed sommige overweging:

* Reliable Services kunt u toochoose een partitieschema sleutel bereik (als u een bereik partitieschema) en partitie count. Reliable Actors beperkte toohello bereik partitieschema (Hallo uniform Int64 schema) is en u Hallo volledige Int64 sleutel bereik vereist.
* Standaard worden actoren willekeurig in partities, wat resulteert in een gelijkmatige verdeling geplaatst.
* Omdat actoren willekeurig worden geplaatst, moet worden verwacht dat actor-bewerkingen altijd netwerkcommunicatie moet, met inbegrip van serialisatie en deserialisatie van methode-aanroepgegevens, latentie en overhead aangaan.
* In geavanceerde scenario's is het mogelijk toocontrol actor partitie plaatsing via Int64 actor-id's die toospecific partities worden toegewezen. Echter, doen dus kan resulteren in een distributie onbalans van actoren meerdere partities.

Voor meer informatie over hoe actorservices worden gepartitioneerd, Raadpleeg te[partitioneren concepten voor actoren](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

### <a name="actor-communication"></a>Actor-communicatie
Actor-interacties worden gedefinieerd in een interface die wordt gedeeld door Hallo actor die Hallo-interface implementeert en Hallo-client die een proxy opgehaald tooan actor via Hallo dezelfde interface. Omdat deze interface asynchroon gebruikte tooinvoke actor-methoden is, moet u elke methode op Hallo-interface moet geretourneerd.

Methode-aanroepen en hun antwoorden uiteindelijk resulteren in netwerkaanvragen via Hallo-cluster, geval Hallo argumenten en resultaattypen Hallo Hallo taken dat ze retourneren serializable door Hallo-platform moet. In het bijzonder, moeten ze [gegevenscontract serialiseerbaar](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

#### <a name="hello-actor-proxy"></a>Hallo actor-proxy
Hallo Reliable Actors client API biedt communicatie tussen een actor-exemplaar en een actor-client. toocommunicate met een actor een client maakt een actor proxy-object dat Hallo actor-interface implementeert. Hallo-client communiceert met de Hallo actor door aanroepen methoden op Hallo proxy-object. Hallo actor proxy kan worden gebruikt voor client-naar-actor en actor-actor-communicatie.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Hallo twee soorten informatie gebruikt toocreate Hallo actor proxyobject zijn Hallo actor-ID en de naam van de toepassing hello. Hallo actor-ID is uniek voor Hallo acteur, terwijl de naam van de toepassing hello Hallo identificeert [Service Fabric-toepassing](service-fabric-reliable-actors-platform.md#application-model) waarop Hallo actor wordt geïmplementeerd.

Hallo `ActorProxy`(C#) / `ActorProxyBase`klasse (Java) aan clientzijde Hallo voert Hallo nodig resolutie toolocate Hallo actor door-ID en een communicatiekanaal met het openen. Het toolocate Hallo actor in geval van Hallo van communicatiefouten en failovers ook opnieuw probeert. Als gevolg hiervan heeft levering van berichten Hallo volgende kenmerken:

* Levering van berichten is zo goed mogelijke poging.
* Actoren mogelijk dubbele berichten van Hallo dezelfde client.

### <a name="concurrency"></a>Gelijktijdigheid
Hallo Reliable Actors runtime biedt een eenvoudige inschakelen op basis van een toegangsmodel voor toegang tot actor-methoden. Dit betekent dat niet meer dan één thread actief binnen een actor-object-code op elk gewenst moment zijn kan. Schakel gebaseerde toegang vereenvoudigt gelijktijdige systemen als er geen synchronisatiemechanismen voor toegang tot gegevens nodig is. Het betekent ook systemen moeten worden ontworpen met speciale overwegingen voor Hallo single thread toegang aard van elk actor-exemplaar.

* Een enkele actor-exemplaar kan niet meer dan één verzoek tegelijkertijd wordt verwerkt. Een actor-exemplaar kan een knelpunt doorvoer veroorzaken als het verwachte toohandle gelijktijdige aanvragen.
* Actoren kunnen impasse op elkaar, als er een circulaire verzoek tussen twee actors tijdens een externe aanvraag wordt gedaan tooone van Hallo actoren tegelijkertijd. Hallo actor runtime wordt automatisch de tijd op actor aangeroepen en genereert een uitzondering toohello aanroeper toointerrupt impasse situaties.

![Betrouwbare actoren communicatie][3]

#### <a name="turn-based-access"></a>Schakel gebaseerde toegang
Een Schakel bestaat uit Hallo uitvoeren van een actormethode in antwoord tooa aanvraag uit andere actoren of clients of Hallo uitvoeren van een [timer/herinnering](service-fabric-reliable-actors-timers-reminders.md) retouraanroep. Hoewel deze methoden en retouraanroepen asynchrone,-Hallo actoren runtime ze komt niet interleave. Een Schakel moet volledig is voltooid voordat een nieuwe Schakel is toegestaan. Met andere woorden, een actor-methode of timer/herinnering callback die momenteel wordt uitgevoerd moet volledig is voltooid voordat u een nieuwe aanroep tooa methode of retouraanroep is toegestaan. Een methode of de retouraanroep wordt beschouwd als toohave is beëindigd als Hallo uitvoering heeft geretourneerd van Hallo-methode of retouraanroep en Hallo taak geretourneerd door het Hallo-methode of retouraanroep is voltooid. Wordt het bewerken van benadrukken dat die op basis van Schakel gelijktijdigheid zelfs in verschillende methoden en timers retouraanroepen is voldaan.

Hallo actoren runtime op basis van Schakel gelijktijdigheid door ophalen van een afzonderlijke actorvergrendeling aan begin van een beurt Hallo afgedwongen en Hallo vergrendeling achter Hallo Hallo inschakelen. Schakel gebaseerde gelijktijdigheid van taken wordt dus afgedwongen op basis van per actor en niet via actoren. Actor-methoden en timer/herinnering retouraanroepen kunnen tegelijkertijd uitvoeren namens actoren.

Hallo volgende voorbeeld illustreert Hallo hierboven concepten. Houd rekening met een actortype waarmee twee asynchrone methoden (bijvoorbeeld *Method1* en *Method2*), een timer en een herinnering. Hallo diagram hieronder toont een voorbeeld van een tijdlijn voor Hallo uitvoering van deze methoden en retouraanroepen namens twee actoren (*ActorId1* en *ActorId2*) die deel uitmaken van toothis actor-type.

![Betrouwbare actoren runtime op basis van Schakel gelijktijdigheid van taken en -toegang][1]

Dit diagram volgt deze conventies:

* Elke verticale lijn bevat Hallo logische stroom van de uitvoering van een methode of een retouraanroep namens een bepaalde actor.
* Hallo gemarkeerd op elke verticale lijn gebeurtenissen in chronologische volgorde met nieuwere gebeurtenissen hieronder oudere.
* Verschillende kleuren worden gebruikt voor het bijbehorende toodifferent actoren tijdlijnen.
* Markering is gebruikte tooindicate Hallo duur voor welke Hallo afzonderlijke actorvergrendeling wordt vastgehouden namens een methode of een retouraanroep.

Sommige tooconsider belangrijke punten:

* Terwijl *Method1* wordt uitgevoerd namens *ActorId2* in antwoord tooclient aanvraag *xyz789*, een andere clientaanvraag (*abc123*) binnenkomt die vereist ook *Method1* toobe uitgevoerd door *ActorId2*. Tweede uitvoering van echter Hallo *Method1* begint niet tot Hallo eerdere uitvoering is voltooid. Op deze manier is geregistreerd door een herinnering *ActorId2* wordt geactiveerd tijdens *Method1* wordt uitgevoerd in reactie tooclient aanvraag *xyz789*. Hallo wordt herinnering retouraanroep uitgevoerd alleen na beide uitvoeringen van *Method1* zijn voltooid. Dit alles is vanwege tooturn gebaseerde gelijktijdigheid van taken wordt afgedwongen voor *ActorId2*.
* Op deze manier ook inschakelen op basis van een gelijktijdigheid van taken wordt afgedwongen voor *ActorId1*, zoals wordt weergegeven door de uitvoering van Hallo *Method1*, *Method2*, en Hallo timer-retouraanroep namens *ActorId1* gebeurt er in een seriële wijze.
* De uitvoering van *Method1* namens *ActorId1* overlapt met de uitvoering ervan namens *ActorId2*. Dit is omdat op basis van Schakel gelijktijdigheid alleen binnen een actor en niet tussen actoren wordt afgedwongen.
* In sommige Hallo methode/callback uitvoeringen Hallo `Task`(C#) / `CompletableFuture`(Java) geretourneerd door Hallo methode/retouraanroep is voltooid nadat het Hallo-methode retourneert. In sommige andere is Hallo asynchrone bewerking al voltooid door Hallo tijd Hallo methode/callback retourneert. In beide gevallen worden Hallo afzonderlijke actorvergrendeling wordt vrijgegeven nadat beide Hallo methode/callback retourneert en Hallo asynchrone bewerking is voltooid.

#### <a name="reentrancy"></a>Herintreding
Hallo actoren runtime kunt herintreding standaard. Dit betekent dat wanneer een actormethode van *Actor A* een methode wordt aangeroepen op *Actor B*, die op zijn beurt een andere methode aanroepen op *Actor A*, dat methode toorun is toegestaan. Dit is omdat deze deel uitmaakt van Hallo dezelfde logische aanroep-keten context. Alle timer en herinnering aanroepen beginnen met de nieuwe logische aanroepcontext Hallo. Zie Hallo [Reliable Actors herintreding](service-fabric-reliable-actors-reentrancy.md) voor meer informatie.

#### <a name="scope-of-concurrency-guarantees"></a>Bereik van garanties gelijktijdigheid van taken
Hallo actoren runtime biedt deze garanties gelijktijdigheid van taken in situaties waar het Hallo-aanroep van deze methoden bepaalt. Bijvoorbeeld, biedt deze garanties voor Hallo methode aanroepen die worden uitgevoerd in reactie tooa clientaanvraag en voor de timer- en herinnering retouraanroepen. Echter als Hallo actor code rechtstreeks deze methoden buiten Hallo-mechanismen die zijn opgegeven door Hallo actoren runtime roept, kan niet Hallo runtime geeft garanties gelijktijdigheid van taken. Bijvoorbeeld, als Hallo-methode wordt aangeroepen in de context van een taak die is niet gekoppeld aan het Hallo-taak die wordt geretourneerd door Hallo actor methoden hello, vervolgens Hallo runtime kan niet gelijktijdigheid garanties bieden. Als het Hallo-methode is aangeroepen vanuit een thread die actor Hallo maakt op een eigen Hallo runtime ook kan niet en geef vervolgens garanties gelijktijdigheid van taken. Daarom tooperform bewerkingen op de achtergrond, actoren moeten gebruiken [actor timers en actor herinneringen](service-fabric-reliable-actors-timers-reminders.md) die op basis van Schakel gelijktijdigheid respecteren.

## <a name="next-steps"></a>Volgende stappen
* Aan de slag met het bouwen van uw eerste Reliable Actors-service:
   * [Aan de slag met Reliable Actors op .NET](service-fabric-reliable-actors-get-started.md)
   * [Aan de slag met Reliable Actors op Java](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
