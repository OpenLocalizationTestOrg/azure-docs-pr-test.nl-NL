---
title: Uw eerste Service Fabric-toepassing maken in C# | Microsoft Docs
description: Inleiding tot het maken van een Microsoft Azure Service Fabric-toepassing met staatloze en stateful services.
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
ms.openlocfilehash: 813021d6239ae3cf79bb84b78f77e39c9e0783f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="c307e-103">Aan de slag met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c307e-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c307e-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="c307e-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="c307e-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="c307e-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="c307e-106">Een Azure Service Fabric-toepassing bevat een of meer services waarop uw code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c307e-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="c307e-107">Deze handleiding wordt beschreven hoe u maakt zowel stateless als stateful Service Fabric-toepassingen met [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c307e-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="c307e-108">Deze video Microsoft Virtual Academy leest u hoe u een stateless betrouwbare service maken:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="c307e-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="c307e-109">Basisconcepten</span><span class="sxs-lookup"><span data-stu-id="c307e-109">Basic concepts</span></span>
<span data-ttu-id="c307e-110">Om aan de slag met Reliable Services, moet u slechts enkele basisbeginselen begrijpen:</span><span class="sxs-lookup"><span data-stu-id="c307e-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="c307e-111">**Servicetype**: dit is uw service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c307e-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="c307e-112">Dit is gedefinieerd door de klasse u schrijven die uitgebreider is dan `StatelessService` en andere code of afhankelijkheden gebruikt, samen met een naam en een uniek versienummer.</span><span class="sxs-lookup"><span data-stu-id="c307e-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="c307e-113">**Service-exemplaar met de naam**: voor het uitvoeren van uw service, u maakt benoemde exemplaren van het servicetype veel zoals u instanties van objecten van het type van een klasse maken.</span><span class="sxs-lookup"><span data-stu-id="c307e-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="c307e-114">Een service-exemplaar heeft een naam in de vorm van een URI met de "fabric: / ' schema, zoals" fabric: / MyApp/MijnService '.</span><span class="sxs-lookup"><span data-stu-id="c307e-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="c307e-115">**ServiceHost**: de benoemde service-exemplaren die u maakt moeten uitvoeren in een hostproces.</span><span class="sxs-lookup"><span data-stu-id="c307e-115">**Service host**: The named service instances you create need to run inside a host process.</span></span> <span data-ttu-id="c307e-116">De ServiceHost is alleen een proces waarbij exemplaren van de service kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c307e-116">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="c307e-117">**Service-registratie**: inschrijving brengt alles bij elkaar.</span><span class="sxs-lookup"><span data-stu-id="c307e-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="c307e-118">Type van de service moet zijn geregistreerd met de Service Fabric-runtime in een ServiceHost om toe te staan van Service Fabric om exemplaren van deze te maken om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c307e-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="c307e-119">Een stateless service maken</span><span class="sxs-lookup"><span data-stu-id="c307e-119">Create a stateless service</span></span>
<span data-ttu-id="c307e-120">Een stateless service is een type service dat momenteel is de norm in de cloud-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c307e-120">A stateless service is a type of service that is currently the norm in cloud applications.</span></span> <span data-ttu-id="c307e-121">Dit wordt beschouwd als staatloze omdat de service zelf bevat geen gegevens die moet worden opgeslagen op betrouwbare wijze of maximaal beschikbaar is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c307e-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span></span> <span data-ttu-id="c307e-122">Als u een exemplaar van een staatloze service wordt afgesloten, is alle van de interne status verloren.</span><span class="sxs-lookup"><span data-stu-id="c307e-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="c307e-123">In dit type van de service moet status worden opgeslagen op een externe winkel, zoals Azure-tabellen of een SQL-database voor de maximaal beschikbare en betrouwbare worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c307e-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span></span>

