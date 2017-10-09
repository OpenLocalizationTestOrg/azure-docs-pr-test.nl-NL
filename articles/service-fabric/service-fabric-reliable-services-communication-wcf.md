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
# <a name="wcf-based-communication-stack-for-reliable-services"></a>WCF-communicatiestack voor Reliable Services
Hallo Reliable Services framework kunt service auteurs toochoose hello communicatiestack ze toouse willen gebruiken voor hun service. Ze communicatiestack Hallo van hun keuze via Hallo kunnen aansluiten **ICommunicationListener** geretourneerd van Hallo [CreateServiceReplicaListeners of CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methoden. Hallo-framework biedt een implementatie van Hallo communicatiestack op basis van Hallo Windows Communication Foundation (WCF) voor service-auteurs willen toouse WCF-communicatie.

## <a name="wcf-communication-listener"></a>Listener voor WCF-communicatie
Hallo WCF-specifieke implementatie van **ICommunicationListener** wordt geleverd door Hallo **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** klasse.

Lest spreek we een servicecontract van het type hebben`ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

We kunt een WCF-communicatie-listener Hallo service Hallo volgende wijze maken.

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>Clients voor Hallo WCF communicatiestack schrijven
Voor het schrijven van clients toocommunicate met services met behulp van WCF, Hallo-framework biedt **WcfClientCommunicationFactory**, namelijk Hallo WCF-specifieke implementatie van [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

Hallo WCF communicatiekanaal toegankelijk zijn vanuit Hallo **WcfCommunicationClient** gemaakt door Hallo **WcfCommunicationClientFactory**.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

Clientcode kunt Hallo **WcfCommunicationClientFactory** samen met de Hallo **WcfCommunicationClient** welke implements **ServicePartitionClient** toodetermine Hallo service-eindpunt en communiceren met Hallo-service.

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
> Hallo standaard ServicePartitionResolver wordt ervan uitgegaan dat Hallo-client in hetzelfde cluster als Hallo-service wordt uitgevoerd. Als dat niet Hallo geval is, een ServicePartitionResolver-object maken en in verbindingseindpunten Hallo-cluster.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Externe procedureaanroep met Reliable Services voor externe toegang](service-fabric-reliable-services-communication-remoting.md)
* [Web-API met OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Beveiligen van communicatie voor Reliable Services](service-fabric-reliable-services-secure-communication.md)

