---
title: aaaService voor externe toegang in Service Fabric | Microsoft Docs
description: Service Fabric remoting kan clients en services toocommunicate met services met behulp van een remote procedure call.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="25b92-103">Service voor externe toegang met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="25b92-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="25b92-104">Voor services die niet zijn gebonden tooa bepaalde communicatieprotocol of stack, zoals WebAPI, Windows Communication Foundation (WCF) of anderen, Hallo Reliable Services framework biedt een mechanisme voor externe toegang tooquickly en externe procedureaanroep gemakkelijk instellen voor services.</span><span class="sxs-lookup"><span data-stu-id="25b92-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="25b92-105">Instellen van externe toegang voor een service</span><span class="sxs-lookup"><span data-stu-id="25b92-105">Set up remoting on a service</span></span>
<span data-ttu-id="25b92-106">Instellen van externe toegang tot een service wordt uitgevoerd in de twee eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="25b92-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="25b92-107">Een interface voor uw service tooimplement maken.</span><span class="sxs-lookup"><span data-stu-id="25b92-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="25b92-108">Deze interface definieert Hallo-methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service.</span><span class="sxs-lookup"><span data-stu-id="25b92-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="25b92-109">Hallo-methoden moeten geretourneerd asynchrone methoden.</span><span class="sxs-lookup"><span data-stu-id="25b92-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="25b92-110">Hallo-interface moet implementeren `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal die Hallo service heeft een interface voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="25b92-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="25b92-111">Gebruik een listener voor externe toegang in uw service.</span><span class="sxs-lookup"><span data-stu-id="25b92-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="25b92-112">Dit is een `ICommunicationListener` -implementatie mogelijkheden voor externe toegang biedt.</span><span class="sxs-lookup"><span data-stu-id="25b92-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="25b92-113">Hallo `Microsoft.ServiceFabric.Services.Remoting.Runtime` -naamruimte bevat een uitbreidingsmethode`CreateServiceRemotingListener` voor zowel stateless als stateful services die kan worden gebruikt toocreate een listener voor externe toegang via Hallo standaard remoting transportprotocol.</span><span class="sxs-lookup"><span data-stu-id="25b92-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="25b92-114">Opmerking: Hallo `Remoting` naamruimte is beschikbaar als een afzonderlijke nuget-pakket aangeroepen`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="25b92-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="25b92-115">Bijvoorbeeld: hello volgende staatloze service wordt een enkele methode tooget 'Hallo wereld' via een externe procedureaanroep.</span><span class="sxs-lookup"><span data-stu-id="25b92-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="25b92-116">Hallo argumenten en Hallo retourneren typen in de service-interface Hallo eenvoudige, aangepaste of complexe typen die kunnen worden, maar ze moeten serialiseerbaar door Hallo .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="25b92-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="25b92-117">Externe servicemethoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="25b92-117">Call remote service methods</span></span>
<span data-ttu-id="25b92-118">Het aanroepen van methoden van een service met behulp van Hallo remoting stack doen met behulp van een lokale proxyserver toohello-service via Hallo `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasse.</span><span class="sxs-lookup"><span data-stu-id="25b92-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="25b92-119">Hallo `ServiceProxy` methode maakt u een lokale proxyserver met behulp van Hallo dezelfde interface die Hallo service implementeert.</span><span class="sxs-lookup"><span data-stu-id="25b92-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="25b92-120">Met de proxyserver, kunt u gewoon methoden op Hallo interface extern aanroepen.</span><span class="sxs-lookup"><span data-stu-id="25b92-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="25b92-121">Hallo remoting framework uitzonderingen op Hallo service toohello client wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="25b92-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="25b92-122">Dus uitzonderingsverwerking logica op Hallo van client met behulp van `ServiceProxy` uitzonderingen die service genereert Hallo rechtstreeks kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="25b92-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="25b92-123">Levensduur voor service-Proxy</span><span class="sxs-lookup"><span data-stu-id="25b92-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="25b92-124">Het maken van ServiceProxy is een lichtgewicht bewerking, zodat gebruikers zo veel naar behoefte kunt maken.</span><span class="sxs-lookup"><span data-stu-id="25b92-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="25b92-125">Proxy-service kan opnieuw worden gebruikt zolang de gebruiker nodig.</span><span class="sxs-lookup"><span data-stu-id="25b92-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="25b92-126">Gebruiker kan opnieuw gebruiken Hallo dezelfde proxy in geval van een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="25b92-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="25b92-127">Elke ServiceProxy bevat communicatie sites client gebruikt toosend berichten via de kabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="25b92-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="25b92-128">Tijdens het aanroepen van API, hebben we interne selectievakje toosee als communicatie-client gebruikt geldig is.</span><span class="sxs-lookup"><span data-stu-id="25b92-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="25b92-129">Op basis van die resulteren, maken we Hallo communicatie client opnieuw.</span><span class="sxs-lookup"><span data-stu-id="25b92-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="25b92-130">Gebruikers hoeven daarom niet toorecreate serviceproxy in geval van een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="25b92-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="25b92-131">ServiceProxyFactory levensduur</span><span class="sxs-lookup"><span data-stu-id="25b92-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="25b92-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is een factory die de proxy voor externe communicatie van andere interfaces maakt.</span><span class="sxs-lookup"><span data-stu-id="25b92-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="25b92-133">Als u API ServiceProxy.Create voor het maken van proxy gebruikt, maakt framework Hallo singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="25b92-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="25b92-134">Deze nuttig toocreate een handmatig is wanneer u toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="25b92-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="25b92-135">Factory is een dure bewerking.</span><span class="sxs-lookup"><span data-stu-id="25b92-135">Factory is an expensive operation.</span></span> <span data-ttu-id="25b92-136">ServiceProxyFactory houdt de cache van de client communicatie.</span><span class="sxs-lookup"><span data-stu-id="25b92-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="25b92-137">Best practices is toocache ServiceProxyFactory voor zo lang mogelijk.</span><span class="sxs-lookup"><span data-stu-id="25b92-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="25b92-138">Afhandeling van uitzonderingen voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="25b92-138">Remoting Exception Handling</span></span>
<span data-ttu-id="25b92-139">Alle Hallo externe uitzondering door de service-API als AggregateException back toohello client verzonden.</span><span class="sxs-lookup"><span data-stu-id="25b92-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="25b92-140">RemoteExceptions moet DataContract serialiseerbaar anders [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) toohello proxy API met Hallo serialisatiefout erin wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="25b92-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="25b92-141">ServiceProxy wordt verwerkt alle failover-uitzondering voor Hallo service partitie deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25b92-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="25b92-142">Het oplossing Hallo-eindpunten opnieuw als er Failover Exceptions(Non-Transient Exceptions) en pogingen Hallo-aanroep met het juiste eindpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="25b92-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="25b92-143">Aantal nieuwe pogingen voor failover-uitzondering is oneindig.</span><span class="sxs-lookup"><span data-stu-id="25b92-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="25b92-144">In geval van een TransientExceptions opnieuw deze alleen Hallo aanroep.</span><span class="sxs-lookup"><span data-stu-id="25b92-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="25b92-145">Standaard opnieuw parameters worden opgegeven door [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="25b92-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="25b92-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Gebruiker kan deze waarden configureren door OperationRetrySettings object tooServiceProxyFactory constructor doorgeven.</span><span class="sxs-lookup"><span data-stu-id="25b92-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25b92-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25b92-147">Next steps</span></span>
* [<span data-ttu-id="25b92-148">Web-API met OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="25b92-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="25b92-149">WCF-communicatie met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="25b92-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="25b92-150">Beveiligen van communicatie voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="25b92-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