<span data-ttu-id="c307e-124">Start Visual Studio 2015 of Visual Studio 2017 als beheerder en maak een nieuwe Service Fabric-toepassingsproject met de naam *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="c307e-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Gebruik het dialoogvenster Nieuw Project voor het maken van een nieuwe Service Fabric-toepassing](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="c307e-126">Maak vervolgens een stateless service-project met de naam *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="c307e-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Klik in het dialoogvenster tweede een stateless serviceproject maken](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="c307e-128">Uw oplossing bevat nu twee projecten:</span><span class="sxs-lookup"><span data-stu-id="c307e-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="c307e-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="c307e-129">*HelloWorld*.</span></span> <span data-ttu-id="c307e-130">Dit is de *toepassing* project met uw *services*.</span><span class="sxs-lookup"><span data-stu-id="c307e-130">This is the *application* project that contains your *services*.</span></span> <span data-ttu-id="c307e-131">Het bevat ook het toepassingsmanifest die worden beschreven van de toepassing, evenals een aantal PowerShell-scripts die u helpen bij het implementeren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="c307e-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span></span>
* <span data-ttu-id="c307e-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="c307e-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="c307e-133">Dit is het serviceproject.</span><span class="sxs-lookup"><span data-stu-id="c307e-133">This is the service project.</span></span> <span data-ttu-id="c307e-134">Het bevat de staatloze service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c307e-134">It contains the stateless service implementation.</span></span>

## <a name="implement-the-service"></a><span data-ttu-id="c307e-135">De service implementeren</span><span class="sxs-lookup"><span data-stu-id="c307e-135">Implement the service</span></span>
<span data-ttu-id="c307e-136">Open de **HelloWorldStateless.cs** bestand in de serviceproject.</span><span class="sxs-lookup"><span data-stu-id="c307e-136">Open the **HelloWorldStateless.cs** file in the service project.</span></span> <span data-ttu-id="c307e-137">Een service kunt eventuele bedrijfslogica uitvoeren in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c307e-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="c307e-138">De service-API biedt twee toegangspunten voor uw code:</span><span class="sxs-lookup"><span data-stu-id="c307e-138">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="c307e-139">Een methode met een vermelding point, aangeroepen *RunAsync*, waar u kunt beginnen alle werkbelastingen, met inbegrip van langlopende compute-workloads uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c307e-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="c307e-140">Een communicatie-ingangspunt waar u uw communicatiestack keuze, zoals ASP.NET Core kunt aansluiten.</span><span class="sxs-lookup"><span data-stu-id="c307e-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="c307e-141">Dit is waar u ontvangen van aanvragen van gebruikers en andere services kan starten.</span><span class="sxs-lookup"><span data-stu-id="c307e-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="c307e-142">In deze zelfstudie gaan we in op de `RunAsync()` entry point-methode.</span><span class="sxs-lookup"><span data-stu-id="c307e-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span></span> <span data-ttu-id="c307e-143">Dit is waar u kunt onmiddellijk starten uitvoeren van uw code.</span><span class="sxs-lookup"><span data-stu-id="c307e-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="c307e-144">De projectsjabloon bevat een Voorbeeldimplementatie van `RunAsync()` die een aantal rolling verhoogd.</span><span class="sxs-lookup"><span data-stu-id="c307e-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="c307e-145">Zie voor meer informatie over het werken met een communicatiestack [Service Fabric-Web-API-services met OWIN zelf die als host fungeert](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="c307e-145">For details about how to work with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="c307e-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="c307e-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

<span data-ttu-id="c307e-147">Het platform roept deze methode wanneer een exemplaar van een service is geplaatst en kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c307e-147">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="c307e-148">Voor een stateless service betekent dat gewoon wanneer het service-exemplaar wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c307e-148">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="c307e-149">Een token annulering is opgegeven voor het coördineren van wanneer uw service-exemplaar moet worden gesloten.</span><span class="sxs-lookup"><span data-stu-id="c307e-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="c307e-150">Deze cyclus openen en sluiten van een service-exemplaar kan vaak gedurende de levensduur van de service in Service Fabric optreden als geheel.</span><span class="sxs-lookup"><span data-stu-id="c307e-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="c307e-151">Dit kan gebeuren om verschillende redenen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="c307e-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="c307e-152">Het systeem wordt uw service-exemplaren voor resourceverdeling verplaatst.</span><span class="sxs-lookup"><span data-stu-id="c307e-152">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="c307e-153">Fouten die voorkomen in uw code.</span><span class="sxs-lookup"><span data-stu-id="c307e-153">Faults occur in your code.</span></span>
* <span data-ttu-id="c307e-154">De toepassing of het systeem is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c307e-154">The application or system is upgraded.</span></span>
* <span data-ttu-id="c307e-155">De onderliggende hardware optreedt een storing.</span><span class="sxs-lookup"><span data-stu-id="c307e-155">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="c307e-156">Deze indeling wordt beheerd door het systeem te houden van uw service maximaal beschikbaar is en goed taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="c307e-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="c307e-157">`RunAsync()`moet niet synchroon blokkeren.</span><span class="sxs-lookup"><span data-stu-id="c307e-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="c307e-158">De implementatie van RunAsync moet een taak retourneren of await op langlopende of blokkeringen bewerkingen waarmee de runtime om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="c307e-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span></span> <span data-ttu-id="c307e-159">Houd er rekening mee de `while(true)` lus in het vorige voorbeeld wordt een taak retourneren `await Task.Delay()` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c307e-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="c307e-160">Als uw werkbelasting synchroon blokkeert moet, moet u een nieuwe taak plannen `Task.Run()` in uw `RunAsync` implementatie.</span><span class="sxs-lookup"><span data-stu-id="c307e-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="c307e-161">Annulering van uw werkbelasting is een gezamenlijke inspanning gedirigeerd door het token opgegeven annulering.</span><span class="sxs-lookup"><span data-stu-id="c307e-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="c307e-162">Het systeem wacht tot de taak te beëindigen (met succes is voltooid, annulering of fault) voordat het wordt verplaatst op.</span><span class="sxs-lookup"><span data-stu-id="c307e-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="c307e-163">Het is belangrijk om te voldoen aan het token annulering, werk voltooien en af te sluiten `RunAsync()` zo snel mogelijk wanneer het systeem annulering aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="c307e-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span></span>

<span data-ttu-id="c307e-164">In dit voorbeeld staatloze service wordt het aantal opgeslagen in een lokale variabele.</span><span class="sxs-lookup"><span data-stu-id="c307e-164">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="c307e-165">Maar omdat dit een stateless service, de waarde die opgeslagen bestaat alleen voor de huidige levenscyclus van de service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c307e-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="c307e-166">Wanneer de service wordt verplaatst of opnieuw wordt opgestart, wordt de waarde is verloren gegaan.</span><span class="sxs-lookup"><span data-stu-id="c307e-166">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="c307e-167">Een stateful service maken</span><span class="sxs-lookup"><span data-stu-id="c307e-167">Create a stateful service</span></span>
<span data-ttu-id="c307e-168">Service Fabric introduceert een nieuw soort stateful service.</span><span class="sxs-lookup"><span data-stu-id="c307e-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="c307e-169">Een stateful service te onderhouden op betrouwbare wijze binnen de service zelf, dezelfde locatie bevindt als de code die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c307e-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="c307e-170">Status is maximaal beschikbaar is gemaakt door de Service Fabric zonder de noodzaak om vast te leggen van de status van een externe winkel.</span><span class="sxs-lookup"><span data-stu-id="c307e-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="c307e-171">Een waarde van het prestatiemeteritem van staatloze conversie naar maximaal beschikbare en permanente, zelfs wanneer de service wordt verplaatst of opnieuw wordt opgestart, moet u een stateful service.</span><span class="sxs-lookup"><span data-stu-id="c307e-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="c307e-172">In dezelfde *HelloWorld* toepassing, kunt u een nieuwe service toevoegen door met de verwijzingen in het project voor een toepassing met de rechtermuisknop op de Services en **toevoegen -> nieuwe Service Fabric-Service**.</span><span class="sxs-lookup"><span data-stu-id="c307e-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Een service aan uw Service Fabric-toepassing toevoegen](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="c307e-174">Selecteer **Stateful Service** en noem deze *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="c307e-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="c307e-175">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c307e-175">Click **OK**.</span></span>

![Gebruik het dialoogvenster Nieuw Project voor het maken van een nieuwe stateful Service Fabric-service](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="c307e-177">Uw toepassing hebt nu twee services: de staatloze service *HelloWorldStateless* en de stateful service *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="c307e-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="c307e-178">Een stateful service heeft de dezelfde toegangspunten als een stateless service.</span><span class="sxs-lookup"><span data-stu-id="c307e-178">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="c307e-179">Het belangrijkste verschil is de beschikbaarheid van een *state-provider* die de status op betrouwbare wijze kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="c307e-179">The main difference is the availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="c307e-180">Service Fabric wordt geleverd met een implementatie van de persistentieprovider status aangeroepen [betrouwbare verzamelingen](service-fabric-reliable-services-reliable-collections.md), dit kunt u gegevensstructuren via statusbeheer voor het betrouwbare gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="c307e-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="c307e-181">Een stateful betrouwbare Service maakt standaard gebruik van deze state-provider.</span><span class="sxs-lookup"><span data-stu-id="c307e-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="c307e-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, die de volgende RunAsync-methode bevat:</span><span class="sxs-lookup"><span data-stu-id="c307e-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="c307e-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="c307e-183">RunAsync</span></span>
<span data-ttu-id="c307e-184">`RunAsync()`draait op dezelfde manier in stateful en staatloze services.</span><span class="sxs-lookup"><span data-stu-id="c307e-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="c307e-185">Echter, in een stateful service het platform extra werk uitvoert namens jou voordat deze wordt uitgevoerd `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c307e-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="c307e-186">Deze taak kunt opnemen ervoor te zorgen dat de betrouwbare statusbeheer en betrouwbare verzamelingen klaar zijn voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="c307e-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="c307e-187">Betrouwbare verzamelingen en de betrouwbare status Manager</span><span class="sxs-lookup"><span data-stu-id="c307e-187">Reliable Collections and the Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="c307e-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is een dictionary-implementatie die u gebruiken kunt om op te slaan op betrouwbare wijze staat in de service.</span><span class="sxs-lookup"><span data-stu-id="c307e-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="c307e-189">Met Service Fabric en betrouwbare verzamelingen, kunt u gegevens opslaan rechtstreeks in uw service zonder de noodzaak van een externe permanente archief.</span><span class="sxs-lookup"><span data-stu-id="c307e-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="c307e-190">Betrouwbare verzamelingen uw gegevens maximaal beschikbaar maken.</span><span class="sxs-lookup"><span data-stu-id="c307e-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="c307e-191">Service Fabric bewerkstelligt dit door het maken en beheren van meerdere *replica's* van uw service voor u.</span><span class="sxs-lookup"><span data-stu-id="c307e-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="c307e-192">Het bevat ook een API die weg de complexiteit isoleert van het beheren van deze replica's en hun statusovergangen.</span><span class="sxs-lookup"><span data-stu-id="c307e-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="c307e-193">Betrouwbare verzamelingen kunnen elk type .NET, met inbegrip van uw aangepaste typen, met een aantal aanvullende opmerkingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c307e-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="c307e-194">Service Fabric worden uw status maximaal beschikbaar door *repliceren* staat tussen knooppunten en betrouwbare verzamelingen opslaan van gegevens naar de lokale schijf op elke replica.</span><span class="sxs-lookup"><span data-stu-id="c307e-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span></span> <span data-ttu-id="c307e-195">Dit betekent dat alles dat is opgeslagen in betrouwbare verzamelingen moet *serialiseerbaar*.</span><span class="sxs-lookup"><span data-stu-id="c307e-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="c307e-196">Standaard gebruik van betrouwbare verzamelingen [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) voor serialisatie, dus is het belangrijk om ervoor te zorgen dat uw typen zijn [ondersteund door de serialisatiefunctie van het gegevenscontract](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) wanneer u de serialisatiefunctie standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c307e-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span></span>
* <span data-ttu-id="c307e-197">Objecten worden gerepliceerd voor hoge beschikbaarheid, wanneer u transacties op betrouwbare verzamelingen doorvoert.</span><span class="sxs-lookup"><span data-stu-id="c307e-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="c307e-198">Objecten die zijn opgeslagen in betrouwbare verzamelingen worden opgeslagen in het lokale geheugen van uw service.</span><span class="sxs-lookup"><span data-stu-id="c307e-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="c307e-199">Dit betekent dat u een lokale verwijzing naar het object hebt.</span><span class="sxs-lookup"><span data-stu-id="c307e-199">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="c307e-200">Het is belangrijk dat u geen lokale exemplaren van deze objecten muteren zonder dat u een updatebewerking op de verzameling betrouwbare uitvoert in een transactie.</span><span class="sxs-lookup"><span data-stu-id="c307e-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="c307e-201">Dit is omdat wijzigingen in de lokale exemplaren van objecten worden niet automatisch worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="c307e-201">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="c307e-202">U moet het object opnieuw weer in de woordenlijst invoegen of gebruik een van de *bijwerken* methoden in de woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="c307e-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="c307e-203">Statusbeheer voor het betrouwbare beheert betrouwbare verzamelingen voor u.</span><span class="sxs-lookup"><span data-stu-id="c307e-203">The Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="c307e-204">U kunt gewoon vragen statusbeheer voor het betrouwbare voor een betrouwbare verzameling met de naam op elk gewenst moment en op een willekeurige plaats in uw service.</span><span class="sxs-lookup"><span data-stu-id="c307e-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="c307e-205">Statusbeheer voor het betrouwbare zorgt ervoor dat u een verwijzing terug.</span><span class="sxs-lookup"><span data-stu-id="c307e-205">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="c307e-206">Wordt niet aanbevolen verwijzingen naar betrouwbare verzameling exemplaren te slaan in klasselid variabelen of eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c307e-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="c307e-207">Speciale aandacht moet worden uitgevoerd om ervoor te zorgen dat de verwijzing naar een exemplaar te allen tijde in de levenscyclus van de service is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c307e-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="c307e-208">Statusbeheer voor het betrouwbare dit werk voor u verwerkt en geoptimaliseerd voor herhaaldelijk bezoeken.</span><span class="sxs-lookup"><span data-stu-id="c307e-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="c307e-209">Transactionele en asynchrone bewerkingen</span><span class="sxs-lookup"><span data-stu-id="c307e-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="c307e-210">Betrouwbare verzamelingen hebben veel van dezelfde bewerkingen die hun `System.Collections.Generic` en `System.Collections.Concurrent` collega's doen, met uitzondering van LINQ.</span><span class="sxs-lookup"><span data-stu-id="c307e-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="c307e-211">Bewerkingen op betrouwbare verzamelingen zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="c307e-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="c307e-212">Dit is omdat schrijfbewerkingen met betrouwbare verzamelingen i/o-bewerkingen als u wilt repliceren en de gegevens naar schijf te behouden.</span><span class="sxs-lookup"><span data-stu-id="c307e-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="c307e-213">Betrouwbare verzameling bewerkingen zijn *transactionele*, zodat u status consistent voor meerdere betrouwbare verzamelingen en bewerkingen houden kunt.</span><span class="sxs-lookup"><span data-stu-id="c307e-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="c307e-214">U kunt bijvoorbeeld een werkitem van een betrouwbare wachtrij in wachtrij, een bewerking uitvoeren op deze en het resultaat opslaan in een betrouwbare woordenlijst alle binnen een transactie.</span><span class="sxs-lookup"><span data-stu-id="c307e-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="c307e-215">Dit wordt beschouwd als een atomic-bewerking en dit zorgt ervoor dat de hele bewerking slaagt of de hele bewerking wordt teruggedraaid.</span><span class="sxs-lookup"><span data-stu-id="c307e-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="c307e-216">Als een fout optreedt nadat u het item in wachtrij, maar voordat u het resultaat opslaat, wordt de hele transactie wordt teruggedraaid en blijft het item in de wachtrij voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="c307e-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="c307e-217">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c307e-217">Run the application</span></span>
<span data-ttu-id="c307e-218">We nu terug naar de *HelloWorld* toepassing.</span><span class="sxs-lookup"><span data-stu-id="c307e-218">We now return to the *HelloWorld* application.</span></span> <span data-ttu-id="c307e-219">U kunt nu bouwen en implementeren van uw services.</span><span class="sxs-lookup"><span data-stu-id="c307e-219">You can now build and deploy your services.</span></span> <span data-ttu-id="c307e-220">Wanneer u drukt op **F5**, uw toepassing worden gemaakt en geïmplementeerd op uw lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="c307e-220">When you press **F5**, your application will be built and deployed to your local cluster.</span></span>

<span data-ttu-id="c307e-221">Nadat de services zijn gestart, kunt u weergeven met de gegenereerde Event Tracing voor Windows (ETW)-gebeurtenissen in een **diagnostische gebeurtenissen** venster.</span><span class="sxs-lookup"><span data-stu-id="c307e-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="c307e-222">Denk eraan dat de weergegeven gebeurtenissen afkomstig van zowel de staatloze service en de stateful service in de toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="c307e-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span></span> <span data-ttu-id="c307e-223">U kunt de stroom onderbreken door te klikken op de **onderbreken** knop.</span><span class="sxs-lookup"><span data-stu-id="c307e-223">You can pause the stream by clicking the **Pause** button.</span></span> <span data-ttu-id="c307e-224">U kunt vervolgens de details van een bericht controleren door het uitbreiden van dat bericht.</span><span class="sxs-lookup"><span data-stu-id="c307e-224">You can then examine the details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="c307e-225">Voordat u de toepassing uitvoert, zorg ervoor dat er een lokaal ontwikkelcluster uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c307e-225">Before you run the application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="c307e-226">Bekijk de [instructiehandleiding](service-fabric-get-started.md) voor informatie over het instellen van uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="c307e-226">Check out the [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Diagnostische gebeurtenissen weergeven in Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="c307e-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c307e-228">Next steps</span></span>
[<span data-ttu-id="c307e-229">Fouten opsporen in uw Service Fabric-toepassing in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c307e-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="c307e-230">Aan de slag: Service Fabric-Web-API-services met OWIN zelf die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="c307e-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="c307e-231">Meer informatie over betrouwbare verzamelingen</span><span class="sxs-lookup"><span data-stu-id="c307e-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="c307e-232">Een toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="c307e-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="c307e-233">Upgrade van de toepassing</span><span class="sxs-lookup"><span data-stu-id="c307e-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="c307e-234">Referentie voor ontwikkelaars voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c307e-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

