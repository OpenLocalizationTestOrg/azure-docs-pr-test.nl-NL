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
# <a name="service-remoting-with-reliable-services"></a>Service voor externe toegang met Reliable Services
Voor services die niet zijn gebonden tooa bepaalde communicatieprotocol of stack, zoals WebAPI, Windows Communication Foundation (WCF) of anderen, Hallo Reliable Services framework biedt een mechanisme voor externe toegang tooquickly en externe procedureaanroep gemakkelijk instellen voor services.

## <a name="set-up-remoting-on-a-service"></a>Instellen van externe toegang voor een service
Instellen van externe toegang tot een service wordt uitgevoerd in de twee eenvoudige stappen:

1. Een interface voor uw service tooimplement maken. Deze interface definieert Hallo-methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service. Hallo-methoden moeten geretourneerd asynchrone methoden. Hallo-interface moet implementeren `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal die Hallo service heeft een interface voor externe toegang.
2. Gebruik een listener voor externe toegang in uw service. Dit is een `ICommunicationListener` -implementatie mogelijkheden voor externe toegang biedt. Hallo `Microsoft.ServiceFabric.Services.Remoting.Runtime` -naamruimte bevat een uitbreidingsmethode`CreateServiceRemotingListener` voor zowel stateless als stateful services die kan worden gebruikt toocreate een listener voor externe toegang via Hallo standaard remoting transportprotocol.

Opmerking: Hallo `Remoting` naamruimte is beschikbaar als een afzonderlijke nuget-pakket aangeroepen`Microsoft.ServiceFabric.Services.Remoting` 

Bijvoorbeeld: hello volgende staatloze service wordt een enkele methode tooget 'Hallo wereld' via een externe procedureaanroep.

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
> Hallo argumenten en Hallo retourneren typen in de service-interface Hallo eenvoudige, aangepaste of complexe typen die kunnen worden, maar ze moeten serialiseerbaar door Hallo .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Externe servicemethoden aanroepen
Het aanroepen van methoden van een service met behulp van Hallo remoting stack doen met behulp van een lokale proxyserver toohello-service via Hallo `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasse. Hallo `ServiceProxy` methode maakt u een lokale proxyserver met behulp van Hallo dezelfde interface die Hallo service implementeert. Met de proxyserver, kunt u gewoon methoden op Hallo interface extern aanroepen.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

Hallo remoting framework uitzonderingen op Hallo service toohello client wordt doorgegeven. Dus uitzonderingsverwerking logica op Hallo van client met behulp van `ServiceProxy` uitzonderingen die service genereert Hallo rechtstreeks kan verwerken.

## <a name="service-proxy-lifetime"></a>Levensduur voor service-Proxy
Het maken van ServiceProxy is een lichtgewicht bewerking, zodat gebruikers zo veel naar behoefte kunt maken. Proxy-service kan opnieuw worden gebruikt zolang de gebruiker nodig. Gebruiker kan opnieuw gebruiken Hallo dezelfde proxy in geval van een uitzondering. Elke ServiceProxy bevat communicatie sites client gebruikt toosend berichten via de kabel Hallo. Tijdens het aanroepen van API, hebben we interne selectievakje toosee als communicatie-client gebruikt geldig is. Op basis van die resulteren, maken we Hallo communicatie client opnieuw. Gebruikers hoeven daarom niet toorecreate serviceproxy in geval van een uitzondering.

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory levensduur
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is een factory die de proxy voor externe communicatie van andere interfaces maakt. Als u API ServiceProxy.Create voor het maken van proxy gebruikt, maakt framework Hallo singelton ServiceProxyFactory.
Deze nuttig toocreate een handmatig is wanneer u toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) eigenschappen.
Factory is een dure bewerking. ServiceProxyFactory houdt de cache van de client communicatie.
Best practices is toocache ServiceProxyFactory voor zo lang mogelijk.

## <a name="remoting-exception-handling"></a>Afhandeling van uitzonderingen voor externe toegang
Alle Hallo externe uitzondering door de service-API als AggregateException back toohello client verzonden. RemoteExceptions moet DataContract serialiseerbaar anders [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) toohello proxy API met Hallo serialisatiefout erin wordt gegenereerd.

ServiceProxy wordt verwerkt alle failover-uitzondering voor Hallo service partitie deze wordt gemaakt. Het oplossing Hallo-eindpunten opnieuw als er Failover Exceptions(Non-Transient Exceptions) en pogingen Hallo-aanroep met het juiste eindpunt Hallo. Aantal nieuwe pogingen voor failover-uitzondering is oneindig.
In geval van een TransientExceptions opnieuw deze alleen Hallo aanroep.

Standaard opnieuw parameters worden opgegeven door [OperationRetrySettings]. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Gebruiker kan deze waarden configureren door OperationRetrySettings object tooServiceProxyFactory constructor doorgeven.

## <a name="next-steps"></a>Volgende stappen
* [Web-API met OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [WCF-communicatie met Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Beveiligen van communicatie voor Reliable Services](service-fabric-reliable-services-secure-communication.md)
