---
title: Service Fabric niveau Toepassingsbewaking aaaAzure | Microsoft Docs
description: Informatie over de toepassing en service level gebeurtenissen en logboeken toomonitor gebruikt en onderzoeken van Azure Service Fabric-clusters.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a>Toepassing en service level genereren van gebeurtenis- en logboekbestanden

## <a name="instrumenting-hello-code-with-custom-events"></a>Hallo-code instrumenteren met aangepaste gebeurtenissen

Hallo code instrumenteren is Hallo basis voor de meeste andere aspecten van uw services bewaking. Instrumentatie is Hallo maar één manier weet dat er iets mis is en toodiagnose wat toobe vast moet. Hoewel het is technisch mogelijk tooconnect een foutopsporingsprogramma tooa productie-service, maar het is niet een gangbare optie. Dus is het belangrijk gedetailleerde gegevens.

Sommige producten softwareontwikkelaars automatisch uw code. Hoewel deze oplossingen goed werken kunnen, is bijna altijd handmatige instrumentation vereist. U moet voldoende informatie tooforensically fouten opsporen in de toepassing hello hebben in Hallo-end. Dit document beschrijft de verschillende benaderingen tooinstrumenting uw code en wanneer toochoose een benaderen via een andere.

## <a name="eventsource"></a>EventSource
Wanneer u een Service Fabric-oplossing van een sjabloon in Visual Studio maakt een **EventSource**-afgeleide klasse (**ServiceEventSource** of **ActorEventSource**) wordt gegenereerd. Een sjabloon is gemaakt, waarin u de gebeurtenissen voor uw toepassing of service kunt toevoegen. Hallo **EventSource** naam **moet** uniek zijn en moet worden gewijzigd van Hallo sjabloon standaardtekenreeks mijnbedrijf -&lt;oplossing&gt; - &lt; Project&gt;. Meerdere **EventSource** definities die gebruikmaken van dezelfde naam oorzaken uitvoeringstijd voor een probleem op Hallo. Elke gedefinieerde gebeurtenis moet een unieke id hebben. Als een id is niet uniek is, treedt er een runtime-fout op. Sommige organisaties preassign bereiken met waarden voor de id's tooavoid conflicten tussen afzonderlijke ontwikkelteams. Zie voor meer informatie [van Vance blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) of Hallo [MSDN-documentatie](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>Het gebruik van gestructureerde EventSource gebeurtenissen

Elk van de gebeurtenissen Hallo in Hallo-codevoorbeelden in deze sectie worden gedefinieerd voor een specifieke aanvraag, bijvoorbeeld wanneer een servicetype is geregistreerd. Wanneer u berichten door gebruiksvoorbeeld definiëren, kunnen gegevens worden verpakt met de tekst hello Hallo-fout en u kunt meer eenvoudig zoeken en filteren op basis van het Hallo-namen of waarden van Hallo eigenschappen opgegeven. Hallo instrumentation uitvoer structureren maakt het eenvoudiger tooconsume maar vereist meer gedachte en het tijdstip toodefine een nieuwe gebeurtenis voor elke gebruiksvoorbeeld. Sommige Gebeurtenisdefinities kunnen worden gedeeld door de gehele toepassing hello. Bijvoorbeeld, een methode starten of stoppen zou gebeurtenis hele veel services in een toepassing worden gebruikt. Een service, domeinspecifieke, zoals een systeem volgorde wellicht een **CreateOrder** gebeurtenis een eigen unieke gebeurtenis heeft. Deze aanpak mogelijk veel gebeurtenissen genereren en mogelijk coördinatie vereisen van id's op projectteams. 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a>EventSource gebruik algemeen

Omdat het definiëren van specifieke gebeurtenissen kan lastig zijn, definiëren veel mensen enkele gebeurtenissen met een gemeenschappelijke set parameters die in het algemeen hun informatie als een tekenreeks voeren. Veel van Hallo gestructureerd aspect is verbroken en is moeilijker toosearch en filter Hallo-resultaten. In deze methode voert worden enkele gebeurtenissen die meestal toohello logboekregistratieniveaus overeen gedefinieerd. Hallo volgende codefragment definieert een bericht voor foutopsporing en de fout:

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

Een hybride van gestructureerde en algemene instrumentation kunt ook werken goed. Gestructureerde instrumentation wordt gebruikt voor het melden van fouten en metrische gegevens. Algemene gebeurtenissen kunnen worden gebruikt voor Hallo gedetailleerde logboekregistratie die verbruikt door engineers voor probleemoplossing.

## <a name="aspnet-core-logging"></a>ASP.NET Core logboekregistratie

