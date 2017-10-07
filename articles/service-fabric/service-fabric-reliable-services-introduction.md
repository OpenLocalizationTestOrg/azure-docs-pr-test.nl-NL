---
title: aaaOverview van Hallo betrouwbare Service Fabric-Service-programmeermodel | Microsoft Docs
description: Informatie over Service Fabric van betrouwbare Service programmeermodel en schrijven van uw eigen services aan de slag.
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Overzicht van Reliable Services
Azure Service Fabric vereenvoudigt schrijven en staatloze en stateful Reliable Services beheren. Dit onderwerp wordt beschreven:

* Hallo Reliable Services programmeermodel voor staatloze en stateful services.
* Hallo keuzes u toomake hebben bij het schrijven van een betrouwbare Service.
* Sommige scenario's en voorbeelden van wanneer toouse betrouwbaar Services en hoe ze zijn geschreven.

Reliable Services is een Hallo programming modellen die beschikbaar is op de Service Fabric. Hallo andere is Hallo betrouwbare Actor programmeermodel, waarmee u een virtuele Actor-programmeermodel op Hallo Reliable Services model. Zie voor meer informatie over model voor Reliable Actors Hallo [inleiding tooService Fabric Reliable Actors](service-fabric-reliable-actors-introduction.md).

Service Fabric Hallo levensduur van de services van de inrichting en implementatie via bijwerken en verwijderen, beheert [Service Fabric-Toepassingsbeheer](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>Wat zijn Reliable Services?
Reliable Services biedt een eenvoudige, krachtige, op het hoogste niveau programming model toohelp u express wat belangrijk tooyour toepassing is. Met de Hallo Reliable Services programmeermodel gebruikt, beschikt u over:

* Toegang toohello rest van Hallo Service Fabric programming API's. In tegenstelling tot Service Fabric-Services is gemodelleerd als [Gast uitvoerbare bestanden](service-fabric-deploy-existing-app.md), Reliable Services toouse Hallo rest Hallo Service Fabric-API's direct ophalen. Hierdoor kunnen services:
  * query Hallo systeem
  * rapport health over entiteiten in Hallo-cluster
  * meldingen ontvangen over configuratie-en code
  * zoeken en te communiceren met andere services
  * (optioneel) gebruik Hallo [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md)
  * .. en toegang te krijgen tot toomany andere mogelijkheden via een eerste-klas programmeermodel in diverse programmeertalen.
* Een eenvoudige model voor het uitvoeren van uw eigen code die lijkt op modellen die u om te gebruikt programmeren. Uw code is een goed gedefinieerde toegangspunt en de levenscyclus van eenvoudig te beheren.
* Een communicatiemodel pluggable. Gebruik Hallo transport van uw keuze, zoals HTTP met [Web API](service-fabric-reliable-services-communication-webapi.md), WebSockets, aangepaste TCP-protocollen, of iets anders. Betrouwbare Services bieden sommige geweldige out-of-the-box-opties die u kunt gebruiken of u kunt uw eigen.
* Voor stateful services Hallo Reliable Services programmeermodel kunt u tooconsistently en veilig opslaan van uw status meteen in uw service met behulp van [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md). Betrouwbare verzamelingen zijn een eenvoudige reeks maximaal beschikbare en betrouwbare verzameling klassen die worden vertrouwd tooanyone die C# verzamelingen heeft gebruikt. Traditioneel vereist services externe systemen voor betrouwbare statusbeheer. Met betrouwbare verzamelingen kunt u uw status volgende tooyour berekenings Hello opslaan dezelfde hoge beschikbaarheid en betrouwbaarheid u tooexpect afkomstig zijn van maximaal beschikbare externe winkels hebt. Dit model verbetert ook latentie omdat u zijn CO-locatie Hallo berekenings- en status moet toofunction.

Bekijk deze video van Microsoft Virtual Academy voor een overzicht van Reliable services:<center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>Wat Reliable Services verschillende maakt?
Reliable Services in Service Fabric wijken af van de services die u hebt gemaakt voordat. Service Fabric biedt betrouwbaarheid, beschikbaarheid, consistentie en schaalbaarheid.

* **Betrouwbaarheid** - uw service blijft zelfs in onbetrouwbaar omgevingen waar uw machines mislukken of druk op de netwerkverbinding, of in gevallen waarbij Hallo services zelf fouten en crashes optreden of mislukken. Voor stateful services, wordt de status behouden zelfs in Hallo aanwezigheid van het netwerk of andere fouten.
* **Beschikbaarheid** -uw-service is bereikbaar is en reageert. Service Fabric onderhoudt het gewenste aantal actieve exemplaren.
* **Schaalbaarheid** - Services worden ontkoppeld van specifieke hardware en ze kunnen vergroten of verkleinen desgewenst via Hallo toevoegen of verwijderen van de hardware of andere bronnen. Services zijn eenvoudig gepartitioneerde (met name in Hallo stateful geval) tooensure die Hallo service kan worden geschaald en ingang gedeeltelijke fouten. Services kunnen worden gemaakt en verwijderd via programmacode, waardoor meer exemplaren toobe ingezette zo nodig een dynamisch spreken in antwoord toocustomer aanvragen. Service Fabric raadt ten slotte services toobe lightweight. Service Fabric kunt duizenden services toobe ingericht in één proces, in plaats van verplicht stellen of dat het volledige OS-exemplaren of processen tooa één exemplaar van een service.
* **Consistentie** -gegevens zijn opgeslagen in deze service kan worden gegarandeerd toobe consistent. Dit geldt zelfs in meerdere betrouwbare verzamelingen binnen een service. Wijzigingen in verzamelingen in een service kunnen worden gemaakt op een transactioneel atomic manier.

## <a name="service-lifecycle"></a>De levenscyclus van de service
Of uw service stateful of stateless, bieden Reliable Services de levensduur van een eenvoudige, waarmee u snel plug-in uw code en aan de slag.  Er zijn maar een of twee methoden moet u tooimplement tooget uw service up-to-date en worden uitgevoerd.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -deze methode is waar Hallo service Hallo communicatie stack(s) dat deze toouse wil definieert. communicatiestack, zoals Hallo [Web API](service-fabric-reliable-services-communication-webapi.md), is wat definieert Hallo luisterende eindpunt of eindpunten voor Hallo service (hoe clients bereiken Hallo-service). Ook wordt gedefinieerd hoe Hallo-berichten die worden weergegeven met de Hallo rest van de servicecode Hallo werken.
* **RunAsync** -deze methode is waarin de zakelijke logica in uw service wordt uitgevoerd en waarbij deze zou ere van eventuele achtergrondtaken die moeten worden uitgevoerd voor Hallo levensduur van Hallo-service. Hallo annulering token dat is opgegeven, is een signaal voor wanneer dat werk moet worden gestopt. Bijvoorbeeld als Hallo-service moet toopull berichten uit een wachtrij van betrouwbare en ze te verwerken, is dit waarbij die werken gebeurt.

Als u over reliable services voor Hallo eerst leert, leest u op! Als u een gedetailleerd overzicht van de levenscyclus van betrouwbare services Hallo zoekt, u kunt Ga te[in dit artikel](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Voorbeeld van de services
Dit programmeermodel weet, gaat nu een kort overzicht van twee verschillende services toosee hoe deze onderdelen in elkaar passen.

### <a name="stateless-reliable-services"></a>Staatloze Reliable Services
Een stateless service is een waar er is geen status die binnen het Hallo-service wordt onderhouden tussen aanroepen. Geen status die aanwezig is, is volledig beschikbare en geen vereist synchronisatie, replicatie, persistentie of hoge beschikbaarheid.

Neem bijvoorbeeld een rekenmachine die heeft geen geheugen en alle bewerkingen voor voorwaarden tooperform in één keer ontvangt.

In dit geval Hallo `RunAsync()` (C#) of `runAsync()` (Java) Hallo service kan niet leeg zijn, omdat er geen achtergrond taakverwerking die service Hallo toodo moet. Wanneer Hallo Rekenmachine service hebt gemaakt, wordt een `ICommunicationListener` (C#) of `CommunicationListener` (Java) (bijvoorbeeld [Web API](service-fabric-reliable-services-communication-webapi.md)) die een luisterende eindpunt op sommige poort wordt geopend. Dit eindpunt luisteren Hiermee up toohello andere berekenings-methoden (voorbeeld: "Toevoegen (n1, n2)") die openbare API van Hallo Rekenmachine definiëren.

Wanneer er wordt een aanroep van een client, relevante Hallo-methode wordt aangeroepen en Hallo Rekenmachine-service uitvoert Hallo-bewerkingen op Hallo gegevens opgeven en deze Hallo resultaat retourneert. Geen status worden niet opgeslagen.

Geen interne status niet opslaan vereenvoudigt de Rekenmachine van dit voorbeeld. Maar de meeste services worden niet echt staatloze. In plaats daarvan extern ze hun status toosome andere store. (Bijvoorbeeld een web-app die is afhankelijk van de sessiestatus behouden in een archief met back-ups maken of de cache is niet staatloze.)

Een voorbeeld van hoe stateless services worden gebruikt in Service Fabric is als een front-end dat gegarandeerd Hallo openbare API voor een webtoepassing. Hallo front-end-service wordt vervolgens gesproken toostateful services toocomplete een gebruikersaanvraag. In dit geval zijn de aanroepen van clients gerichte tooa bekende poort, bijvoorbeeld 80, waarbij Hallo staatloze service luistert. Deze service staatloze Hallo aanroep ontvangt en bepaalt of Hallo aanroep van een vertrouwde partij is en welke service het bestemd is voor.  Vervolgens staatloze Hallo-service stuurt Hallo aanroep toohello juiste partitie van Hallo stateful service en wordt gewacht op een antwoord. Wanneer Hallo staatloze service een antwoord ontvangt, wordt de oorspronkelijke client toohello geantwoord. Een voorbeeld van deze service is in onze voorbeelden [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). Dit is slechts één voorbeeld van dit patroon in de voorbeelden van hello, anderen er zijn ook andere controles.

### <a name="stateful-reliable-services"></a>Stateful Reliable Services
Een stateful service is een die een gedeelte van de status behouden van consistente en aanwezig is in de volgorde voor Hallo service toofunction moeten hebben. Houd rekening met een service die voortdurend berekent een oplopende gemiddelde van een bepaalde waarde op basis van updates die het ontvangt. toodo, het moet de huidige set Hallo van inkomende aanvragen moet tooprocess en huidige gemiddelde Hallo. Alle services die worden opgehaald, verwerkt en wordt informatie opgeslagen in een externe winkel (zoals een Azure-blob of tabel store vandaag) is stateful. De status blijven alleen in de externe Statusopslag Hallo.

De meeste services opslaan vandaag hun status extern, aangezien Hallo externe archief wat biedt betrouwbaarheid, beschikbaarheid, schaalbaarheid en consistentie voor die status. In Service Fabric-services zijn niet vereist toostore extern hun status. Service Fabric zorgt voor deze vereisten voor zowel servicecode Hallo Hallo-servicestatus.

> [!NOTE]
> Ondersteuning voor betrouwbare Stateful Services is niet beschikbaar op Linux nog (voor C# of Java).
>

Stel, dat we willen toowrite een service waarmee afbeeldingen worden verwerkt. toodo dit Hallo service duurt in een installatiekopie en Hallo reeks conversies tooperform op die installatiekopie. Deze service retourneert een communicatie-listener (we Stel dat het is een WebAPI) dat gegarandeerd een API, zoals `ConvertImage(Image i, IList<Conversion> conversions)`. Wanneer een aanvraag ontvangt, Hallo service slaat deze op in een `IReliableQueue`, en retourneert een id toohello client zodat deze Hallo aanvraag kunt bijhouden.

In deze service `RunAsync()` complexere kan worden. Hallo-service heeft een lus in de `RunAsync()` die aanvragen van haalt `IReliableQueue` en voert Hallo conversies aangevraagd. Hallo resultaten ophalen opgeslagen in een `IReliableDictionary` zodat wanneer Hallo client terugkomt krijgen ze hun geconverteerde installatiekopieën. tooensure dat zelfs als er iets Hallo afbeelding mislukt niet verloren, deze betrouwbare Service zou ophalen uit de wachtrij hello, Hallo-conversies uitvoeren en Hallo resultaat opslaan in een enkele transactie. In dit geval wordt het Hallo-bericht is verwijderd uit de wachtrij Hallo en Hallo resultaten worden opgeslagen in Hallo resultaat woordenlijst alleen wanneer Hallo conversies voltooid zijn. Hallo-service kan ook pull-hallo afbeelding buiten het Hallo-wachtrij en direct op te slaan in een externe winkel. Dit vermindert Hallo hoeveelheid Hallo-statusservice toomanage heeft, maar verhoogt de complexiteit omdat Hallo-service tookeep Hallo benodigde metagegevens toomanage Hallo externe winkel heeft. Met de methode als er iets is mislukt blijft Hallo middelste Hallo aanvraag in Hallo wachtrij wachten toobe verwerkt.

Één ding toonote over deze service is dat deze als een normale .NET-service klinkt. Hallo enige verschil is dat Hallo gegevensstructuren wordt gebruikt (`IReliableQueue` en `IReliableDictionary`) worden geleverd door de Service Fabric en maximaal betrouwbare, beschikbare en consistent zijn.

## <a name="when-toouse-reliable-services-apis"></a>Wanneer toouse betrouwbare API's voor Services
Als geen van de volgende Hallo kenmerkend zijn voor de behoeften van uw toepassing-service, moet u betrouwbare Services-API's overwegen:

* U wilt dat uw service-code (en desgewenst-status) toobe maximaal beschikbare en betrouwbare
* U moet transactionele garanties over meerdere van status (bijvoorbeeld orders en items op).
* De status van uw toepassing kan natuurlijk worden gemodelleerd als betrouwbare woordenlijsten en wachtrijen.
* Uw toepassingen, code of de status moet toobe maximaal beschikbaar is met lage latentie lees- en schrijfbewerkingen.
* Uw toepassing moet toocontrol Hallo gelijktijdigheid of granulatie van de transactiebewerkingen in een of meer betrouwbare verzamelingen.
* U wilt toomanage Hallo communicatie of besturingselement Hallo partitieschema voor uw service.
* Uw code moet een gratis thread-runtime-omgeving.
* Uw toepassing moet toodynamically maken of vernietigen betrouwbare woordenlijsten of wachtrijen of hele Services tijdens runtime.
* In dat geval moet u tooprogrammatically Service Fabric-voorwaarde back-up en herstel functies in voor de status van uw service.
* Uw toepassing moet toomaintain wijzigingsoverzicht voor de eenheden van de status.
* U wilt toodevelop of de van de derde partij ontwikkeld, aangepaste statusproviders gebruiken.

## <a name="next-steps"></a>Volgende stappen
* [Betrouwbare Services snel starten](service-fabric-reliable-services-quick-start.md)
* [Reliable Services geavanceerde gebruik](service-fabric-reliable-services-advanced-usage.md)
* [Hallo model voor Reliable Actors](service-fabric-reliable-actors-introduction.md)
