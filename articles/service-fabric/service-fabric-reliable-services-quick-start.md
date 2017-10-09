---
title: aaaCreate uw eerste Service Fabric-toepassing in C# | Microsoft Docs
description: Inleiding toocreating een Microsoft Azure Service Fabric-toepassing met staatloze en stateful services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="cc7cb-103">Aan de slag met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cc7cb-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc7cb-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="cc7cb-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="cc7cb-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="cc7cb-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="cc7cb-106">Een Azure Service Fabric-toepassing bevat een of meer services waarop uw code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="cc7cb-107">Deze handleiding ontdekt u hoe toocreate staatloze en stateful Service Fabric-toepassingen met [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc7cb-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="cc7cb-108">Deze Microsoft Virtual Academy video ook ziet u hoe toocreate een stateless betrouwbare service:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="cc7cb-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="cc7cb-109">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="cc7cb-109">Basic concepts</span></span>
<span data-ttu-id="cc7cb-110">de slag met Reliable Services, u alleen tooget moet toounderstand enkele basisbeginselen:</span><span class="sxs-lookup"><span data-stu-id="cc7cb-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="cc7cb-111">**Servicetype**: dit is uw service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="cc7cb-112">Dit is gedefinieerd door u schrijft Hallo-klasse die uitgebreider is dan `StatelessService` en andere code of afhankelijkheden gebruikt, samen met een naam en een uniek versienummer.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="cc7cb-113">**Service-exemplaar met de naam**: toorun uw service u maakt benoemde exemplaren van het servicetype veel zoals u instanties van objecten van het type van een klasse maken.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="cc7cb-114">Een service-exemplaar heeft een naam in de vorm van een URI met Hallo Hallo "fabric: / ' schema, zoals" fabric: / MyApp/MijnService '.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="cc7cb-115">**ServiceHost**: Hallo service-exemplaren maken van toorun moet binnen een hostproces verstrekt met de naam.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="cc7cb-116">Hallo ServiceHost is alleen een proces waarbij exemplaren van de service kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="cc7cb-117">**Service-registratie**: inschrijving brengt alles bij elkaar.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="cc7cb-118">Hallo servicetype moet zijn geregistreerd met Hallo Service Fabric runtime in een service hosten tooallow Service Fabric toocreate exemplaren van deze toorun.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="cc7cb-119">Een stateless service maken</span><span class="sxs-lookup"><span data-stu-id="cc7cb-119">Create a stateless service</span></span>
<span data-ttu-id="cc7cb-120">Een stateless service is een type service dat momenteel is Hallo-norm in de cloud-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="cc7cb-121">Dit wordt beschouwd als staatloze omdat Hallo-service zelf bevat geen gegevens die moeten worden toobe betrouwbaar opgeslagen of maximaal beschikbaar is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="cc7cb-122">Als u een exemplaar van een staatloze service wordt afgesloten, is alle van de interne status verloren.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="cc7cb-123">In dit type van service status persistente tooan externe winkel, zoals Azure-tabellen of een SQL-database, moet voor deze toobe maximaal beschikbare en betrouwbare aangebracht.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="cc7cb-124">Start Visual Studio 2015 of Visual Studio 2017 als beheerder en maak een nieuwe Service Fabric-toepassingsproject met de naam *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="cc7cb-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Hallo nieuw Project dialoogvenster vak toocreate een nieuwe Service Fabric-toepassing gebruiken](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="cc7cb-126">Maak vervolgens een stateless service-project met de naam *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="cc7cb-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Hallo tweede in het dialoogvenster een stateless serviceproject maken](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="cc7cb-128">Uw oplossing bevat nu twee projecten:</span><span class="sxs-lookup"><span data-stu-id="cc7cb-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="cc7cb-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-129">*HelloWorld*.</span></span> <span data-ttu-id="cc7cb-130">Dit is Hallo *toepassing* project met uw *services*.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="cc7cb-131">Het bevat ook Hallo-toepassingsmanifest die worden beschreven toepassing hello, evenals een aantal PowerShell-scripts waarmee u toodeploy uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="cc7cb-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="cc7cb-133">Dit is het serviceproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-133">This is hello service project.</span></span> <span data-ttu-id="cc7cb-134">Het bevat Hallo-implementatie voor stateless service.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="cc7cb-135">Hallo service implementeren</span><span class="sxs-lookup"><span data-stu-id="cc7cb-135">Implement hello service</span></span>
<span data-ttu-id="cc7cb-136">Open Hallo **HelloWorldStateless.cs** bestand in Hallo serviceproject.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="cc7cb-137">Een service kunt eventuele bedrijfslogica uitvoeren in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="cc7cb-138">Hallo service API biedt twee toegangspunten voor uw code:</span><span class="sxs-lookup"><span data-stu-id="cc7cb-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="cc7cb-139">Een methode met een vermelding point, aangeroepen *RunAsync*, waar u kunt beginnen alle werkbelastingen, met inbegrip van langlopende compute-workloads uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="cc7cb-140">Een communicatie-ingangspunt waar u uw communicatiestack keuze, zoals ASP.NET Core kunt aansluiten.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="cc7cb-141">Dit is waar u ontvangen van aanvragen van gebruikers en andere services kan starten.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="cc7cb-142">In deze zelfstudie gaan we in op Hallo `RunAsync()` entry point-methode.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="cc7cb-143">Dit is waar u kunt onmiddellijk starten uitvoeren van uw code.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="cc7cb-144">Hallo-projectsjabloon bevat een Voorbeeldimplementatie van `RunAsync()` die een aantal rolling verhoogd.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="cc7cb-145">Zie voor meer informatie over hoe toowork met een mededeling stack [Service Fabric-Web-API-services met OWIN zelf die als host fungeert](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="cc7cb-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="cc7cb-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="cc7cb-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="cc7cb-147">Hallo platform roept deze methode wanneer u een exemplaar van een service wordt geplaatst en zijn ze klaar tooexecute.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="cc7cb-148">Voor een stateless service betekent dat gewoon wanneer Hallo service-exemplaar wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="cc7cb-149">Een token annulering wordt toocoordinate opgegeven als uw service-exemplaar toobe gesloten moet.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="cc7cb-150">Deze cyclus openen en sluiten van een service-exemplaar kan in Service Fabric vaak tijdens Hallo-levensduur van Hallo service optreden als geheel.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="cc7cb-151">Dit kan gebeuren om verschillende redenen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="cc7cb-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="cc7cb-152">Hallo-systeem wordt uw service-exemplaren voor resourceverdeling verplaatst.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="cc7cb-153">Fouten die voorkomen in uw code.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-153">Faults occur in your code.</span></span>
* <span data-ttu-id="cc7cb-154">Hallo toepassings- of upgrade.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="cc7cb-155">de onderliggende hardware Hallo optreedt een storing.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="cc7cb-156">Deze indeling wordt beheerd door Hallo system tookeep uw service maximaal beschikbaar is en goed taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="cc7cb-157">`RunAsync()`moet niet synchroon blokkeren.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="cc7cb-158">De implementatie van RunAsync moet een taak retourneren of op alle bewerkingen langlopende of blokkeringen tooallow Hallo runtime toocontinue await.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="cc7cb-159">Let op Hallo `while(true)` lus in het vorige voorbeeld hello, een taak retourneren `await Task.Delay()` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="cc7cb-160">Als uw werkbelasting synchroon blokkeert moet, moet u een nieuwe taak plannen `Task.Run()` in uw `RunAsync` implementatie.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="cc7cb-161">Annulering van uw werkbelasting is een gezamenlijke inspanning gedirigeerd door Hallo annulering token opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="cc7cb-162">Hallo systeem wacht tot de taak tooend (door met succes is voltooid, geannuleerd of fault) voordat het wordt verplaatst op.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="cc7cb-163">Het is belangrijk toohonor Hallo annulering token, voltooien een werken en af te sluiten `RunAsync()` zo snel mogelijk wanneer Hallo system annulering aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="cc7cb-164">In dit voorbeeld staatloze service wordt Hallo count opgeslagen in een lokale variabele.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="cc7cb-165">Maar omdat dit een stateless service, Hallo-waarde die opgeslagen bestaat alleen voor de huidige levenscyclus Hallo van de service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="cc7cb-166">Wanneer Hallo-service wordt verplaatst of opnieuw wordt opgestart, is Hallo-waarde verloren gegaan.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="cc7cb-167">Een stateful service maken</span><span class="sxs-lookup"><span data-stu-id="cc7cb-167">Create a stateful service</span></span>
<span data-ttu-id="cc7cb-168">Service Fabric introduceert een nieuw soort stateful service.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="cc7cb-169">Een stateful service te onderhouden op betrouwbare wijze binnen het Hallo-service zelf, CO-locaties met Hallo-code die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="cc7cb-170">Status is maximaal beschikbaar is gemaakt door de Service Fabric zonder Hallo nodig toopersist status tooan externe winkel.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="cc7cb-171">een waarde van het prestatiemeteritem van staatloze toohighly beschikbaar is en permanente tooconvert, zelfs wanneer het Hallo-service is verplaatst of opnieuw is opgestart, moet u een stateful service.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="cc7cb-172">Hallo in dezelfde *HelloWorld* toepassing, kunt u een nieuwe service toevoegen door met de rechtermuisknop op Hallo Services verwijzingen in Hallo toepassingsproject en selecteren **toevoegen -> nieuwe Service Fabric-Service**.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Een service tooyour Service Fabric-toepassing toevoegen](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="cc7cb-174">Selecteer **Stateful Service** en noem deze *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="cc7cb-175">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-175">Click **OK**.</span></span>

![Hallo nieuw Project dialoogvenster vak toocreate een nieuwe stateful Service Fabric-service gebruiken](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="cc7cb-177">Uw toepassing hebt nu twee services: Hallo staatloze service *HelloWorldStateless* en stateful service Hallo *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="cc7cb-178">Een stateful service Hallo heeft dezelfde toegangspunten als een stateless service.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="cc7cb-179">het belangrijkste verschil Hallo is Hallo beschikbaarheid van een *state-provider* die de status op betrouwbare wijze kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="cc7cb-180">Service Fabric wordt geleverd met een implementatie van de persistentieprovider status aangeroepen [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md), waarmee u gerepliceerde gegevensstructuren via Hallo betrouwbare status Manager maken.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="cc7cb-181">Een stateful betrouwbare Service maakt standaard gebruik van deze state-provider.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="cc7cb-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, die Hallo RunAsync-methode volgende bevat:</span><span class="sxs-lookup"><span data-stu-id="cc7cb-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="cc7cb-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="cc7cb-183">RunAsync</span></span>
<span data-ttu-id="cc7cb-184">`RunAsync()`draait op dezelfde manier in stateful en staatloze services.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="cc7cb-185">Echter in een stateful service Hallo platform extra werk uitvoert namens jou voordat deze wordt uitgevoerd `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="cc7cb-186">Deze taak kunt opnemen ervoor te zorgen dat Hallo betrouwbare statusbeheer en betrouwbare verzamelingen toouse gereed zijn.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="cc7cb-187">Betrouwbare verzamelingen en Hallo betrouwbare statusbeheer</span><span class="sxs-lookup"><span data-stu-id="cc7cb-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="cc7cb-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is de implementatie van een woordenlijst waarmee u de archiefstatus tooreliably in Hallo-service kunt.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="cc7cb-189">Met Service Fabric en betrouwbare verzamelingen, kunt u gegevens opslaan rechtstreeks in uw service zonder Hallo nodig is voor een externe permanente archief.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="cc7cb-190">Betrouwbare verzamelingen uw gegevens maximaal beschikbaar maken.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="cc7cb-191">Service Fabric bewerkstelligt dit door het maken en beheren van meerdere *replica's* van uw service voor u.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="cc7cb-192">Het bevat ook een API die de complexiteit van het beheer van deze replica's en hun statusovergangen opslag Hallo isoleert.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="cc7cb-193">Betrouwbare verzamelingen kunnen elk type .NET, met inbegrip van uw aangepaste typen, met een aantal aanvullende opmerkingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="cc7cb-194">Service Fabric worden uw status maximaal beschikbaar door *repliceren* staat tussen knooppunten en betrouwbare verzamelingen uw toolocal gegevensschijf opslaan op elke replica.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="cc7cb-195">Dit betekent dat alles dat is opgeslagen in betrouwbare verzamelingen moet *serialiseerbaar*.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="cc7cb-196">Standaard gebruik van betrouwbare verzamelingen [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) voor serialisatie, dus is het belangrijk ervoor dat uw typen toomake [ondersteund door de serialisatiefunctie van het gegevenscontract Hallo](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) wanneer u Hallo standaardwaarde gebruiken serializer.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="cc7cb-197">Objecten worden gerepliceerd voor hoge beschikbaarheid, wanneer u transacties op betrouwbare verzamelingen doorvoert.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="cc7cb-198">Objecten die zijn opgeslagen in betrouwbare verzamelingen worden opgeslagen in het lokale geheugen van uw service.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="cc7cb-199">Dit betekent dat u een lokale toohello referentieobject hebt.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="cc7cb-200">Het is belangrijk dat u geen lokale exemplaren van deze objecten muteren zonder dat er een updatebewerking op Hallo betrouwbare verzameling in een transactie.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="cc7cb-201">Dit is omdat wijzigingen toolocal exemplaren van objecten worden niet automatisch worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="cc7cb-202">U moet steek deze opnieuw Hallo object weer in de woordenlijst Hallo of gebruik een van de Hallo *bijwerken* methoden op Hallo woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="cc7cb-203">Hallo betrouwbare status Manager beheert betrouwbare verzamelingen voor u.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="cc7cb-204">U kunt gewoon vragen Hallo betrouwbare status Manager voor een betrouwbare verzameling met de naam op elk gewenst moment en op een willekeurige plaats in uw service.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="cc7cb-205">Hallo betrouwbare status Manager zorgt ervoor dat u een verwijzing terug.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="cc7cb-206">We raadzaam niet op te slaan verwijzingen tooreliable verzameling exemplaren in Klassenlidvariabelen of eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="cc7cb-207">Speciale Wees voorzichtig tooensure die Hallo verwijzing ingesteld tooan exemplaar te allen tijde in Hallo service lifecycle.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="cc7cb-208">Hallo betrouwbare statusbeheer dit werk voor u verwerkt en geoptimaliseerd voor herhaaldelijk bezoeken.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="cc7cb-209">Transactionele en asynchrone bewerkingen</span><span class="sxs-lookup"><span data-stu-id="cc7cb-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="cc7cb-210">Betrouwbare verzamelingen hebben veel Hallo dezelfde bewerkingen die hun `System.Collections.Generic` en `System.Collections.Concurrent` collega's doen, met uitzondering van LINQ.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="cc7cb-211">Bewerkingen op betrouwbare verzamelingen zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="cc7cb-212">Dit is omdat schrijfbewerkingen met betrouwbare verzamelingen tooreplicate van i/o-bewerkingen uitvoeren, zodat gegevens toodisk behouden blijven.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="cc7cb-213">Betrouwbare verzameling bewerkingen zijn *transactionele*, zodat u status consistent voor meerdere betrouwbare verzamelingen en bewerkingen houden kunt.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="cc7cb-214">U kunt bijvoorbeeld een werkitem van een betrouwbare wachtrij in wachtrij, een bewerking uitvoeren op deze en Hallo resultaat opslaan in een betrouwbare woordenlijst alle binnen een transactie.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="cc7cb-215">Dit wordt beschouwd als een atomic-bewerking en dit zorgt ervoor dat de hele bewerking Hallo slaagt of Hallo hele bewerking wordt teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="cc7cb-216">Als een fout optreedt nadat u uit de wachtrij Hallo item halen maar voordat u Hallo resultaat opslaat, Hallo hele transactie wordt teruggedraaid en Hallo item blijft in Hallo wachtrij voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="cc7cb-217">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="cc7cb-217">Run hello application</span></span>
<span data-ttu-id="cc7cb-218">Nu wordt teruggeplaatst toohello *HelloWorld* toepassing.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="cc7cb-219">U kunt nu bouwen en implementeren van uw services.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-219">You can now build and deploy your services.</span></span> <span data-ttu-id="cc7cb-220">Wanneer u drukt op **F5**, uw toepassing worden gebouwd en geïmplementeerde tooyour lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="cc7cb-221">Nadat Hallo-services uitgevoerd worden gestart, kunt u weergeven Hallo gegenereerd Event Tracing voor Windows (ETW) gebeurtenissen in een **diagnostische gebeurtenissen** venster.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="cc7cb-222">Merk op dat Hallo gebeurtenissen weergegeven uit Hallo staatloze service en Hallo stateful service in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="cc7cb-223">U kunt Hallo stroom onderbreken door te klikken op Hallo **onderbreken** knop.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="cc7cb-224">U kunt vervolgens Hallo details van een bericht controleren door het uitbreiden van dat bericht.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="cc7cb-225">Voordat u de toepassing hello uitvoert, zorg ervoor dat er een lokaal ontwikkelcluster uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="cc7cb-226">Bekijk Hallo [instructiehandleiding](service-fabric-get-started.md) voor informatie over het instellen van uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="cc7cb-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Diagnostische gebeurtenissen weergeven in Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="cc7cb-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc7cb-228">Next steps</span></span>
[<span data-ttu-id="cc7cb-229">Fouten opsporen in uw Service Fabric-toepassing in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc7cb-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="cc7cb-230">Aan de slag: Service Fabric-Web-API-services met OWIN zelf die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="cc7cb-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="cc7cb-231">Meer informatie over betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="cc7cb-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="cc7cb-232">Een toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="cc7cb-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="cc7cb-233">Upgrade van de toepassing</span><span class="sxs-lookup"><span data-stu-id="cc7cb-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="cc7cb-234">Referentie voor ontwikkelaars voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cc7cb-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

