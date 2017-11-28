---
title: Betrouwbare WCF Services communicatiestack | Microsoft Docs
description: De ingebouwde WCF communicatie-stack in Service Fabric biedt WCF-communicatie van client-service voor Reliable Services.
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
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="7d1f4-103">WCF-communicatiestack voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7d1f4-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="7d1f4-104">Het framework Reliable Services kan auteurs in service kiezen van de communicatiestack die ze willen gebruiken voor hun service.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="7d1f4-105">Ze kunnen plug-in de communicatiestack van hun keuze via de **ICommunicationListener** geretourneerd door de [CreateServiceReplicaListeners of CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methoden.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="7d1f4-106">Het framework biedt een implementatie van de communicatiestack gebaseerd op Windows Communication Foundation (WCF) voor service-auteurs die u wilt gebruiken, WCF-communicatie.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="7d1f4-107">Listener voor WCF-communicatie</span><span class="sxs-lookup"><span data-stu-id="7d1f4-107">WCF Communication Listener</span></span>
<span data-ttu-id="7d1f4-108">De WCF-specifieke implementatie van **ICommunicationListener** wordt geleverd door de **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** klasse.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="7d1f4-109">Lest spreek we een servicecontract van het type hebben`ICalculator`</span><span class="sxs-lookup"><span data-stu-id="7d1f4-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="7d1f4-110">We kunnen de listener voor een WCF-communicatie maken in de service de volgende manier.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="7d1f4-111">Schrijven van clients voor de WCF-stack-communicatie</span><span class="sxs-lookup"><span data-stu-id="7d1f4-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="7d1f4-112">Voor het schrijven van clients te communiceren met services met behulp van WCF het framework biedt **WcfClientCommunicationFactory**, dit is de WCF-specifieke implementatie van [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="7d1f4-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="7d1f4-113">Het communicatiekanaal WCF toegankelijk is vanaf de **WcfCommunicationClient** gemaakt door de **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="7d1f4-114">Clientcode kunt gebruiken de **WcfCommunicationClientFactory** samen met de **WcfCommunicationClient** welke implements **ServicePartitionClient** om te bepalen van het service-eindpunt en communiceren met de service.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="7d1f4-115">De standaardwaarde ServicePartitionResolver wordt ervan uitgegaan dat de client in hetzelfde cluster als de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="7d1f4-116">Als dat niet het geval is, een ServicePartitionResolver-object maken en in de eindpunten van het cluster-verbinding.</span><span class="sxs-lookup"><span data-stu-id="7d1f4-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7d1f4-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d1f4-117">Next steps</span></span>
* [<span data-ttu-id="7d1f4-118">Externe procedureaanroep met Reliable Services voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="7d1f4-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="7d1f4-119">Web-API met OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7d1f4-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="7d1f4-120">Beveiligen van communicatie voor Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7d1f4-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

