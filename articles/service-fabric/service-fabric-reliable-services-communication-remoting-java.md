---
title: aaaService voor externe toegang in Azure Service Fabric | Microsoft Docs
description: Service Fabric remoting kan clients en services toocommunicate met services met behulp van een remote procedure call.
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="cc46a-103">Service voor externe toegang met Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cc46a-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc46a-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="cc46a-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="cc46a-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="cc46a-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="cc46a-106">Hallo Reliable Services framework biedt een mechanisme voor externe toegang tooquickly en gemakkelijk externe procedureaanroep voor services instellen.</span><span class="sxs-lookup"><span data-stu-id="cc46a-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="cc46a-107">Instellen van externe toegang voor een service</span><span class="sxs-lookup"><span data-stu-id="cc46a-107">Set up remoting on a service</span></span>
<span data-ttu-id="cc46a-108">Instellen van externe toegang tot een service wordt uitgevoerd in de twee eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="cc46a-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="cc46a-109">Een interface voor uw service tooimplement maken.</span><span class="sxs-lookup"><span data-stu-id="cc46a-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="cc46a-110">Deze interface definieert Hallo-methoden die beschikbaar voor een externe procedureaanroep voor uw service zijn.</span><span class="sxs-lookup"><span data-stu-id="cc46a-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="cc46a-111">Hallo-methoden moeten geretourneerd asynchrone methoden.</span><span class="sxs-lookup"><span data-stu-id="cc46a-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="cc46a-112">Hallo-interface moet implementeren `microsoft.serviceFabric.services.remoting.Service` toosignal die Hallo service heeft een interface voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="cc46a-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="cc46a-113">Gebruik een listener voor externe toegang in uw service.</span><span class="sxs-lookup"><span data-stu-id="cc46a-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="cc46a-114">Dit is een `CommunicationListener` -implementatie mogelijkheden voor externe toegang biedt.</span><span class="sxs-lookup"><span data-stu-id="cc46a-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="cc46a-115">`FabricTransportServiceRemotingListener`kan worden gebruikt toocreate met Hallo standaard remoting transportprotocol listener voor een externe toegang.</span><span class="sxs-lookup"><span data-stu-id="cc46a-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="cc46a-116">Bijvoorbeeld: hello volgende staatloze service wordt een enkele methode tooget 'Hallo wereld' via een externe procedureaanroep.</span><span class="sxs-lookup"><span data-stu-id="cc46a-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="cc46a-117">Hallo argumenten en Hallo retourneren typen in de service-interface Hallo eenvoudige, aangepaste of complexe typen die kunnen worden, maar ze moeten worden geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="cc46a-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="cc46a-118">Externe servicemethoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="cc46a-118">Call remote service methods</span></span>
<span data-ttu-id="cc46a-119">Het aanroepen van methoden van een service met behulp van Hallo remoting stack doen met behulp van een lokale proxyserver toohello-service via Hallo `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasse.</span><span class="sxs-lookup"><span data-stu-id="cc46a-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="cc46a-120">Hallo `ServiceProxyBase` methode maakt u een lokale proxyserver met behulp van Hallo dezelfde interface die Hallo service implementeert.</span><span class="sxs-lookup"><span data-stu-id="cc46a-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="cc46a-121">Met de proxyserver, kunt u gewoon methoden op Hallo interface extern aanroepen.</span><span class="sxs-lookup"><span data-stu-id="cc46a-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="cc46a-122">Hallo remoting framework uitzonderingen op Hallo service toohello client wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="cc46a-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="cc46a-123">Dus uitzonderingsverwerking logica op Hallo van client met behulp van `ServiceProxyBase` uitzonderingen die service genereert Hallo rechtstreeks kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="cc46a-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="cc46a-124">Levensduur voor service-Proxy</span><span class="sxs-lookup"><span data-stu-id="cc46a-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="cc46a-125">Het maken van ServiceProxy is een lichtgewicht bewerking, zodat gebruikers zo veel naar behoefte kunt maken.</span><span class="sxs-lookup"><span data-stu-id="cc46a-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="cc46a-126">Proxy-service kan opnieuw worden gebruikt zolang de gebruiker nodig.</span><span class="sxs-lookup"><span data-stu-id="cc46a-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="cc46a-127">Gebruiker kan opnieuw gebruiken Hallo dezelfde proxy in geval van een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="cc46a-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="cc46a-128">Elke ServiceProxy bevat communicatie client gebruikt toosend berichten via de kabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc46a-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="cc46a-129">Tijdens het aanroepen van API, hebben we interne selectievakje toosee als communicatie-client gebruikt geldig is.</span><span class="sxs-lookup"><span data-stu-id="cc46a-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="cc46a-130">Op basis van die resulteren, maken we Hallo communicatie client opnieuw.</span><span class="sxs-lookup"><span data-stu-id="cc46a-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="cc46a-131">Gebruikers hoeven daarom niet toorecreate serviceproxy in geval van een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="cc46a-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="cc46a-132">ServiceProxyFactory levensduur</span><span class="sxs-lookup"><span data-stu-id="cc46a-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="cc46a-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is een factory die de proxy voor externe communicatie van andere interfaces maakt.</span><span class="sxs-lookup"><span data-stu-id="cc46a-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="cc46a-134">Als u API gebruikt `ServiceProxyBase.create` voor het maken van proxy framework maakt vervolgens een `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="cc46a-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="cc46a-135">Deze nuttig toocreate een handmatig is wanneer u toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="cc46a-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="cc46a-136">Factory is een dure bewerking.</span><span class="sxs-lookup"><span data-stu-id="cc46a-136">Factory is an expensive operation.</span></span> <span data-ttu-id="cc46a-137">`FabricServiceProxyFactory`houdt de cache van clients voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="cc46a-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="cc46a-138">Aanbevolen procedure is toocache `FabricServiceProxyFactory` voor zo lang mogelijk.</span><span class="sxs-lookup"><span data-stu-id="cc46a-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="cc46a-139">Afhandeling van uitzonderingen voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="cc46a-139">Remoting Exception Handling</span></span>
<span data-ttu-id="cc46a-140">Alle Hallo externe uitzondering door de service-API als RuntimeException of FabricException back toohello client worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="cc46a-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="cc46a-141">ServiceProxy wordt verwerkt alle failover-uitzondering voor Hallo service partitie deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cc46a-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="cc46a-142">Het oplossing Hallo-eindpunten opnieuw als er Failover Exceptions(Non-Transient Exceptions) en pogingen Hallo-aanroep met het juiste eindpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="cc46a-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="cc46a-143">Aantal nieuwe pogingen voor failover-uitzondering is oneindig.</span><span class="sxs-lookup"><span data-stu-id="cc46a-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="cc46a-144">In geval van een TransientExceptions opnieuw deze alleen Hallo aanroep.</span><span class="sxs-lookup"><span data-stu-id="cc46a-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="cc46a-145">Standaard opnieuw parameters worden opgegeven door [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="cc46a-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="cc46a-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Gebruiker kan deze waarden configureren door OperationRetrySettings object tooServiceProxyFactory constructor doorgeven.</span><span class="sxs-lookup"><span data-stu-id="cc46a-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc46a-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cc46a-147">Next steps</span></span>
* [<span data-ttu-id="cc46a-148">Beveiligen van communicatie voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cc46a-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
