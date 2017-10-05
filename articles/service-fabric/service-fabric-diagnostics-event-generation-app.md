---
title: Azure Service Fabric-toepassingsniveau bewaking | Microsoft Docs
description: Meer informatie over de toepassing en service level gebeurtenissen en logboeken die worden gebruikt om te bewaken en onderzoeken van Azure Service Fabric-clusters.
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
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="16d5a-103">Toepassing en service level genereren van gebeurtenis- en logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="16d5a-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="16d5a-104">De code met aangepaste gebeurtenissen instrumenteren</span><span class="sxs-lookup"><span data-stu-id="16d5a-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="16d5a-105">De code instrumenteren vormt de basis voor de meeste andere aspecten van de bewaking van uw services.</span><span class="sxs-lookup"><span data-stu-id="16d5a-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="16d5a-106">Instrumentatie is de enige manier kunt u weet dat er iets mis is, en op te sporen wat moet worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="16d5a-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="16d5a-107">Hoewel het is technisch mogelijk verbinding maken met een foutopsporingsprogramma een productieservice, maar het is niet een gangbare optie.</span><span class="sxs-lookup"><span data-stu-id="16d5a-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="16d5a-108">Dus is het belangrijk gedetailleerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="16d5a-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="16d5a-109">Sommige producten softwareontwikkelaars automatisch uw code.</span><span class="sxs-lookup"><span data-stu-id="16d5a-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="16d5a-110">Hoewel deze oplossingen goed werken kunnen, is bijna altijd handmatige instrumentation vereist.</span><span class="sxs-lookup"><span data-stu-id="16d5a-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="16d5a-111">U moet voldoende informatie voor foutopsporing van de toepassing volledig hebben in het einde.</span><span class="sxs-lookup"><span data-stu-id="16d5a-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="16d5a-112">Dit document beschrijft de verschillende methoden voor het instrumenteren van uw code en het kiezen van een methode op een andere.</span><span class="sxs-lookup"><span data-stu-id="16d5a-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="16d5a-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="16d5a-113">EventSource</span></span>
<span data-ttu-id="16d5a-114">Wanneer u een Service Fabric-oplossing van een sjabloon in Visual Studio maakt een **EventSource**-afgeleide klasse (**ServiceEventSource** of **ActorEventSource**) wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="16d5a-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="16d5a-115">Een sjabloon is gemaakt, waarin u de gebeurtenissen voor uw toepassing of service kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16d5a-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="16d5a-116">De **EventSource** naam **moet** uniek zijn en moet worden gewijzigd van de sjabloon standaardtekenreeks mijnbedrijf -&lt;oplossing&gt;-&lt;project&gt;.</span><span class="sxs-lookup"><span data-stu-id="16d5a-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="16d5a-117">Meerdere **EventSource** definities die dezelfde naam gebruiken voor een probleem zorgt tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="16d5a-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="16d5a-118">Elke gedefinieerde gebeurtenis moet een unieke id hebben.</span><span class="sxs-lookup"><span data-stu-id="16d5a-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="16d5a-119">Als een id is niet uniek is, treedt er een runtime-fout op.</span><span class="sxs-lookup"><span data-stu-id="16d5a-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="16d5a-120">Sommige organisaties preassign bereiken met waarden voor de id's voorkomen van conflicten tussen afzonderlijke ontwikkelteams.</span><span class="sxs-lookup"><span data-stu-id="16d5a-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="16d5a-121">Zie voor meer informatie [van Vance blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) of de [MSDN-documentatie](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="16d5a-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="16d5a-122">Het gebruik van gestructureerde EventSource gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="16d5a-122">Using structured EventSource events</span></span>

<span data-ttu-id="16d5a-123">Elk van de gebeurtenissen in de codevoorbeelden in deze sectie worden gedefinieerd voor een specifieke aanvraag, bijvoorbeeld wanneer een servicetype is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="16d5a-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="16d5a-124">Wanneer u berichten door gebruiksvoorbeeld definiëren, kunnen gegevens worden verpakt met de tekst van de fout en u meer kunt eenvoudig zoeken en filteren op basis van de namen of waarden van de opgegeven eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="16d5a-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="16d5a-125">Zorgt ervoor dat de uitvoer instrumentation structureren vereist gemakkelijker te gebruiken, maar meer gedachte en tijd voor het definiëren van een nieuwe gebeurtenis voor elke gebruiksvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="16d5a-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="16d5a-126">Sommige Gebeurtenisdefinities kunnen worden gedeeld door de gehele toepassing.</span><span class="sxs-lookup"><span data-stu-id="16d5a-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="16d5a-127">Bijvoorbeeld, een methode starten of stoppen zou gebeurtenis hele veel services in een toepassing worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="16d5a-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="16d5a-128">Een service, domeinspecifieke, zoals een systeem volgorde wellicht een **CreateOrder** gebeurtenis een eigen unieke gebeurtenis heeft.</span><span class="sxs-lookup"><span data-stu-id="16d5a-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="16d5a-129">Deze aanpak mogelijk veel gebeurtenissen genereren en mogelijk coördinatie vereisen van id's op projectteams.</span><span class="sxs-lookup"><span data-stu-id="16d5a-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="16d5a-130">EventSource gebruik algemeen</span><span class="sxs-lookup"><span data-stu-id="16d5a-130">Using EventSource generically</span></span>

<span data-ttu-id="16d5a-131">Omdat het definiëren van specifieke gebeurtenissen kan lastig zijn, definiëren veel mensen enkele gebeurtenissen met een gemeenschappelijke set parameters die in het algemeen hun informatie als een tekenreeks voeren.</span><span class="sxs-lookup"><span data-stu-id="16d5a-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="16d5a-132">Veel van de gestructureerde aspect gaat verloren en is het moeilijker om te zoeken en filteren van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="16d5a-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="16d5a-133">In deze methode voert worden enkele gebeurtenissen die meestal met de registratieniveaus overeen gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="16d5a-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="16d5a-134">Het volgende fragment definieert een bericht voor foutopsporing en de fout:</span><span class="sxs-lookup"><span data-stu-id="16d5a-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
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

<span data-ttu-id="16d5a-135">Een hybride van gestructureerde en algemene instrumentation kunt ook werken goed.</span><span class="sxs-lookup"><span data-stu-id="16d5a-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="16d5a-136">Gestructureerde instrumentation wordt gebruikt voor het melden van fouten en metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="16d5a-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="16d5a-137">Algemene gebeurtenissen kunnen worden gebruikt voor de gedetailleerde logboekregistratie die wordt gebruikt door engineers voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="16d5a-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="16d5a-138">ASP.NET Core logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="16d5a-138">ASP.NET Core logging</span></span>

<span data-ttu-id="16d5a-139">Het is belangrijk dat u zorgvuldig plannen hoe u uw code wordt instrumenteren.</span><span class="sxs-lookup"><span data-stu-id="16d5a-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="16d5a-140">Het plan rechts instrumentation kunt u mogelijk uw codebasis destabilizing en hoeven de code reinstrument voorkomen.</span><span class="sxs-lookup"><span data-stu-id="16d5a-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="16d5a-141">Om risico te beperken, kunt u een instrumentatiebiblotheek zoals [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), die deel uitmaakt van Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="16d5a-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="16d5a-142">ASP.NET Core is een [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface die u met de leverancier van uw keuze, gebruiken kunt terwijl het effect op de bestaande code worden geminimaliseerd.</span><span class="sxs-lookup"><span data-stu-id="16d5a-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="16d5a-143">U kunt de code in ASP.NET Core voor Windows en Linux, en in het volledige .NET Framework, zodat uw code instrumentation gestandaardiseerd.</span><span class="sxs-lookup"><span data-stu-id="16d5a-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="16d5a-144">Dit is meer verkend hieronder:</span><span class="sxs-lookup"><span data-stu-id="16d5a-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="16d5a-145">Met behulp van Microsoft.Extensions.Logging in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="16d5a-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="16d5a-146">Het Microsoft.Extensions.Logging NuGet-pakket aan het project dat u wilt toevoegen is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="16d5a-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="16d5a-147">Ook alle pakketten provider toe te voegen (Zie het volgende voorbeeld voor een pakket van derden).</span><span class="sxs-lookup"><span data-stu-id="16d5a-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="16d5a-148">Zie voor meer informatie [logboekregistratie in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="16d5a-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="16d5a-149">Voeg een **met** richtlijn voor Microsoft.Extensions.Logging in uw servicebestand.</span><span class="sxs-lookup"><span data-stu-id="16d5a-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="16d5a-150">Definieer een persoonlijke variabele binnen uw serviceklasse.</span><span class="sxs-lookup"><span data-stu-id="16d5a-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="16d5a-151">Voeg deze code in de constructor van uw serviceklasse:</span><span class="sxs-lookup"><span data-stu-id="16d5a-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="16d5a-152">Start uw code in uw methoden instrumenteren.</span><span class="sxs-lookup"><span data-stu-id="16d5a-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="16d5a-153">Hier volgen enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="16d5a-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="16d5a-154">Andere providers voor logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="16d5a-154">Using other logging providers</span></span>

<span data-ttu-id="16d5a-155">Sommige leveranciers gebruik de methode die wordt beschreven in de vorige sectie, inclusief [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), en [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="16d5a-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="16d5a-156">U kunt elk van deze in ASP.NET Core logboekregistratie aansluiten of u afzonderlijk kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16d5a-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="16d5a-157">Serilog bevat een functie waarmee alle berichten van een logboek verrijkt.</span><span class="sxs-lookup"><span data-stu-id="16d5a-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="16d5a-158">Deze functie kan nuttig zijn voor de servicenaam, het type en de partitiegegevens uitvoer.</span><span class="sxs-lookup"><span data-stu-id="16d5a-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="16d5a-159">Als u deze mogelijkheid in de infrastructuur van ASP.NET Core, voer deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="16d5a-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="16d5a-160">De Serilog Serilog.Extensions.Logging en Serilog.Sinks.Observable NuGet-pakketten toevoegen aan het project.</span><span class="sxs-lookup"><span data-stu-id="16d5a-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="16d5a-161">Voor het volgende voorbeeld moet u ook Serilog.Sinks.Literate toevoegen.</span><span class="sxs-lookup"><span data-stu-id="16d5a-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="16d5a-162">Een betere benadering wordt verderop in dit artikel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="16d5a-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="16d5a-163">In Serilog, maakt u een LoggerConfiguration en het exemplaar van het berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="16d5a-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="16d5a-164">Een argument Serilog.ILogger toevoegen aan de constructor service en de zojuist gemaakte berichtenlogboek doorgeven.</span><span class="sxs-lookup"><span data-stu-id="16d5a-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="16d5a-165">Voeg in de constructor service de volgende code, die wordt gemaakt van de eigenschap enrichers voor de **ServiceTypeName**, **ServiceName**, **PartitionId**, en **InstanceId** eigenschappen van de service.</span><span class="sxs-lookup"><span data-stu-id="16d5a-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="16d5a-166">Ook wordt toegevoegd een eigenschap enricher ASP.NET Core logboekregistratie fabriek, zodat u Microsoft.Extensions.Logging.ILogger in uw code gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="16d5a-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="16d5a-167">Softwareontwikkelaars de code hetzelfde als wanneer u ASP.NET Core zonder Serilog.</span><span class="sxs-lookup"><span data-stu-id="16d5a-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="16d5a-168">U wordt aangeraden dat u de statische Log.Logger niet met het voorgaande voorbeeld gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16d5a-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="16d5a-169">Service Fabric kunt meerdere exemplaren van hetzelfde servicetype binnen een enkel proces hosten.</span><span class="sxs-lookup"><span data-stu-id="16d5a-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="16d5a-170">Als u de statische Log.Logger gebruikt, ziet de laatste schrijver van de eigenschap enrichers waarden voor alle exemplaren die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16d5a-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="16d5a-171">Dit is een reden waarom de variabele _logger een variabele persoonlijk lid van de serviceklasse.</span><span class="sxs-lookup"><span data-stu-id="16d5a-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="16d5a-172">Bovendien moet u de _logger beschikbaar is voor algemene code, die kan worden gebruikt op services.</span><span class="sxs-lookup"><span data-stu-id="16d5a-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="16d5a-173">Een provider logboekregistratie kiezen</span><span class="sxs-lookup"><span data-stu-id="16d5a-173">Choosing a logging provider</span></span>

<span data-ttu-id="16d5a-174">Als uw toepassing afhankelijk van hoge prestaties is, **EventSource** is meestal een goede benadering.</span><span class="sxs-lookup"><span data-stu-id="16d5a-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="16d5a-175">**EventSource** *doorgaans* minder bronnen gebruikt en beter presteert dan ASP.NET Core logboekregistratie of een van de beschikbare oplossingen van derden.</span><span class="sxs-lookup"><span data-stu-id="16d5a-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="16d5a-176">Dit is een probleem voor veel services, maar als uw service prestatiegerichte, met is niet **EventSource** mogelijk een betere keuze.</span><span class="sxs-lookup"><span data-stu-id="16d5a-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="16d5a-177">Gestructureerde echter ophalen van deze voordelen van logboekregistratie, **EventSource** moet een grotere geïnvesteerd van het technische team.</span><span class="sxs-lookup"><span data-stu-id="16d5a-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="16d5a-178">Indien mogelijk een snelle prototype van een aantal logboekregistratieopties doen en kies vervolgens die het beste voldoet aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="16d5a-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16d5a-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16d5a-179">Next steps</span></span>

<span data-ttu-id="16d5a-180">Nadat u ervoor uw provider logboekregistratie gekozen hebt softwareontwikkelaars uw toepassingen en services, moeten uw logboeken en gebeurtenissen worden geaggregeerd voordat ze kunnen worden verzonden naar een willekeurig platform analyse.</span><span class="sxs-lookup"><span data-stu-id="16d5a-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="16d5a-181">Meer informatie over [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) en [af](service-fabric-diagnostics-event-aggregation-wad.md) om enkele van de aanbevolen opties beter te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="16d5a-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
