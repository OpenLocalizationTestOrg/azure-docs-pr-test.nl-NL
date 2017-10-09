---
title: aaaReliable WCF Services communicatiestack | Microsoft Docs
description: Hallo ingebouwde WCF communicatiestack in Service Fabric biedt WCF-communicatie van client-service voor Reliable Services.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="2c059-103">WCF-communicatiestack voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2c059-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="2c059-104">Hallo Reliable Services framework kunt service auteurs toochoose hello communicatiestack ze toouse willen gebruiken voor hun service.</span><span class="sxs-lookup"><span data-stu-id="2c059-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="2c059-105">Ze communicatiestack Hallo van hun keuze via Hallo kunnen aansluiten **ICommunicationListener** geretourneerd van Hallo [CreateServiceReplicaListeners of CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methoden.</span><span class="sxs-lookup"><span data-stu-id="2c059-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="2c059-106">Hallo-framework biedt een implementatie van Hallo communicatiestack op basis van Hallo Windows Communication Foundation (WCF) voor service-auteurs willen toouse WCF-communicatie.</span><span class="sxs-lookup"><span data-stu-id="2c059-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="2c059-107">Listener voor WCF-communicatie</span><span class="sxs-lookup"><span data-stu-id="2c059-107">WCF Communication Listener</span></span>
<span data-ttu-id="2c059-108">Hallo WCF-specifieke implementatie van **ICommunicationListener** wordt geleverd door Hallo **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** klasse.</span><span class="sxs-lookup"><span data-stu-id="2c059-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="2c059-109">Lest spreek we een servicecontract van het type hebben`ICalculator`</span><span class="sxs-lookup"><span data-stu-id="2c059-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="2c059-110">We kunt een WCF-communicatie-listener Hallo service Hallo volgende wijze maken.</span><span class="sxs-lookup"><span data-stu-id="2c059-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="2c059-111">Clients voor Hallo WCF communicatiestack schrijven</span><span class="sxs-lookup"><span data-stu-id="2c059-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="2c059-112">Voor het schrijven van clients toocommunicate met services met behulp van WCF, Hallo-framework biedt **WcfClientCommunicationFactory**, namelijk Hallo WCF-specifieke implementatie van [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="2c059-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="2c059-113">Hallo WCF communicatiekanaal toegankelijk zijn vanuit Hallo **WcfCommunicationClient** gemaakt door Hallo **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="2c059-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="2c059-114">Clientcode kunt Hallo **WcfCommunicationClientFactory** samen met de Hallo **WcfCommunicationClient** welke implements **ServicePartitionClient** toodetermine Hallo service-eindpunt en communiceren met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="2c059-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="2c059-115">Hallo standaard ServicePartitionResolver wordt ervan uitgegaan dat Hallo-client in hetzelfde cluster als Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2c059-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="2c059-116">Als dat niet Hallo geval is, een ServicePartitionResolver-object maken en in verbindingseindpunten Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2c059-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2c059-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2c059-117">Next steps</span></span>
* [<span data-ttu-id="2c059-118">Externe procedureaanroep met Reliable Services voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="2c059-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="2c059-119">Web-API met OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2c059-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="2c059-120">Beveiligen van communicatie voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2c059-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