De belangrijke toocarefully plannen hoe u uw code wordt instrumenteren. Hallo rechts instrumentation plan kunt u mogelijk uw codebasis destabilizing en vervolgens hoeven tooreinstrument Hallo code voorkomen. tooreduce risico, kunt u een instrumentatiebiblotheek zoals [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), die deel uitmaakt van Microsoft ASP.NET Core. ASP.NET Core is een [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface die u met Hallo-provider van uw keuze, gebruiken kunt terwijl het minimaliseert Hallo invloed op bestaande code. U kunt ASP.NET Core voor Windows en Linux Hallo code gebruikt en volledige in Hallo .NET Framework, zodat uw code instrumentation is gestandaardiseerd. Dit is meer verkend hieronder:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Met behulp van Microsoft.Extensions.Logging in Service Fabric

1. Hallo Microsoft.Extensions.Logging NuGet-pakket toohello project u tooinstrument wilt toevoegen. Ook alle pakketten provider toe te voegen (Zie Hallo voorbeeld te volgen voor een pakket van derden). Zie voor meer informatie [logboekregistratie in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).
2. Voeg een **met** richtlijn voor bestand Microsoft.Extensions.Logging tooyour-service.
3. Definieer een persoonlijke variabele binnen uw serviceklasse.

  ```csharp
  private ILogger _logger = null;

  ```
4. Voeg deze code in Hallo constructor van uw serviceklasse:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Start uw code in uw methoden instrumenteren. Hier volgen enkele voorbeelden:

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Andere providers voor logboekregistratie

Sommige providers van derden gebruiken dat wordt beschreven in voorgaande sectie Hallo Hallo-benadering met inbegrip van [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), en [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). U kunt elk van deze in ASP.NET Core logboekregistratie aansluiten of u afzonderlijk kunt gebruiken. Serilog bevat een functie waarmee alle berichten van een logboek verrijkt. Deze functie kan worden nuttig toooutput Hallo service-naam, type en partitiegegevens. toouse deze mogelijkheid in Hallo ASP.NET-infrastructuur, moet u deze stappen uitvoeren:

1. Hallo Serilog, Serilog.Extensions.Logging, en Serilog.Sinks.Observable NuGet-pakketten toohello project toevoegen. Voor het volgende voorbeeld hello, moet u ook Serilog.Sinks.Literate toevoegen. Een betere benadering wordt verderop in dit artikel weergegeven.
2. In Serilog, maakt u een LoggerConfiguration en Hallo berichtenlogboek-exemplaar.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Voeg een constructor Serilog.ILogger argument toohello service, en Hallo nieuw gemaakte berichtenlogboek.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. In Hallo service constructor toevoegen na de code die u Hallo eigenschap enrichers voor Hallo maakt Hallo **ServiceTypeName**, **ServiceName**, **PartitionId**, en  **InstanceId** eigenschappen van Hallo-service. Een eigenschap enricher toohello ASP.NET Core logboekregistratie factory, worden ook toegevoegd zodat u Microsoft.Extensions.Logging.ILogger in uw code gebruiken kunt.

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. Instrument Hallo code Hallo hetzelfde als wanneer u ASP.NET Core zonder Serilog.

  >[!NOTE]
  >Het is raadzaam Hallo statisch gebruik geen Log.Logger Hello voorgaande voorbeeld. Service Fabric kan hosten meerdere exemplaren van Hallo dezelfde servicetype binnen een enkel proces. Als u statische Log.Logger hello, Hallo laatste schrijver van Hallo eigenschap enrichers wordt weergegeven voor alle exemplaren die worden uitgevoerd. Dit is een reden waarom Hallo _logger variabele persoonlijk lid van de serviceklasse Hallo wordt. Zorg ook Hallo _logger beschikbaar toocommon code, die alle services kan worden gebruikt.

## <a name="choosing-a-logging-provider"></a>Een provider logboekregistratie kiezen

Als uw toepassing afhankelijk van hoge prestaties is, **EventSource** is meestal een goede benadering. **EventSource** *doorgaans* minder bronnen gebruikt en beter presteert dan ASP.NET Core logboekregistratie of een van de oplossingen van derden beschikbaar van Hallo.  Dit is een probleem voor veel services, maar als uw service prestatiegerichte, met is niet **EventSource** mogelijk een betere keuze. Echter, tooget deze voordelen van gestructureerde aan te melden, **EventSource** moet een grotere geïnvesteerd van het technische team. Voer indien mogelijk een snelle prototype van een aantal logboekregistratieopties en kies vervolgens Hallo die het beste voldoet aan uw behoeften.

## <a name="next-steps"></a>Volgende stappen

Nadat u uw provider logboekregistratie tooinstrument uw toepassingen en services gekozen hebt, moeten uw logboeken en gebeurtenissen toobe geaggregeerd voordat ze kunnen worden verzonden tooany analysis platform. Meer informatie over [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) en [af](service-fabric-diagnostics-event-aggregation-wad.md) toobetter weet Hallo aanbevolen opties.
