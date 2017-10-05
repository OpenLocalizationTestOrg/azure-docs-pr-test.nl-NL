---
title: Service voor externe toegang in Service Fabric | Microsoft Docs
description: Service Fabric remoting kan clients en -services te communiceren met services met behulp van een remote procedure call.
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
# <a name="service-remoting-with-reliable-services"></a>Service voor externe toegang met Reliable Services
Voor services die niet zijn gekoppeld aan een bepaalde communicatieprotocol of stack, zoals WebAPI, Windows Communication Foundation (WCF) of anderen, biedt het framework Reliable Services een mechanisme voor externe toegang voor het snel en eenvoudig instellen van externe procedureaanroep voor services.

## <a name="set-up-remoting-on-a-service"></a>Instellen van externe toegang voor een service
Instellen van externe toegang tot een service wordt uitgevoerd in de twee eenvoudige stappen:

1. Maak een interface voor uw service te implementeren. Deze interface definieert de methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service. De methoden moeten geretourneerd asynchrone methoden. De interface moet implementeren `Microsoft.ServiceFabric.Services.Remoting.IService` om aan te geven dat de service een externe communicatie-interface heeft.
2. Gebruik een listener voor externe toegang in uw service. Dit is een `ICommunicationListener` -implementatie mogelijkheden voor externe toegang biedt. De `Microsoft.ServiceFabric.Services.Remoting.Runtime` -naamruimte bevat een uitbreidingsmethode`CreateServiceRemotingListener` voor zowel stateless als stateful services die kunnen worden gebruikt voor het maken van de listener voor een externe toegang met behulp van het standaardprotocol voor het transport van externe toegang.

Opmerking: De `Remoting` naamruimte is beschikbaar als een afzonderlijke nuget-pakket aangeroepen`Microsoft.ServiceFabric.Services.Remoting` 

De volgende staatloze service wordt bijvoorbeeld één methode voor 'Hallo wereld' via een externe procedureaanroep.

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
> De argumenten en de retourtypen in de interface van de service mag geen enkelvoudig, complexe of aangepaste typen, maar ze moeten serialiseerbaar zijn door de .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Externe servicemethoden aanroepen
Bij het aanroepen van methoden met een service met behulp van de stack voor externe toegang wordt uitgevoerd met behulp van een lokale proxy voor de service via de `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasse. De `ServiceProxy` methode maakt u een lokale proxyserver met behulp van dezelfde interface die de service implementeert. Met de proxyserver, kunt u gewoon methoden aanroepen op de interface op afstand.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

Het framework remoting uitzonderingen op de service naar de client wordt doorgegeven. Dus uitzonderingsverwerking logica op de client met behulp van `ServiceProxy` uitzonderingen die de service genereert rechtstreeks kan verwerken.

## <a name="service-proxy-lifetime"></a>Levensduur voor service-Proxy
Het maken van ServiceProxy is een lichtgewicht bewerking, zodat gebruikers zo veel naar behoefte kunt maken. Proxy-service kan opnieuw worden gebruikt zolang de gebruiker nodig. Gebruiker kan dezelfde proxy in geval van een uitzondering opnieuw gebruiken. Elke ServiceProxy bevat communicatie sites client wordt gebruikt om berichten te verzenden via de kabel. Tijdens het aanroepen van API, hebben we interne controleert u of de client wordt communicatie gebruikt geldig is. Op basis van die resulteren, maken wordt de client communicatie opnieuw. Gebruiker hoeft dus niet opnieuw maken van serviceproxy in geval van een uitzondering.

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory levensduur
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is een factory die de proxy voor externe communicatie van andere interfaces maakt. Als u API ServiceProxy.Create voor het maken van proxy gebruikt, maakt de singelton ServiceProxyFactory met framework.
Is het nuttig om een handmatig maken als u wilt onderdrukken [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) eigenschappen.
Factory is een dure bewerking. ServiceProxyFactory houdt de cache van de client communicatie.
Aanbevolen procedure is het in de cache ServiceProxyFactory zo lang mogelijk.

## <a name="remoting-exception-handling"></a>Afhandeling van uitzonderingen voor externe toegang
De externe uitzondering veroorzaakt door de API-service, worden verzonden naar de client als AggregateException. RemoteExceptions moet DataContract serialiseerbaar anders [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) verstuurd naar de proxy-API met de serialisatiefout in het.

ServiceProxy wordt verwerkt alle failover-uitzondering voor de service-partitie dat deze wordt gemaakt. Deze opnieuw de eindpunten opgelost als er Failover Exceptions(Non-Transient Exceptions) en probeert om opnieuw de aanroep met het juiste eindpunt. Aantal nieuwe pogingen voor failover-uitzondering is oneindig.
In geval van een TransientExceptions, het alleen opnieuw probeert de aanroep.

Standaard opnieuw parameters worden opgegeven door [OperationRetrySettings]. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Gebruiker kan deze waarden door OperationRetrySettings object doorgeven aan de constructor ServiceProxyFactory configureren.

## <a name="next-steps"></a>Volgende stappen
* [Web-API met OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [WCF-communicatie met Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Beveiligen van communicatie voor Reliable Services](service-fabric-reliable-services-secure-communication.md)
