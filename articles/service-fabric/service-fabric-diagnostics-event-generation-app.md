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
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="c10cd-103">Toepassing en service level genereren van gebeurtenis- en logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="c10cd-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="c10cd-104">Hallo-code instrumenteren met aangepaste gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c10cd-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="c10cd-105">Hallo code instrumenteren is Hallo basis voor de meeste andere aspecten van uw services bewaking.</span><span class="sxs-lookup"><span data-stu-id="c10cd-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="c10cd-106">Instrumentatie is Hallo maar één manier weet dat er iets mis is en toodiagnose wat toobe vast moet.</span><span class="sxs-lookup"><span data-stu-id="c10cd-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="c10cd-107">Hoewel het is technisch mogelijk tooconnect een foutopsporingsprogramma tooa productie-service, maar het is niet een gangbare optie.</span><span class="sxs-lookup"><span data-stu-id="c10cd-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="c10cd-108">Dus is het belangrijk gedetailleerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="c10cd-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="c10cd-109">Sommige producten softwareontwikkelaars automatisch uw code.</span><span class="sxs-lookup"><span data-stu-id="c10cd-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="c10cd-110">Hoewel deze oplossingen goed werken kunnen, is bijna altijd handmatige instrumentation vereist.</span><span class="sxs-lookup"><span data-stu-id="c10cd-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="c10cd-111">U moet voldoende informatie tooforensically fouten opsporen in de toepassing hello hebben in Hallo-end.</span><span class="sxs-lookup"><span data-stu-id="c10cd-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="c10cd-112">Dit document beschrijft de verschillende benaderingen tooinstrumenting uw code en wanneer toochoose een benaderen via een andere.</span><span class="sxs-lookup"><span data-stu-id="c10cd-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="c10cd-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="c10cd-113">EventSource</span></span>
<span data-ttu-id="c10cd-114">Wanneer u een Service Fabric-oplossing van een sjabloon in Visual Studio maakt een **EventSource**-afgeleide klasse (**ServiceEventSource** of **ActorEventSource**) wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c10cd-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="c10cd-115">Een sjabloon is gemaakt, waarin u de gebeurtenissen voor uw toepassing of service kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c10cd-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="c10cd-116">Hallo **EventSource** naam **moet** uniek zijn en moet worden gewijzigd van Hallo sjabloon standaardtekenreeks mijnbedrijf -&lt;oplossing&gt; - &lt; Project&gt;.</span><span class="sxs-lookup"><span data-stu-id="c10cd-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="c10cd-117">Meerdere **EventSource** definities die gebruikmaken van dezelfde naam oorzaken uitvoeringstijd voor een probleem op Hallo.</span><span class="sxs-lookup"><span data-stu-id="c10cd-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="c10cd-118">Elke gedefinieerde gebeurtenis moet een unieke id hebben.</span><span class="sxs-lookup"><span data-stu-id="c10cd-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="c10cd-119">Als een id is niet uniek is, treedt er een runtime-fout op.</span><span class="sxs-lookup"><span data-stu-id="c10cd-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="c10cd-120">Sommige organisaties preassign bereiken met waarden voor de id's tooavoid conflicten tussen afzonderlijke ontwikkelteams.</span><span class="sxs-lookup"><span data-stu-id="c10cd-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="c10cd-121">Zie voor meer informatie [van Vance blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) of Hallo [MSDN-documentatie](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="c10cd-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="c10cd-122">Het gebruik van gestructureerde EventSource gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="c10cd-122">Using structured EventSource events</span></span>

<span data-ttu-id="c10cd-123">Elk van de gebeurtenissen Hallo in Hallo-codevoorbeelden in deze sectie worden gedefinieerd voor een specifieke aanvraag, bijvoorbeeld wanneer een servicetype is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="c10cd-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="c10cd-124">Wanneer u berichten door gebruiksvoorbeeld definiëren, kunnen gegevens worden verpakt met de tekst hello Hallo-fout en u kunt meer eenvoudig zoeken en filteren op basis van het Hallo-namen of waarden van Hallo eigenschappen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c10cd-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="c10cd-125">Hallo instrumentation uitvoer structureren maakt het eenvoudiger tooconsume maar vereist meer gedachte en het tijdstip toodefine een nieuwe gebeurtenis voor elke gebruiksvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c10cd-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="c10cd-126">Sommige Gebeurtenisdefinities kunnen worden gedeeld door de gehele toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="c10cd-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="c10cd-127">Bijvoorbeeld, een methode starten of stoppen zou gebeurtenis hele veel services in een toepassing worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10cd-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="c10cd-128">Een service, domeinspecifieke, zoals een systeem volgorde wellicht een **CreateOrder** gebeurtenis een eigen unieke gebeurtenis heeft.</span><span class="sxs-lookup"><span data-stu-id="c10cd-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="c10cd-129">Deze aanpak mogelijk veel gebeurtenissen genereren en mogelijk coördinatie vereisen van id's op projectteams.</span><span class="sxs-lookup"><span data-stu-id="c10cd-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

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

