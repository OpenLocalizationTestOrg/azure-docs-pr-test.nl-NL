---
title: een webfront-end voor uw Azure Service Fabric-app met behulp van ASP.NET Core aaaCreate | Microsoft Docs
description: Uw web-Service Fabric-toepassing toohello weergeven met behulp van een ASP.NET Core project en service-interne communicatie via de Service voor externe toegang.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Een service webfront-end voor uw toepassing met behulp van ASP.NET Core bouwen
Azure Service Fabric-services bieden standaard geen een openbare interface toohello web. tooexpose van uw toepassing functionaliteit tooHTTP clients, hebt u toocreate een web project tooact als een toegangspunt en vervolgens communiceren van er tooyour afzonderlijke services.

In deze zelfstudie gaan we waar we werd afgebroken in Hallo [maken van uw eerste toepassing in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) zelfstudie en een webservice ASP.NET Core voren Hallo teller stateful service toevoegen. Als u dit nog niet hebt gedaan, moet u teruggaan en deze zelfstudie eerst doorlopen.

## <a name="set-up-your-environment-for-aspnet-core"></a>Instellen van uw omgeving voor ASP.NET Core

Moet u Visual Studio 2017 toofollow samen met deze zelfstudie. Elke editie wordt gedaan. 

 - [Visual Studio 2017 installeren](https://www.visualstudio.com/)

toodevelop ASP.NET Core Service Fabric-toepassingen, moet u Hallo volgende van werkbelastingen geïnstalleerd hebben:
 - **Ontwikkelen van Azure** (onder *Web- en Cloud*)
 - **ASP.NET- en web ontwikkeling** (onder *Web- en Cloud*)
 - **.NET core platformoverschrijdende ontwikkeling** (onder *andere Toolsets*)

>[!Note] 
>Hallo .NET Core tools voor Visual Studio 2015 zijn niet langer wordt bijgewerkt, maar als u nog steeds Visual Studio 2015 gebruikt, u toohave moet [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) geïnstalleerd.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>Een ASP.NET Core service tooyour toepassing toevoegen
ASP.NET Core is een lichtgewicht, platformoverschrijdende ontwikkeling webframework toocreate moderne webgebruikersinterface gebruiken en web-API's. 

We gaan een ASP.NET Web API-project tooour bestaande toepassing toevoegen.

1. Klik in Solution Explorer met de rechtermuisknop op **Services** binnen Hallo application-project en kies **toevoegen > nieuwe Service Fabric-Service**.
   
    ![Een nieuwe service tooan bestaande toepassing toevoegen][vs-add-new-service]
2. Op Hallo **maken van een Service** pagina **ASP.NET Core** en een naam geven.
   
    ![ASP.NET-webservice te kiezen in het dialoogvenster voor nieuwe service Hallo][vs-new-service-dialog]

3. de volgende pagina Hallo biedt een set van ASP.NET Core projectsjablonen. Opmerking dat deze identiek zijn Hallo keuzes die u zou zien als u een project ASP.NET Core buiten een Service Fabric-toepassing hebt gemaakt met een kleine hoeveelheid aanvullende code tooregister Hallo service met de Hallo Service Fabric-runtime. Voor deze zelfstudie kiest **Web API**. U kunt echter toepassen Hallo dezelfde concepten toobuilding een volledige webtoepassing.
   
    ![ASP.NET-projecttype kiezen][vs-new-aspnet-project-dialog]
   
    Zodra uw Web API-project is gemaakt, hebt u twee services in uw toepassing. Als u toobuild uw toepassing doorgaat, kunt u meer services toevoegen in exact Hallo dezelfde manier. Elk zijn onafhankelijk samengestelde en bijgewerkte.

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren
tooget een beeld krijgt van wat we hebt gedaan, gaan we implementeren de nieuwe toepassing hello en los het bekijkt hello standaardgedrag dat ASP.NET Core Web API-sjabloon Hallo biedt.

1. Druk op F5 in Visual Studio toodebug Hallo-app.
2. Wanneer de implementatie is voltooid, Start Visual Studio een browser toohello basis Hallo ASP.NET Web API-service. Hallo ASP.NET Core Web API-sjabloon biedt niet standaardgedrag voor Hallo toegangspunt, zodat u een 404-fout in de browser Hallo ziet.
3. Voeg `/api/values` toohello locatie in Hallo browser. Hiermee wordt Hallo `Get` methode op Hallo ValuesController in Hallo Web API-sjabloon. Deze retourneert Hallo standaardreactie die wordt geleverd door Hallo sjabloon--een JSON-matrix die twee tekenreeksen bevat:
   
    ![Standaardwaarden geretourneerd van ASP.NET Core Web API-sjabloon][browser-aspnet-template-values]
   
    Hallo einde van de zelfstudie hello, wordt deze pagina weergegeven Hallo meest recente itemwaarde van onze stateful service in plaats van Hallo standaardtekenreeksen.

## <a name="connect-hello-services"></a>Verbinding maken met de Hallo-services
Service Fabric biedt volledige flexibiliteit in hoe u met reliable services communiceren. Binnen één toepassing hebt u mogelijk services die toegankelijk zijn via TCP, andere services die toegankelijk via een HTTP REST-API zijn en nog andere services die toegankelijk via het websockets zijn. Zie voor achtergrondinformatie over Hallo opties die beschikbaar zijn en Hallo-en nadelen betrokken [services communiceert](service-fabric-connect-and-communicate-with-services.md). In deze zelfstudie gebruiken we [Service Fabric-Service voor externe toegang](service-fabric-reliable-services-communication-remoting.md), opgegeven in Hallo SDK.

In Hallo Remoting Service benadering (gemodelleerd op externe procedureaanroepen of RPC's), definieert u een tooact interface als openbare contract Hallo voor Hallo-service. Vervolgens gebruikt u deze interface toogenerate een proxy-klasse voor interactie met Hallo-service.

### <a name="create-hello-remoting-interface"></a>Hallo-interface voor externe toegang maken
Begint met het maken van Hallo interface tooact als Hallo contract tussen Hallo stateful service en andere services, in deze aanvraag Hallo webproject ASP.NET Core. Deze interface moet worden gedeeld door alle services die gebruikmaken van deze toomake RPC-aanroepen, zodat deze in een eigen Class Library-project maakt.

1. Klik in Solution Explorer met de rechtermuisknop op uw oplossing en kies **toevoegen** > **nieuw Project**.

2. Kies Hallo **Visual C#** vermelding in het navigatiedeelvenster en selecteert u vervolgens Hallo Hallo **Class Library** sjabloon. Zorg ervoor dat .NET Framework-versie van het Hallo te is ingesteld**4.5.2**.
   
    ![Een project interface voor uw stateful service maken][vs-add-class-library-project]

3. Hallo installeren **Microsoft.ServiceFabric.Services.Remoting** NuGet-pakket. Zoeken naar **Microsoft.ServiceFabric.Services.Remoting** in Hallo NuGet-pakket manager en installeren voor alle projecten in Hallo oplossing die gebruikmaken van de Service voor externe toegang, waaronder:
   - Hallo Class Library-project met Hallo service-interface
   - Hallo Stateful Service-project
   - Hallo ASP.NET Core web service-project
   
    ![Hallo Services NuGet-pakket toe te voegen][vs-services-nuget-package]

4. Maak in klassebibliotheek hello, een interface met een enkele methode `GetCountAsync`, en uit te breiden Hallo-interface van `Microsoft.ServiceFabric.Services.Remoting.IService`. Hallo remoting interface moet worden afgeleid van deze interface tooindicate is een Service voor externe toegang-interface.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>Hallo-interface implementeren in uw stateful service
Nu dat we Hallo interface hebt gedefinieerd, moeten we tooimplement in Hallo stateful service.

1. In uw stateful service, Voeg een verwijzing toohello klasse bibliotheek-project met Hallo-interface.
   
    ![Een verwijzing toohello class library-project toe te voegen in Hallo stateful service][vs-add-class-library-reference]
2. Hallo-klasse die eigenschappen van overneemt vinden `StatefulService`, zoals `MyStatefulService`, en deze uitbreiden tooimplement hello `ICounter` interface.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. Hallo-één-methode die is gedefinieerd in Hallo nu implementeren `ICounter` interface, `GetCountAsync`.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Hallo stateful service met behulp van een service voor externe toegang-listener blootstelt
Hello `ICounter` interface geïmplementeerd, de laatste stap Hallo is tooopen Hallo Remoting Service communicatiekanaal. Voor stateful services, Service Fabric bevat een overschrijfbare methode aangeroepen `CreateServiceReplicaListeners`. Met deze methode kunt u een of meer communicatielisteners, op basis van Hallo type communicatie dat u voor uw service tooenable wilt opgeven.

> [!NOTE]
> Hallo gelijkwaardige methode voor het openen van een communicatie-kanaal toostateless services heet `CreateServiceInstanceListeners`.

In dit geval wordt de bestaande Hallo `CreateServiceReplicaListeners` methode en geef een exemplaar van `ServiceRemotingListener`, die een RPC-eindpunt maakt die kan worden aangeroepen van clients via `ServiceProxy`.  

Hallo `CreateServiceRemotingListener` uitbreidingsmethode op Hallo `IService` interface kunt u tooeasily maken een `ServiceRemotingListener` met alle standaardinstellingen. toouse deze uitbreidingsmethode, zorg ervoor dat u hebt Hallo `Microsoft.ServiceFabric.Services.Remoting.Runtime` naamruimte geïmporteerd. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Hallo ServiceProxy klasse toointeract gebruiken met Hallo-service
Onze stateful service is nu gereed tooreceive verkeer van andere services via RPC. Blijft is zodat Hallo code toocommunicate met het toevoegen van Hallo ASP.NET-webservice.

1. Toevoegen in uw ASP.NET-project een verwijzing toohello class-bibliotheek met Hallo `ICounter` interface.

2. Eerder u Hallo toegevoegd **Microsoft.ServiceFabric.Services.Remoting** NuGet-pakket toohello ASP.NET-project. Dit pakket biedt Hallo `ServiceProxy` klasse die u gebruikt toomake RPC toohello stateful service aanroepen. Zorg ervoor dat deze NuGet-pakket is geïnstalleerd in Hallo ASP.NET Core web service-project.

4. In Hallo **domeincontrollers** map, open Hallo `ValuesController` klasse. Houd er rekening mee dat Hallo `Get` methode wordt momenteel alleen een vastgelegde tekenreeksmatrix van 'waarde1' en 'waarde2'--die overeenkomt met wat we eerder in de browser Hallo gezien. Vervang deze implementatie met Hallo code te volgen:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    de eerste coderegel Hallo is Hallo sleutel. toocreate hello ICounter proxy toohello stateful service, moet u twee soorten informatie tooprovide: een partitie-ID en het Hallo-naam van Hallo-service.
   
    U kunt partitionering tooscale stateful services door deze van hun status in verschillende buckets, op basis van een sleutel die u hebt gedefinieerd, zoals een klant-ID of postcode te gebruiken. In onze toepassing trivial heeft Hallo stateful service slechts één partitie zodat Hallo-sleutel is niet van belang. Een sleutel die u opgeeft leidt toohello dezelfde partitie. toolearn meer informatie over het partitioneren van services, Zie [hoe toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).
   
    Hallo-servicenaam is een URI van Hallo formulier fabric: /&lt;$application_name&gt;/&lt;service_name&gt;.
   
    Met deze twee soorten informatie kunt Service Fabric Hallo-machine die aanvragen moeten worden verzonden naar een unieke identificatie. Hallo `ServiceProxy` klasse ook naadloos verwerkt Hallo geval waarbij Hallo-machine die als host fungeert voor Hallo stateful service partitie is mislukt en een andere computer moet worden bevorderd tootake plaats. Deze abstractie maakt schrijven Hallo van client code toodeal met andere services die aanzienlijk eenvoudiger.
   
    Wanneer we Hallo proxy hebt, roepen we Hallo `GetCountAsync` methode en het resultaat te retourneren.

5. Druk op F5 opnieuw toorun Hallo toepassing gewijzigd. Als voordat, Visual Studio wordt automatisch gestart Hallo browser toohello hoofdmap van Hallo webproject. Hallo 'api en-waarden' pad toevoegen en u ziet Hallo huidige waarde van het prestatiemeteritem geretourneerd.
   
    ![Hallo stateful itemwaarde weergegeven in de browser Hallo][browser-aspnet-counter-value]
   
    Vernieuw de browser Hallo periodiek toosee Hallo teller waarde update.

## <a name="kestrel-and-weblistener"></a>Kestrel en WebListener

Hallo standaard ASP.NET Core-webserver, Kestrel, ook wel is [momenteel niet ondersteund voor het verwerken van directe internetverkeer](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). Als gevolg hiervan hello ASP.NET Core staatloze servicesjabloon voor Service Fabric gebruikt [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) standaard. 

toolearn meer informatie over Kestrel en WebListener in Service Fabric-services, Raadpleeg te[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Verbinding maken met tooa betrouwbare Actor-service
Deze zelfstudie is gericht op het toevoegen van een webfront-end die gecommuniceerd met een stateful service. U kunt echter een vergelijkbaar model tootalk tooactors volgen. Wanneer u een betrouwbare Actor-project maakt, wordt in Visual Studio automatisch een interface-project voor u gegenereerd. Kunt u deze interface toogenerate een actor-proxy in Hallo web project toocommunicate met acteur Hallo. Hallo communicatiekanaal is automatisch beschikbaar. Zo hoeft u geen toodo alles dat gelijkwaardige tooestablishing is een `ServiceRemotingListener` net zoals voor stateful service Hallo in deze zelfstudie.

## <a name="how-web-services-work-on-your-local-cluster"></a>De werking van web-services op uw lokale cluster
U kunt precies Hallo dezelfde Service Fabric-toepassing tooa meerdere machine cluster die u hebt geïmplementeerd op uw lokale cluster en maximaal vertrouwen werkt zoals verwacht in het algemeen kunt implementeren. Dit is omdat uw lokale cluster is gewoon een vijf knooppunten configuratie die is samengevouwen tooa enkele machine.

Wanneer er tooweb services, maar is er een belangrijke aspect. Als uw cluster zich achter een load balancer, zoals dat in Azure, moet u ervoor zorgen dat uw webservices zijn geïmplementeerd op elke machine sinds Hallo load balancer gewoon round robins verkeer over Hallo-machines. U kunt dit doen door de instelling Hallo `InstanceCount` voor Hallo service toohello speciale waarde '1'.

Daarentegen, wanneer u een webservice lokaal uitvoeren, moet u tooensure dat slechts één exemplaar van Hallo-service wordt uitgevoerd. Anders u uitvoeren in conflicten uit meerdere processen die op Hallo hetzelfde luisteren pad en de poort. Als gevolg hiervan Hallo web service-exemplaren te moet worden ingesteld '1' voor lokale implementaties.

hoe tooconfigure verschillende waarden voor verschillende omgeving zien toolearn [beheren voor omgevingen met meerdere parameters voor de toepassing](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Volgende stappen
Nu dat u een web-front end set hebt voor uw toepassing met ASP.NET Core, meer informatie over [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) voor een diepgaand inzicht in hoe ASP.NET Core met Service Fabric werkt.

Vervolgens [meer informatie over de communicatie met services](service-fabric-connect-and-communicate-with-services.md) in het algemeen tooget een volledige afbeelding van hoe service communicatie werkt in Service Fabric.

Zodra u een goed inzicht hebt in hoe servicecommunicatie werkt, [een cluster in Azure maken en implementeren van uw toepassing toohello cloud](service-fabric-cluster-creation-via-portal.md).

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
