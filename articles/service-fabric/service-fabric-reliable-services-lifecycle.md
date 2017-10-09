---
title: aaaOverview van Hallo levenscyclus van Azure Service Fabric Reliable Services | Microsoft Docs
description: Meer informatie over Hallo levenscyclus van andere gebeurtenissen in betrouwbare Service Fabric-services
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Overzicht van de levenscyclus van betrouwbare services
> [!div class="op_single_selector"]
> * [C# op Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java op Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Wanneer u nadenkt over Hallo levenscycli van Reliable Services, zijn Hallo basisprincipes van de levenscyclus van Hallo Hallo belangrijkste. In het algemeen:

- Tijdens het opstarten
  - Services zijn gebouwd
  - Ze hebben een kans tooconstruct en nul of meer listeners retourneren
  - Elke geretourneerde luisteraars worden geopend, zodat de communicatie met de Hallo-service
  - Hallo-Service RunAsync methode wordt aangeroepen, zodat Hallo service toodo langlopende of werk op de achtergrond
- Tijdens het afsluiten
  - Hallo annulering token doorgegeven tooRunAsync wordt geannuleerd en Hallo-listeners zijn gesloten
  - Eenmaal is voltooid, wordt Hallo serviceobject zelf destructed

Er zijn details rond Hallo exacte ordening van deze gebeurtenissen. Hallo-volgorde van gebeurtenissen mogelijk in het bijzonder enigszins, afhankelijk van Hallo betrouwbare Service Stateless of Stateful wijzigen. Daarnaast hebben we voor stateful services toodeal met Hallo primaire wisselen scenario. Tijdens deze reeks Hallo-functie van primaire replica is overgedragen tooanother (of terugkomt) zonder Hallo-service is afgesloten. Ten slotte hebben we toothink over fout of storing voorwaarden.

## <a name="stateless-service-startup"></a>Staatloze service is gestart
levenscyclus van een staatloze service Hallo is zeer eenvoudig. Hier volgt Hallo volgorde van gebeurtenissen:

1. Hallo wordt Service samengesteld
2. Klik in de parallelle twee dingen gebeuren:
    - `StatelessService.CreateServiceInstanceListeners()`wordt aangeroepen en elke geretourneerde luisteraars worden geopend. `ICommunicationListener.OpenAsync()`voor elke listener wordt aangeroepen
    - Hallo van service `StatelessService.RunAsync()` methode wordt aangeroepen
3. Indien aanwezig, Hallo van service `StatelessService.OnOpenAsync()` methode wordt aangeroepen. Dit is een ongewoon onderdrukking, maar deze beschikbaar is.

Het is belangrijk toonote of er is geen ordening tussen Hallo aanroepen toocreate en open Hallo listeners en RunAsync. Hallo-listeners geopend voordat RunAsync wordt gestart. Op deze manier RunAsync mogelijk uiteindelijk aangeroepen voordat de communicatielisteners Hallo geopend zijn of zelfs is samengesteld. Als geen synchronisatie vereist is, is het een oefening toohello implementeerder gehandhaafd. Algemene oplossingen:

  - Soms werkt listeners alleen als andere informatie is gemaakt of gewerkte. Voor stateless services die werk kan doorgaans worden uitgevoerd op andere locaties, zoals: 
    - in de constructor van het Hallo-service
    - tijdens het Hallo `CreateServiceInstanceListeners()` aanroepen
    - Als onderdeel van het Hallo-constructie van Hallo-listener zelf
  - Soms wil hello code in RunAsync niet toostart totdat het Hallo-listeners zijn geopend. In dit geval is aanvullende coördinatie nodig. Een veelgebruikte oplossing is een aantal markering binnen Hallo-listeners die aangeeft wanneer ze zijn voltooid. Deze markering wordt vervolgens gecontroleerd in RunAsync voordat u doorgaat tooactual werk.

## <a name="stateless-service-shutdown"></a>Afsluiten van de staatloze service
Wanneer een stateless service wordt afgesloten, wordt hello hetzelfde patroon gevolgd, alleen in omgekeerde volgorde:

1. Parallel
    - Alle open listeners worden gesloten. `ICommunicationListener.CloseAsync()`voor elke listener wordt aangeroepen.
    - Hallo annulering token te doorgegeven`RunAsync()` is geannuleerd. Controleren of Hallo annulering van token `IsCancellationRequested` eigenschap true retourneert, en als aangeroepen Hallo-token `ThrowIfCancellationRequested` methode er wordt een `OperationCanceledException`.
2. Eenmaal `CloseAsync()` is voltooid op elke listener en `RunAsync()` ook is voltooid, Hallo-service `StatelessService.OnCloseAsync()` methode wordt aangeroepen, indien aanwezig. Het is ongewoon toooverride `StatelessService.OnCloseAsync()`.
3. Na `StatelessService.OnCloseAsync()` is voltooid, Hallo serviceobject wordt destructed

## <a name="stateful-service-startup"></a>Stateful service starten
Stateful services hebben een vergelijkbaar patroon toostateless services, met enkele wijzigingen. Bij het opstarten van een stateful service, is Hallo volgorde van gebeurtenissen als volgt uit:

1. Hallo wordt Service samengesteld
2. `StatefulServiceBase.OnOpenAsync()`wordt aangeroepen. Dit is uncommonly overschreven in Hallo-service.
3. Hallo plaats volgende parallel
    - `StatefulServiceBase.CreateServiceReplicaListeners()`wordt aangeroepen 
      - Als het Hallo-service is een primaire alle geretourneerde luisteraars geopend. `ICommunicationListener.OpenAsync()`voor elke listener wordt aangeroepen.
      - Als Hallo-service een secundaire database is, alleen deze listeners gemarkeerd als `ListenOnSecondary = true` worden geopend. -Listeners die geopend op de secundaire replica's zijn met is minder gangbaar.
    - Hallo als Hallo Service momenteel van een primaire, Hallo service is `StatefulServiceBase.RunAsync()` methode wordt aangeroepen
4. Nadat alle replica-listener Hallo `OpenAsync()` aanroepen voltooien en `RunAsync()` wordt aangeroepen, `StatefulServiceBase.OnChangeRoleAsync()` wordt aangeroepen. Dit is uncommonly overschreven in Hallo-service.

Op dezelfde manier toostateless services, is er geen coördinatie tussen Hallo volgorde in welke Hallo listeners zijn gemaakt en geopend en wanneer RunAsync wordt genoemd. Als u moet coördinatie, kunnen Hallo oplossingen zijn veel Hallo dezelfde. Er is één extra aanvraag: zeggen dat Hallo aanroepen die binnenkomen bij de communicatielisteners Hallo informatie bewaard binnen enkele vereist [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md). Omdat Hallo communicatielisteners kunnen openen voordat Hallo betrouwbare verzamelingen worden gelezen of geschreven en voordat RunAsync kan worden gestart, is enkele aanvullende coördinatie nodig. Hallo eenvoudigste en meest voorkomende oplossing is voor Hallo communicatie listeners tooreturn sommige foutcode die Hallo gebruikt tooknow tooretry Hallo clientaanvraag.

## <a name="stateful-service-shutdown"></a>Stateful service afsluiten
Op dezelfde manier tooStateless services, Hallo lifecycle gebeurtenissen tijdens het afsluiten zijn Hallo dezelfde als tijdens het opstarten, maar omgekeerd. Wanneer een stateful service wordt afgesloten, hello volgende gebeurtenissen:

1. Parallel
    - Alle open listeners worden gesloten. `ICommunicationListener.CloseAsync()`voor elke listener wordt aangeroepen.
    - Hallo annulering token te doorgegeven`RunAsync()` is geannuleerd. Controleren of Hallo annulering van token `IsCancellationRequested` eigenschap true retourneert, en als aangeroepen Hallo-token `ThrowIfCancellationRequested` methode er wordt een `OperationCanceledException`.
2. Eenmaal `CloseAsync()` is voltooid op elke listener en `RunAsync()` ook is voltooid, Hallo-service `StatefulServiceBase.OnChangeRoleAsync()` wordt aangeroepen. (Dit is uncommonly overschreven in Hallo-service.)
    - Wachten op RunAsync het toocomplete is alleen nodig als de replica van deze service een primaire is.
3. Eenmaal Hallo `StatefulServiceBase.OnChangeRoleAsync()` methode is voltooid, hello `StatefulServiceBase.OnCloseAsync()` methode wordt aangeroepen. Dit is een ongewoon onderdrukking, maar deze beschikbaar is.
3. Na `StatefulServiceBase.OnCloseAsync()` is voltooid, Hallo serviceobject wordt destructed.

## <a name="stateful-service-primary-swaps"></a>Primaire worden verwisseld stateful service
Terwijl een stateful service wordt uitgevoerd, alleen hebben hello primaire replica's van die stateful services hun communicatielisteners geopend en hun RunAsync-methode aangeroepen. Secundaire zijn gebouwd, maar er worden geen verdere aanroepen niet zien. Terwijl een stateful service echter wordt uitgevoerd, kunt welke replica is momenteel Hallo primaire wijzigen. Wat betekent dit in termen van Hallo lifecycle gebeurtenissen die een replica kunt zien? Hallo gedrag Hallo stateful replica ziet, is afhankelijk van de Hallo replica wordt gedegradeerd of gepromoveerd tijdens Hallo wisselen.

### <a name="for-hello-primary-being-demoted"></a>Voor primaire gedegradeerd Hallo
Service Fabric moet deze replica toostop berichten worden verwerkt en eventuele achtergrondwerk hiervan is afgesloten. Als gevolg hiervan wordt deze stap ziet er vergelijkbare toowhen Hallo service afgesloten. Een verschil is dat Hallo-Service is niet destructed of gesloten nadat een secundaire database blijft. Hallo volgende API's worden genoemd:

1. Parallel
    - Alle open listeners worden gesloten. `ICommunicationListener.CloseAsync()`voor elke listener wordt aangeroepen.
    - Hallo annulering token te doorgegeven`RunAsync()` is geannuleerd. Controleren of Hallo annulering van token `IsCancellationRequested` eigenschap true retourneert, en als aangeroepen Hallo-token `ThrowIfCancellationRequested` methode er wordt een `OperationCanceledException`.
2. Eenmaal `CloseAsync()` is voltooid op elke listener en `RunAsync()` ook is voltooid, Hallo-service `StatefulServiceBase.OnChangeRoleAsync()` wordt aangeroepen. Dit is uncommonly overschreven in Hallo-service.

### <a name="for-hello-secondary-being-promoted"></a>Voor secundaire hello wordt gepromoveerd
Op deze manier Service Fabric moet deze replica toostart luisteren naar berichten op het Hallo-kabel en start u eventuele achtergrondtaken die het is belangrijk. Zodoende kan dit proces lijkt vergelijkbare toowhen Hallo service hebt gemaakt, met uitzondering van die replica Hallo bestaat zelf al. Hallo volgende API's worden genoemd:

1. Parallel
    - `StatefulServiceBase.CreateServiceReplicaListeners()`wordt aangeroepen en elke geretourneerde luisteraars worden geopend. `ICommunicationListener.OpenAsync()`voor elke listener wordt aangeroepen.
    - Hallo van service `StatefulServiceBase.RunAsync()` methode wordt aangeroepen
2. Nadat alle replica-listener Hallo `OpenAsync()` aanroepen voltooien en `RunAsync()` is aangeroepen, `StatefulServiceBase.OnChangeRoleAsync()` wordt aangeroepen. Dit is uncommonly overschreven in Hallo-service.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Veelvoorkomende problemen tijdens het afsluiten van de stateful service en de primaire degradatie
Service Fabric-wijzigingen Hallo primaire van een stateful service voor een aantal redenen. Hallo meest voorkomende zijn [cluster herverdeling](service-fabric-cluster-resource-manager-balancing.md) en [upgrade van de toepassing](service-fabric-application-upgrade.md). Tijdens deze bewerkingen (en tijdens het afsluiten van de normale service, zoals u zien zou als Hallo-service is verwijderd), is het belangrijk dat Hallo Hallo service ten opzichte van `CancellationToken`. Services die door deze annulering niet correct verwerken wordt enkele problemen optreden. Deze bewerkingen niet in het bijzonder traag omdat Service Fabric wordt gewacht op Hallo services toostop probleemloos. Dit kan uiteindelijk leiden toofailed upgrades die time-out en terug te draaien. Fout toohonor Hallo annulering token kan ook leiden tot imbalanced clusters omdat Hallo services kunnen niet worden uitgevoerd omdat het duurt te lang toomove maar knooppunten hot krijgen ze ergens anders. 

Aangezien Hallo services stateful, is het ook waarschijnlijk dat ze Hallo gebruiken [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md). In Service Fabric bij een primaire wordt gedegradeerd, is Hallo eerste dingen die plaatsvindt of de status van onderliggende schrijftoegang toohello is ingetrokken. Dit leidt tweede reeks problemen die invloed op Hallo service lifecycle hebben kunnen tooa. Hallo verzamelingen return uitzonderingen op basis van Hallo timing en Hiermee wordt aangegeven of Hallo replica wordt verplaatst of afsluiten. Deze uitzonderingen moeten correct worden verwerkt. Uitzonderingen in Service Fabric vallen in de permanente [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) en tijdelijke [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet) categorieën. Permanente uitzonderingen moeten worden geregistreerd en veroorzaakt tijdens het Hallo tijdelijke uitzonderingen worden geprobeerd op basis van bepaalde Pogingslogica.

Afhandeling van uitzonderingen Hallo die afkomstig van het gebruik van Hallo zijn `ReliableCollections` in combinatie met gebeurtenissen van de levenscyclus van de service is een belangrijk onderdeel van de testen en valideren van een betrouwbare Service. Hallo aanbeveling is altijd toorun uw service onder belasting tijdens het uitvoeren van upgrades en [chaos testen](service-fabric-controlled-chaos.md) voordat u ooit implementeert tooproduction. Deze eenvoudige stappen kunt u ervoor te zorgen dat uw service correct is geïmplementeerd en de levenscyclus van gebeurtenissen correct worden verwerkt.


## <a name="notes-on-service-lifecycle"></a>Opmerkingen bij de levenscyclus van de service
  - Beide Hallo `RunAsync()` methode en Hallo `CreateServiceReplicaListeners/CreateServiceInstanceListeners` aanroepen zijn optioneel. Een service kan één van deze beide of geen van beide hebben. Bijvoorbeeld, als het Hallo-service alle zijn werk in het antwoord toouser aanroepen doet, hoeft niet voor tooimplement `RunAsync()`. Alleen Hallo communicatielisteners en hun bijbehorende code zijn nodig. Op deze manier maken communicatielisteners retourneren is optioneel, want het Hallo-service mogelijk alleen de achtergrond toodo werken en hoeft dus alleen tooimplement`RunAsync()`
  - Is geldig voor een service-toocomplete `RunAsync()` is en dat het resultaat van deze. Voltooien is niet een voorwaarde is mislukt. Voltooien van `RunAsync()` geeft aan dat de achtergrondwerk Hallo van Hallo-service is voltooid. Voor betrouwbare stateful services `RunAsync()` opnieuw wordt aangeroepen als Hallo replica van primaire tooSecondary werden gedegradeerd en vervolgens back tooPrimary gepromoveerd.
  - Als een service afsluit `RunAsync()` door er een onverwachte uitzondering is opgetreden, betekent dit een fout. Hallo-serviceobject wordt afgesloten en een statusfout gemeld.
  - Hoewel er geen tijdslimiet bij het retourneren van deze methoden, kunt u onmiddellijk tooReliable verzamelingen verliezen Hallo mogelijkheid toowrite en daarom echte werk niet voltooien. Het is raadzaam dat u zo snel mogelijk na ontvangst van de annuleringsaanvraag Hallo terugkeren. Als uw service toothese API-aanroepen niet reageert binnen een redelijk tijdsbestek die service Fabric mogelijk geforceerd uw service beëindigen. Meestal gebeurt dit alleen tijdens toepassingsupgrades of wanneer een service wordt verwijderd. Deze time-out is 15 minuten standaard.
  - Fouten in Hallo `OnCloseAsync()` pad leiden tot een `OnAbort()` wordt aangeroepen dit is een kans van de laatste kans best-effort voor Hallo tooclean up service en laat alle bronnen die ze hebben aangevraagd.

## <a name="next-steps"></a>Volgende stappen
- [Inleiding tooReliable Services](service-fabric-reliable-services-introduction.md)
- [Betrouwbare Services snel starten](service-fabric-reliable-services-quick-start.md)
- [Reliable Services geavanceerde gebruik](service-fabric-reliable-services-advanced-usage.md)