### <a name="using-eventsource-generically"></a><span data-ttu-id="c10cd-130">EventSource gebruik algemeen</span><span class="sxs-lookup"><span data-stu-id="c10cd-130">Using EventSource generically</span></span>

<span data-ttu-id="c10cd-131">Omdat het definiëren van specifieke gebeurtenissen kan lastig zijn, definiëren veel mensen enkele gebeurtenissen met een gemeenschappelijke set parameters die in het algemeen hun informatie als een tekenreeks voeren.</span><span class="sxs-lookup"><span data-stu-id="c10cd-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="c10cd-132">Veel van Hallo gestructureerd aspect is verbroken en is moeilijker toosearch en filter Hallo-resultaten.</span><span class="sxs-lookup"><span data-stu-id="c10cd-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="c10cd-133">In deze methode voert worden enkele gebeurtenissen die meestal toohello logboekregistratieniveaus overeen gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c10cd-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="c10cd-134">Hallo volgende codefragment definieert een bericht voor foutopsporing en de fout:</span><span class="sxs-lookup"><span data-stu-id="c10cd-134">hello following snippet defines a debug and error message:</span></span>

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

<span data-ttu-id="c10cd-135">Een hybride van gestructureerde en algemene instrumentation kunt ook werken goed.</span><span class="sxs-lookup"><span data-stu-id="c10cd-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="c10cd-136">Gestructureerde instrumentation wordt gebruikt voor het melden van fouten en metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="c10cd-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="c10cd-137">Algemene gebeurtenissen kunnen worden gebruikt voor Hallo gedetailleerde logboekregistratie die verbruikt door engineers voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="c10cd-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="c10cd-138">ASP.NET Core logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="c10cd-138">ASP.NET Core logging</span></span>

