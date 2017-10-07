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
# <a name="service-remoting-with-reliable-services"></a>Service voor externe toegang met Reliable Services
> [!div class="op_single_selector"]
> * [C# op Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java op Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

Hallo Reliable Services framework biedt een mechanisme voor externe toegang tooquickly en gemakkelijk externe procedureaanroep voor services instellen.

## <a name="set-up-remoting-on-a-service"></a>Instellen van externe toegang voor een service
Instellen van externe toegang tot een service wordt uitgevoerd in de twee eenvoudige stappen:

1. Een interface voor uw service tooimplement maken. Deze interface definieert Hallo-methoden die beschikbaar voor een externe procedureaanroep voor uw service zijn. Hallo-methoden moeten geretourneerd asynchrone methoden. Hallo-interface moet implementeren `microsoft.serviceFabric.services.remoting.Service` toosignal die Hallo service heeft een interface voor externe toegang.
2. Gebruik een listener voor externe toegang in uw service. Dit is een `CommunicationListener` -implementatie mogelijkheden voor externe toegang biedt. `FabricTransportServiceRemotingListener`kan worden gebruikt toocreate met Hallo standaard remoting transportprotocol listener voor een externe toegang.

Bijvoorbeeld: hello volgende staatloze service wordt een enkele methode tooget 'Hallo wereld' via een externe procedureaanroep.

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
> Hallo argumenten en Hallo retourneren typen in de service-interface Hallo eenvoudige, aangepaste of complexe typen die kunnen worden, maar ze moeten worden geserialiseerd.
>
>

## <a name="call-remote-service-methods"></a>Externe servicemethoden aanroepen
Het aanroepen van methoden van een service met behulp van Hallo remoting stack doen met behulp van een lokale proxyserver toohello-service via Hallo `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasse. Hallo `ServiceProxyBase` methode maakt u een lokale proxyserver met behulp van Hallo dezelfde interface die Hallo service implementeert. Met de proxyserver, kunt u gewoon methoden op Hallo interface extern aanroepen.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

Hallo remoting framework uitzonderingen op Hallo service toohello client wordt doorgegeven. Dus uitzonderingsverwerking logica op Hallo van client met behulp van `ServiceProxyBase` uitzonderingen die service genereert Hallo rechtstreeks kan verwerken.

## <a name="service-proxy-lifetime"></a>Levensduur voor service-Proxy
Het maken van ServiceProxy is een lichtgewicht bewerking, zodat gebruikers zo veel naar behoefte kunt maken. Proxy-service kan opnieuw worden gebruikt zolang de gebruiker nodig. Gebruiker kan opnieuw gebruiken Hallo dezelfde proxy in geval van een uitzondering. Elke ServiceProxy bevat communicatie client gebruikt toosend berichten via de kabel Hallo. Tijdens het aanroepen van API, hebben we interne selectievakje toosee als communicatie-client gebruikt geldig is. Op basis van die resulteren, maken we Hallo communicatie client opnieuw. Gebruikers hoeven daarom niet toorecreate serviceproxy in geval van een uitzondering.

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory levensduur
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is een factory die de proxy voor externe communicatie van andere interfaces maakt. Als u API gebruikt `ServiceProxyBase.create` voor het maken van proxy framework maakt vervolgens een `FabricServiceProxyFactory`.
Deze nuttig toocreate een handmatig is wanneer u toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) eigenschappen.
Factory is een dure bewerking. `FabricServiceProxyFactory`houdt de cache van clients voor communicatie.
Aanbevolen procedure is toocache `FabricServiceProxyFactory` voor zo lang mogelijk.

## <a name="remoting-exception-handling"></a>Afhandeling van uitzonderingen voor externe toegang
Alle Hallo externe uitzondering door de service-API als RuntimeException of FabricException back toohello client worden verzonden.

ServiceProxy wordt verwerkt alle failover-uitzondering voor Hallo service partitie deze wordt gemaakt. Het oplossing Hallo-eindpunten opnieuw als er Failover Exceptions(Non-Transient Exceptions) en pogingen Hallo-aanroep met het juiste eindpunt Hallo. Aantal nieuwe pogingen voor failover-uitzondering is oneindig.
In geval van een TransientExceptions opnieuw deze alleen Hallo aanroep.

Standaard opnieuw parameters worden opgegeven door [OperationRetrySettings]. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Gebruiker kan deze waarden configureren door OperationRetrySettings object tooServiceProxyFactory constructor doorgeven.

## <a name="next-steps"></a>Volgende stappen
* [Beveiligen van communicatie voor Reliable Services](service-fabric-reliable-services-secure-communication.md)
