---
title: <span data-ttu-id="bc025-101">Service voor externe toegang in Service Fabric | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="bc025-101">Service remoting in Service Fabric | Microsoft Docs</span></span>
description: <span data-ttu-id="bc025-102">Service Fabric remoting kan clients en -services te communiceren met services met behulp van een remote procedure call.</span><span class="sxs-lookup"><span data-stu-id="bc025-102">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>
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
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="bc025-103">Service voor externe toegang met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bc025-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="bc025-104">Voor services die niet zijn gekoppeld aan een bepaalde communicatieprotocol of stack, zoals WebAPI, Windows Communication Foundation (WCF) of anderen, biedt het framework Reliable Services een mechanisme voor externe toegang voor het snel en eenvoudig instellen van externe procedureaanroep voor services.</span><span class="sxs-lookup"><span data-stu-id="bc025-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="bc025-105">Instellen van externe toegang voor een service</span><span class="sxs-lookup"><span data-stu-id="bc025-105">Set up remoting on a service</span></span>
<span data-ttu-id="bc025-106">Instellen van externe toegang tot een service wordt uitgevoerd in de twee eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="bc025-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="bc025-107">Maak een interface voor uw service te implementeren.</span><span class="sxs-lookup"><span data-stu-id="bc025-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="bc025-108">Deze interface definieert de methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service.</span><span class="sxs-lookup"><span data-stu-id="bc025-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="bc025-109">De methoden moeten geretourneerd asynchrone methoden.</span><span class="sxs-lookup"><span data-stu-id="bc025-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="bc025-110">De interface moet implementeren `Microsoft.ServiceFabric.Services.Remoting.IService` om aan te geven dat de service een externe communicatie-interface heeft.</span><span class="sxs-lookup"><span data-stu-id="bc025-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="bc025-111">Gebruik een listener voor externe toegang in uw service.</span><span class="sxs-lookup"><span data-stu-id="bc025-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="bc025-112">Dit is een `ICommunicationListener` -implementatie mogelijkheden voor externe toegang biedt.</span><span class="sxs-lookup"><span data-stu-id="bc025-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="bc025-113">De `Microsoft.ServiceFabric.Services.Remoting.Runtime` -naamruimte bevat een uitbreidingsmethode`CreateServiceRemotingListener` voor zowel stateless als stateful services die kunnen worden gebruikt voor het maken van de listener voor een externe toegang met behulp van het standaardprotocol voor het transport van externe toegang.</span><span class="sxs-lookup"><span data-stu-id="bc025-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="bc025-114">Opmerking: De `Remoting` naamruimte is beschikbaar als een afzonderlijke nuget-pakket aangeroepen`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="bc025-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="bc025-115">De volgende staatloze service wordt bijvoorbeeld één methode voor 'Hallo wereld' via een externe procedureaanroep.</span><span class="sxs-lookup"><span data-stu-id="bc025-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="bc025-116">De argumenten en de retourtypen in de interface van de service mag geen enkelvoudig, complexe of aangepaste typen, maar ze moeten serialiseerbaar zijn door de .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc025-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="bc025-117">Externe servicemethoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="bc025-117">Call remote service methods</span></span>
<span data-ttu-id="bc025-118">Bij het aanroepen van methoden met een service met behulp van de stack voor externe toegang wordt uitgevoerd met behulp van een lokale proxy voor de service via de `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasse.</span><span class="sxs-lookup"><span data-stu-id="bc025-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="bc025-119">De `ServiceProxy` methode maakt u een lokale proxyserver met behulp van dezelfde interface die de service implementeert.</span><span class="sxs-lookup"><span data-stu-id="bc025-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="bc025-120">Met de proxyserver, kunt u gewoon methoden aanroepen op de interface op afstand.</span><span class="sxs-lookup"><span data-stu-id="bc025-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="bc025-121">Het framework remoting uitzonderingen op de service naar de client wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="bc025-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="bc025-122">Dus uitzonderingsverwerking logica op de client met behulp van `ServiceProxy` uitzonderingen die de service genereert rechtstreeks kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="bc025-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="bc025-123">Levensduur voor service-Proxy</span><span class="sxs-lookup"><span data-stu-id="bc025-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="bc025-124">Het maken van ServiceProxy is een lichtgewicht bewerking, zodat gebruikers zo veel naar behoefte kunt maken.</span><span class="sxs-lookup"><span data-stu-id="bc025-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="bc025-125">Proxy-service kan opnieuw worden gebruikt zolang de gebruiker nodig.</span><span class="sxs-lookup"><span data-stu-id="bc025-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="bc025-126">Gebruiker kan dezelfde proxy in geval van een uitzondering opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc025-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="bc025-127">Elke ServiceProxy bevat communicatie sites client wordt gebruikt om berichten te verzenden via de kabel.</span><span class="sxs-lookup"><span data-stu-id="bc025-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="bc025-128">Tijdens het aanroepen van API, hebben we interne controleert u of de client wordt communicatie gebruikt geldig is.</span><span class="sxs-lookup"><span data-stu-id="bc025-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="bc025-129">Op basis van die resulteren, maken wordt de client communicatie opnieuw.</span><span class="sxs-lookup"><span data-stu-id="bc025-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="bc025-130">Gebruiker hoeft dus niet opnieuw maken van serviceproxy in geval van een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="bc025-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="bc025-131">ServiceProxyFactory levensduur</span><span class="sxs-lookup"><span data-stu-id="bc025-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="bc025-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is een factory die de proxy voor externe communicatie van andere interfaces maakt.</span><span class="sxs-lookup"><span data-stu-id="bc025-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="bc025-133">Als u API ServiceProxy.Create voor het maken van proxy gebruikt, maakt de singelton ServiceProxyFactory met framework.</span><span class="sxs-lookup"><span data-stu-id="bc025-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="bc025-134">Is het nuttig om een handmatig maken als u wilt onderdrukken [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="bc025-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="bc025-135">Factory is een dure bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc025-135">Factory is an expensive operation.</span></span> <span data-ttu-id="bc025-136">ServiceProxyFactory houdt de cache van de client communicatie.</span><span class="sxs-lookup"><span data-stu-id="bc025-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="bc025-137">Aanbevolen procedure is het in de cache ServiceProxyFactory zo lang mogelijk.</span><span class="sxs-lookup"><span data-stu-id="bc025-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="bc025-138">Afhandeling van uitzonderingen voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="bc025-138">Remoting Exception Handling</span></span>
<span data-ttu-id="bc025-139">De externe uitzondering veroorzaakt door de API-service, worden verzonden naar de client als AggregateException.</span><span class="sxs-lookup"><span data-stu-id="bc025-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="bc025-140">RemoteExceptions moet DataContract serialiseerbaar anders [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) verstuurd naar de proxy-API met de serialisatiefout in het.</span><span class="sxs-lookup"><span data-stu-id="bc025-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="bc025-141">ServiceProxy wordt verwerkt alle failover-uitzondering voor de service-partitie dat deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bc025-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="bc025-142">Deze opnieuw de eindpunten opgelost als er Failover Exceptions(Non-Transient Exceptions) en probeert om opnieuw de aanroep met het juiste eindpunt.</span><span class="sxs-lookup"><span data-stu-id="bc025-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="bc025-143">Aantal nieuwe pogingen voor failover-uitzondering is oneindig.</span><span class="sxs-lookup"><span data-stu-id="bc025-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="bc025-144">In geval van een TransientExceptions, het alleen opnieuw probeert de aanroep.</span><span class="sxs-lookup"><span data-stu-id="bc025-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="bc025-145">Standaard opnieuw parameters worden opgegeven door [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="bc025-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="bc025-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Gebruiker kan deze waarden door OperationRetrySettings object doorgeven aan de constructor ServiceProxyFactory configureren.</span><span class="sxs-lookup"><span data-stu-id="bc025-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc025-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc025-147">Next steps</span></span>
* [<span data-ttu-id="bc025-148">Web-API met OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bc025-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="bc025-149">WCF-communicatie met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bc025-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="bc025-150">Beveiligen van communicatie voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bc025-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