<span data-ttu-id="c10cd-139">De belangrijke toocarefully plannen hoe u uw code wordt instrumenteren.</span><span class="sxs-lookup"><span data-stu-id="c10cd-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="c10cd-140">Hallo rechts instrumentation plan kunt u mogelijk uw codebasis destabilizing en vervolgens hoeven tooreinstrument Hallo code voorkomen.</span><span class="sxs-lookup"><span data-stu-id="c10cd-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="c10cd-141">tooreduce risico, kunt u een instrumentatiebiblotheek zoals [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), die deel uitmaakt van Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c10cd-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="c10cd-142">ASP.NET Core is een [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface die u met Hallo-provider van uw keuze, gebruiken kunt terwijl het minimaliseert Hallo invloed op bestaande code.</span><span class="sxs-lookup"><span data-stu-id="c10cd-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="c10cd-143">U kunt ASP.NET Core voor Windows en Linux Hallo code gebruikt en volledige in Hallo .NET Framework, zodat uw code instrumentation is gestandaardiseerd.</span><span class="sxs-lookup"><span data-stu-id="c10cd-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="c10cd-144">Dit is meer verkend hieronder:</span><span class="sxs-lookup"><span data-stu-id="c10cd-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="c10cd-145">Met behulp van Microsoft.Extensions.Logging in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c10cd-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="c10cd-146">Hallo Microsoft.Extensions.Logging NuGet-pakket toohello project u tooinstrument wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c10cd-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="c10cd-147">Ook alle pakketten provider toe te voegen (Zie Hallo voorbeeld te volgen voor een pakket van derden).</span><span class="sxs-lookup"><span data-stu-id="c10cd-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="c10cd-148">Zie voor meer informatie [logboekregistratie in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="c10cd-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="c10cd-149">Voeg een **met** richtlijn voor bestand Microsoft.Extensions.Logging tooyour-service.</span><span class="sxs-lookup"><span data-stu-id="c10cd-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="c10cd-150">Definieer een persoonlijke variabele binnen uw serviceklasse.</span><span class="sxs-lookup"><span data-stu-id="c10cd-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="c10cd-151">Voeg deze code in Hallo constructor van uw serviceklasse:</span><span class="sxs-lookup"><span data-stu-id="c10cd-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="c10cd-152">Start uw code in uw methoden instrumenteren.</span><span class="sxs-lookup"><span data-stu-id="c10cd-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="c10cd-153">Hier volgen enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="c10cd-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="c10cd-154">Andere providers voor logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="c10cd-154">Using other logging providers</span></span>

<span data-ttu-id="c10cd-155">Sommige providers van derden gebruiken dat wordt beschreven in voorgaande sectie Hallo Hallo-benadering met inbegrip van [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), en [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="c10cd-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="c10cd-156">U kunt elk van deze in ASP.NET Core logboekregistratie aansluiten of u afzonderlijk kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c10cd-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="c10cd-157">Serilog bevat een functie waarmee alle berichten van een logboek verrijkt.</span><span class="sxs-lookup"><span data-stu-id="c10cd-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="c10cd-158">Deze functie kan worden nuttig toooutput Hallo service-naam, type en partitiegegevens.</span><span class="sxs-lookup"><span data-stu-id="c10cd-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="c10cd-159">toouse deze mogelijkheid in Hallo ASP.NET-infrastructuur, moet u deze stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c10cd-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="c10cd-160">Hallo Serilog, Serilog.Extensions.Logging, en Serilog.Sinks.Observable NuGet-pakketten toohello project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c10cd-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="c10cd-161">Voor het volgende voorbeeld hello, moet u ook Serilog.Sinks.Literate toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c10cd-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="c10cd-162">Een betere benadering wordt verderop in dit artikel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c10cd-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="c10cd-163">In Serilog, maakt u een LoggerConfiguration en Hallo berichtenlogboek-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c10cd-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="c10cd-164">Voeg een constructor Serilog.ILogger argument toohello service, en Hallo nieuw gemaakte berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="c10cd-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="c10cd-165">In Hallo service constructor toevoegen na de code die u Hallo eigenschap enrichers voor Hallo maakt Hallo **ServiceTypeName**, **ServiceName**, **PartitionId**, en  **InstanceId** eigenschappen van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c10cd-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="c10cd-166">Een eigenschap enricher toohello ASP.NET Core logboekregistratie factory, worden ook toegevoegd zodat u Microsoft.Extensions.Logging.ILogger in uw code gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="c10cd-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="c10cd-167">Instrument Hallo code Hallo hetzelfde als wanneer u ASP.NET Core zonder Serilog.</span><span class="sxs-lookup"><span data-stu-id="c10cd-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="c10cd-168">Het is raadzaam Hallo statisch gebruik geen Log.Logger Hello voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c10cd-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="c10cd-169">Service Fabric kan hosten meerdere exemplaren van Hallo dezelfde servicetype binnen een enkel proces.</span><span class="sxs-lookup"><span data-stu-id="c10cd-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="c10cd-170">Als u statische Log.Logger hello, Hallo laatste schrijver van Hallo eigenschap enrichers wordt weergegeven voor alle exemplaren die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c10cd-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="c10cd-171">Dit is een reden waarom Hallo _logger variabele persoonlijk lid van de serviceklasse Hallo wordt.</span><span class="sxs-lookup"><span data-stu-id="c10cd-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="c10cd-172">Zorg ook Hallo _logger beschikbaar toocommon code, die alle services kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c10cd-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="c10cd-173">Een provider logboekregistratie kiezen</span><span class="sxs-lookup"><span data-stu-id="c10cd-173">Choosing a logging provider</span></span>

<span data-ttu-id="c10cd-174">Als uw toepassing afhankelijk van hoge prestaties is, **EventSource** is meestal een goede benadering.</span><span class="sxs-lookup"><span data-stu-id="c10cd-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="c10cd-175">**EventSource** *doorgaans* minder bronnen gebruikt en beter presteert dan ASP.NET Core logboekregistratie of een van de oplossingen van derden beschikbaar van Hallo.</span><span class="sxs-lookup"><span data-stu-id="c10cd-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="c10cd-176">Dit is een probleem voor veel services, maar als uw service prestatiegerichte, met is niet **EventSource** mogelijk een betere keuze.</span><span class="sxs-lookup"><span data-stu-id="c10cd-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="c10cd-177">Echter, tooget deze voordelen van gestructureerde aan te melden, **EventSource** moet een grotere geïnvesteerd van het technische team.</span><span class="sxs-lookup"><span data-stu-id="c10cd-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="c10cd-178">Voer indien mogelijk een snelle prototype van een aantal logboekregistratieopties en kies vervolgens Hallo die het beste voldoet aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="c10cd-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c10cd-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c10cd-179">Next steps</span></span>

<span data-ttu-id="c10cd-180">Nadat u uw provider logboekregistratie tooinstrument uw toepassingen en services gekozen hebt, moeten uw logboeken en gebeurtenissen toobe geaggregeerd voordat ze kunnen worden verzonden tooany analysis platform.</span><span class="sxs-lookup"><span data-stu-id="c10cd-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="c10cd-181">Meer informatie over [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) en [af](service-fabric-diagnostics-event-aggregation-wad.md) toobetter weet Hallo aanbevolen opties.</span><span class="sxs-lookup"><span data-stu-id="c10cd-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
