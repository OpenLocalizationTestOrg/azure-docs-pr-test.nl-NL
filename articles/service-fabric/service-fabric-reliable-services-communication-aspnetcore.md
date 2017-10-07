---
title: aaaService communicatie met de Hallo ASP.NET Core | Microsoft Docs
description: Meer informatie over hoe toouse ASP.NET Core in staatloze en stateful Reliable Services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>ASP.NET Core in Service Fabric Reliable Services

ASP.NET Core is een nieuw open source en platformoverschrijdende framework voor het bouwen van moderne cloud-gebaseerde Internet verbonden toepassingen, zoals web-apps, IoT-apps en mobiele back-ends. 

Dit artikel is een uitgebreidere handleiding toohosting ASP.NET Core services in Service Fabric Reliable Services met behulp van Hallo **Microsoft.ServiceFabric.AspNetCore.** * set NuGet-pakketten.

Zie voor een inleidende zelfstudie voor ASP.NET Core in Service Fabric en instructies over het ophalen van uw ontwikkelomgeving instellen [bouwen van een webfront-end voor uw toepassing met behulp van ASP.NET Core](service-fabric-add-a-web-frontend.md).

Hallo rest van dit artikel wordt ervan uitgegaan dat u al bekend bent met ASP.NET Core. Als u niet het geval is, wordt aangeraden lezen via Hallo [ASP.NET Core grondbeginselen](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>ASP.NET Core in Hallo Service Fabric-omgeving

Terwijl ASP.NET Core apps kunnen worden uitgevoerd op .NET Core of volledige .NET Framework, Service Fabric-services momenteel kan alleen worden uitgevoerd op Hallo Hallo volledige .NET Framework. Dit betekent dat wanneer u een ASP.NET Core Service Fabric-service maakt, moet nog steeds gericht Hallo volledige .NET Framework.

ASP.NET Core kunnen worden gebruikt op twee verschillende manieren in Service Fabric:
 - **Als het uitvoerbare bestand van een gast gehost**. Dit is vooral gebruikte toorun bestaande ASP.NET Core toepassingen op Service Fabric zonder wijzigingen code.
 - **Uitgevoerd binnen een betrouwbare Service**. Dit kunt betere integratie met Hallo Service Fabric-runtime en stateful ASP.NET Core services.

Hallo rest van dit artikel wordt uitgelegd hoe toouse ASP.NET Core binnen een betrouwbare Service met ASP.NET Core integratieonderdelen die worden geleverd met Service Fabric SDK Hallo Hallo. 

## <a name="service-fabric-service-hosting"></a>Hosting van service Fabric-service

In Service Fabric, een of meer exemplaren en/of replica's van uw service worden uitgevoerd in een *service hostproces*, een uitvoerbaar bestand dat uw servicecode wordt uitgevoerd. U, als de auteur van een service, de eigenaar hostproces Hallo-service en Service Fabric wordt geactiveerd en controleert u het voor u.

Traditionele ASP.NET (omhoog tooMVC 5) is nauw gekoppeld tooIIS via System.Web.dll. ASP.NET Core biedt een scheiding tussen Hallo-webserver en uw webtoepassing. Hiermee kan de web-toepassingen toobe draagbare tussen verschillende webservers en kunt u ook web servers toobe *zelf gehost*, wat betekent dat u kunt een webserver starten in uw eigen proces als tegengestelde tooa proces dat eigendom is van een specifieke web Server-software zoals IIS. 

U moet in volgorde toocombine een Service Fabric-service en ASP.NET als het uitvoerbare bestand van een gastbesturingssysteem of in een betrouwbare Service kunnen toostart ASP.NET zijn binnen het hostproces van uw service. ASP.NET Core zelf hosten, kunt u toodo dit.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Hosting van ASP.NET Core in een betrouwbare Service
Normaal gesproken zelf gehoste ASP.NET Core toepassingen een WebHost maken in het toegangspunt van een toepassing, zoals Hallo `static void Main()` methode in `Program.cs`. In dit geval is Hallo levenscyclus van Hallo WebHost gebonden toohello levenscyclus van Hallo-proces.

![ASP.NET Core hosten in een proces][0]

Echter ingangspunt voor toepassing hello niet Hallo goede plek toocreate een WebHost in een betrouwbare Service, omdat het ingangspunt Hallo-toepassing wordt alleen gebruikt tooregister een service Typ met Hallo Service Fabric-runtime, zodat deze exemplaren van die service mogelijk maken type. Hallo WebHost moet worden gemaakt in een betrouwbare Service zelf. In hostproces Hallo-service, kunnen service-exemplaren en/of replica's doorlopen die meerdere levenscycli. 

Een betrouwbare Service-exemplaar wordt vertegenwoordigd door uw serviceklasse die zijn afgeleid van `StatelessService` of `StatefulService`. Hallo communicatiestack voor een service deel uitmaakt van een `ICommunicationListener` -implementatie in uw serviceklasse. Hallo `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet-pakketten bevatten implementaties van `ICommunicationListener` die starten en te beheren Hallo ASP.NET Core WebHost voor Kestrel of WebListener in een betrouwbare Service.

![Hosting van ASP.NET Core in een betrouwbare Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a>ASP.NET Core ICommunicationListeners
Hallo `ICommunicationListener` implementaties voor Kestrel en WebListener in Hallo `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet-pakketten vergelijkbare gebruikspatronen hebben maar enigszins andere acties specifieke tooeach webserver uitvoeren. 

Beide communicatielisteners bieden een constructor die Hallo volgende argumenten:
 - **`ServiceContext serviceContext`**: Hallo `ServiceContext` object dat informatie bevat over Hallo waarop service wordt uitgevoerd.
 - **`string endpointName`**: Hallo-naam van een `Endpoint` configuratie in ServiceManifest.xml. Dit is vooral waar Hallo twee communicatielisteners verschillen: WebListener **vereist** een `Endpoint` configuratie, maar niet door Kestrel.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: een lambda die u implementeert in die u maakt en retourneren een `IWebHost`. Hiermee kunt u tooconfigure `IWebHost` Hallo manier u dat gewend bent in een toepassing ASP.NET Core. Hallo lambda biedt een URL die wordt gegenereerd voor u, afhankelijk van de Service Fabric-integratie Hallo u opties gebruik en Hallo `Endpoint` configuratie die u opgeeft. Dat URL vervolgens kan worden gewijzigd of als gebruikt-toostart Hallo web server.

## <a name="service-fabric-integration-middleware"></a>Service Fabric-integratie middleware
Hallo `Microsoft.ServiceFabric.Services.AspNetCore` NuGet-pakket bevat Hallo `UseServiceFabricIntegration` extensiemethode op `IWebHostBuilder` die Service Fabric-bewuste middleware toevoegt. Deze middleware configureert Hallo Kestrel of WebListener `ICommunicationListener` tooregister een unieke service-URL met Service Fabric Naming Service Hallo en controleert vervolgens client aanvragen tooensure clients verbinding maken toohello juiste service. Dit is nodig in een omgeving met gedeelde host zoals Service Fabric, waarbij meerdere webtoepassingen kunnen uitvoeren op Hallo dezelfde fysieke of virtuele machine, maar gebruik geen unieke hostnamen tooprevent clients per ongeluk de verkeerde service toohello verbinding kunnen maken. Dit scenario wordt beschreven in de volgende sectie Hallo nader.

### <a name="a-case-of-mistaken-identity"></a>Een aanvraag van onjuiste identiteit
Service-replica's, ongeacht het protocol, luisteren op de combinatie van een uniek IP: poort. Wanneer een replica van de service is begonnen met luisteren op een eindpunt IP: poort, rapporteert dat eindpunt adres toohello Service Fabric Naming Service waar deze kan worden gedetecteerd door clients of andere services. Als u services gebruiken toepassing dynamisch toegewezen poorten, een service-replica kunnen tegelijk gebruiken hetzelfde IP: poort eindpunt van een andere service die voorheen op Hallo Hallo dezelfde fysieke of virtuele machine. Dit kan ertoe leiden dat een client toomistakely verbinding maken met de verkeerde toohello-service. Dit kan gebeuren als de volgende reeks gebeurtenissen Hallo optreden:

 1. Een service luistert op 10.0.0.1:30000 via HTTP. 
 2. Client-Service A wordt omgezet en adres 10.0.0.1:30000 opgehaald
 3. Een ander knooppunt voor verplaatst tooa-service.
 4. Service B 10.0.0.1 is geplaatst en tegelijk maakt gebruik van dezelfde poort 30000 Hallo.
 5. Client probeert tooconnect tooservice A met het adres in cache 10.0.0.1:30000.
 6. Client is nu is verbonden tooservice geen B is verbonden toohello verkeerde service.

Dit kan fouten veroorzaken op willekeurige tijdstippen die moeilijk toodiagnose kunnen zijn. 

### <a name="using-unique-service-urls"></a>Met unieke service-URL 's
tooprevent deze services kunt plaatsen van een eindpunt toohello Naming Service met een unieke id en vervolgens valideren die de unieke id tijdens het aanvragen van clients. Dit is een gezamenlijke actie tussen services in een vertrouwde omgeving van niet-onveilige-tenant. Dit biedt geen verificatie van de beveiligde service in een onveilige tenant-omgeving.

In een vertrouwde omgeving Hallo middleware die wordt toegevoegd door Hallo `UseServiceFabricIntegration` methode automatisch een unieke id toohello-adres dat wordt gepost toohello Naming Service en valideert die bij elke aanvraag-id worden toegevoegd. Als het Hallo-id komt niet overeen met, retourneert Hallo middleware onmiddellijk een antwoord HTTP 410 geworden.

Services die gebruikmaken van een dynamisch toegewezen poort moet maken gebruik van deze middleware.

Services die gebruikmaken van een vaste unieke poort hoeft dit probleem niet in een gezamenlijke omgeving. Een unieke vaste poort wordt doorgaans gebruikt voor extern gerichte services die voor client toepassingen tooconnect naar een bekende poort nodig hebt. Bijvoorbeeld: de meeste internetgerichte webtoepassingen poort 80 of 443 gebruikt voor web browser verbindingen. In dit geval wordt worden de unieke id Hallo niet ingeschakeld.

Hallo volgende diagram toont Hallo aanvragen bewegen met Hallo middleware ingeschakeld:

![Service Fabric ASP.NET Core-integratie][2]

Zowel Kestrel als WebListener `ICommunicationListener` implementaties gebruikt dit mechanisme in exact Hallo dezelfde manier. Hoewel WebListener kunt aanvragen op basis van unieke URL-paden met onderliggende hello intern onderscheiden *http.sys* poort functie die de functionaliteit voor het delen *niet* die wordt gebruikt door Hallo WebListener `ICommunicationListener` implementatie omdat die in een HTTP 503- en HTTP 404 status foutcodes in Hallo scenario eerder beschreven resulteert. Op zijn beurt waardoor het moeilijk voor clients toodetermine Hallo bedoeling van Hallo fout, zoals HTTP 503- en HTTP 404 al veelgebruikte tooindicate zijn andere fouten. Dus zowel Kestrel en WebListener `ICommunicationListener` implementaties standaardiseren op Hallo middleware geleverd door Hallo `UseServiceFabricIntegration` uitbreidingsmethode zodat clients alleen een service-eindpunt tooperform hoeft te zetten actie op 410 HTTP-antwoorden.

## <a name="weblistener-in-reliable-services"></a>WebListener in Reliable Services
WebListener kan worden gebruikt in een betrouwbare Service door het importeren van Hallo **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet-pakket. Dit pakket bevat `WebListenerCommunicationListener`, een implementatie van `ICommunicationListener`, waarmee u een ASP.NET Core WebHost binnen een betrouwbare Service toocreate WebListener gebruikt als Hallo-webserver.

WebListener is gebouwd op Hallo [Windows HTTP-Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). Dit maakt gebruik van Hallo *http.sys* kernel-stuurprogramma die wordt gebruikt door IIS tooprocess HTTP-aanvragen en versturen ze tooprocesses waarop webtoepassingen worden uitgevoerd. Hierdoor kunnen meerdere processen op Hallo dezelfde fysieke of virtuele machine toohost webtoepassingen op Hallo dezelfde poort, ondubbelzinnig gemaakt door een unieke URL-pad of de hostnaam. Deze functies zijn handig in Service Fabric voor het hosten van meerdere websites in Hallo hetzelfde cluster.

Hallo volgende diagram illustreert hoe WebListener Hallo gebruikt *http.sys* kernel-stuurprogramma in Windows voor het delen van poort:

![HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>WebListener in een stateless service
toouse `WebListener` in een stateless service overschrijven Hallo `CreateServiceInstanceListeners` methode en retourneren een `WebListenerCommunicationListener` exemplaar:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>WebListener in een stateful service

`WebListenerCommunicationListener`op dit moment niet is ontworpen voor gebruik in stateful services vanwege toocomplications met onderliggende hello *http.sys* poort functie voor het delen. Zie volgende sectie op dynamische poorttoewijzing met WebListener Hallo voor meer informatie. Voor stateful services is Kestrel Hallo aanbevolen webserver.

### <a name="endpoint-configuration"></a>Endpoint-configuratie

Een `Endpoint` configuratie is vereist voor webservers die gebruikmaken van Hallo Windows HTTP-Server API, met inbegrip van WebListener. Webservers die gebruikmaken van Windows HTTP-Server API Hallo moeten eerst hun URL met reserveren *http.sys* (dit is normaal gesproken bewerkstelligd met Hallo [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool). Deze actie is vereist voor verhoogde bevoegdheden die uw services standaard geen hebben. Hallo 'http' of 'https'-opties voor Hallo `Protocol` eigenschap Hallo `Endpoint` configuratie in *ServiceManifest.xml* worden gebruikt specifiek tooinstruct Hallo Service Fabric-runtime tooregister een URL met *http.sys* namens jou Hallo met [ *sterk jokertekens* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL-voorvoegsel.

Bijvoorbeeld: tooreserve `http://+:80` voor een service hello volgende configuratie moet worden gebruikt in ServiceManifest.xml:

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

En de naam van het eindpunt Hallo toohello moet worden doorgegeven `WebListenerCommunicationListener` constructor:

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>WebListener gebruiken met een statische poort
toouse een statische poort met WebListener, geef Hallo poortnummer in Hallo `Endpoint` configuratie:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>WebListener gebruiken met een dynamische poort
een dynamisch toegewezen poort met WebListener, toouse weglaten Hallo `Port` eigenschap in Hallo `Endpoint` configuratie:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Merk op dat een dynamische poort is toegewezen door een `Endpoint` configuratie biedt slechts één poort *per hostproces*. Hallo huidige Service Fabric hostingmodel meerdere service-exemplaren en/of replica's toobe gehost in Hallo kunt dezelfde verwerken, wat betekent dat elke dezelfde poort delen als toegewezen via Hallo Hallo `Endpoint` configuratie. Meerdere exemplaren van WebListener kunnen delen een poort met onderliggende hello *http.sys* poort delen onderdeel, maar die niet wordt ondersteund door `WebListenerCommunicationListener` vanwege toohello problemen hierdoor voor clientaanvragen. Voor het gebruik van dynamische poort is Kestrel Hallo aanbevolen webserver.

## <a name="kestrel-in-reliable-services"></a>Kestrel in Reliable Services
Kestrel kan worden gebruikt in een betrouwbare Service door het importeren van Hallo **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet-pakket. Dit pakket bevat `KestrelCommunicationListener`, een implementatie van `ICommunicationListener`, waarmee u een ASP.NET Core WebHost binnen een betrouwbare Service toocreate Kestrel gebruikt als Hallo-webserver.

Kestrel is dat een platformoverschrijdende webserver voor ASP.NET Core op basis van libuv, een platformoverschrijdende asynchrone i/o-bibliotheek. In tegenstelling tot WebListener, Kestrel gebruikt geen een gecentraliseerde eindpunt manager zoals *http.sys*. En in tegenstelling tot WebListener, Kestrel biedt geen ondersteuning voor poort delen tussen meerdere processen. Elk exemplaar van Kestrel moet een unieke poort gebruiken.

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Kestrel in een stateless service
toouse `Kestrel` in een stateless service overschrijven Hallo `CreateServiceInstanceListeners` methode en retourneren een `KestrelCommunicationListener` exemplaar:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>Kestrel in een stateful service
toouse `Kestrel` in een stateful service overschrijven Hallo `CreateServiceReplicaListeners` methode en retourneren een `KestrelCommunicationListener` exemplaar:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

In dit voorbeeld wordt een singleton-instantie van `IReliableStateManager` toohello WebHost afhankelijkheid injectie container is opgegeven. Dit is niet strikt noodzakelijk zijn, maar kunt u toouse `IReliableStateManager` en betrouwbare verzamelingen in uw MVC-controller-actiemethoden.

Houd er rekening mee dat een `Endpoint` configuratienaam is **niet** te opgegeven`KestrelCommunicationListener` in een stateful service. Dit wordt nader beschreven in de volgende sectie Hallo uitgelegd.

### <a name="endpoint-configuration"></a>Endpoint-configuratie
Een `Endpoint` configuratie is niet vereist toouse Kestrel. 

Kestrel is een eenvoudige zelfstandige webserver; in tegenstelling tot WebListener (of HttpListener), hoeft deze niet een `Endpoint` configuratie in *ServiceManifest.xml* omdat er geen URL registratie eerdere toostarting nodig. 

#### <a name="use-kestrel-with-a-static-port"></a>Kestrel gebruiken met een statische poort
Een statische poort kan worden geconfigureerd in Hallo `Endpoint` ServiceManifest.xml-configuratie voor gebruik met Kestrel. Hoewel dit niet strikt noodzakelijk is, heeft deze twee mogelijke voordelen:
 1. Als Hallo poort niet in Hallo toepassingspoortbereik valt, wordt dit door de Service Fabric via Hallo OS firewall geopend.
 2. Hallo-URL opgegeven tooyou via `KestrelCommunicationListener` deze poort wordt gebruikt.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Als een `Endpoint` is geconfigureerd, de naam moet worden doorgegeven in Hallo `KestrelCommunicationListener` constructor: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Als een `Endpoint` configuratie wordt niet gebruikt, laat u Hallo-naam in Hallo `KestrelCommunicationListener` constructor. In dit geval wordt een dynamische poort gebruikt. Zie de volgende sectie Hallo voor meer informatie.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Kestrel gebruiken met een dynamische poort
Kestrel hello automatische poorttoewijzing van Hallo niet gebruiken `Endpoint` configuratie in ServiceManifest.xml, omdat automatische poorttoewijzing van een `Endpoint` configuratie wijst een unieke poort per *hosten proces* , en een proces voor één host meerdere exemplaren van Kestrel kan bevatten. Aangezien Kestrel biedt geen ondersteuning voor het delen van de poort, werkt dit niet zoals elk exemplaar Kestrel moet worden geopend op een unieke poort.

toewijzing van de dynamische poort toouse met Kestrel, weglaten gewoon Hallo `Endpoint` configuratie in ServiceManifest.xml volledig, en een eindpunt naam toohello niet doorgegeven `KestrelCommunicationListener` constructor:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

In deze configuratie `KestrelCommunicationListener` automatisch een niet-gebruikte poort van Hallo toepassingspoortbereik selecteert.

## <a name="scenarios-and-configurations"></a>Scenario's en configuraties
Deze sectie wordt beschreven Hallo volgen scenario's en biedt Hallo aanbevolen combinatie van de webserver, poortconfiguratie, opties voor Service Fabric-integratie en diverse instellingen tooachieve een service naar behoren werkt:
 - Extern blootgesteld ASP.NET Core staatloze service
 - Alleen intern-ASP.NET Core staatloze service
 - Alleen intern-ASP.NET Core stateful service

Een **extern blootgesteld** -service maakt dat toegang biedt tot een eindpunt dat bereikbaar is vanaf buiten Hallo-cluster, meestal via een load balancer.

Een **alleen interne** -service is een waarvan eindpunt alleen bereikbaar is vanaf binnen Hallo-cluster is.

> [!NOTE]
> Stateful service eindpunten in het algemeen niet moeten worden blootgesteld toohello Internet. Clusters die zich achter de load balancers die zich niet bewust zijn van de oplossing van het Service Fabric-service, zoals hello Azure Load Balancer worden stateful services kan geen tooexpose omdat Hallo load balancer wordt niet kunnen toolocate en toohello verkeer routeren de replica van de juiste stateful service. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>Extern blootgesteld ASP.NET Core stateless services
WebListener wordt aanbevolen webserver voor de front-end-services die externe, internetgerichte HTTP-eindpunten op Windows hello. Dit biedt betere bescherming tegen aanvallen en functies die Kestrel niet, zoals Windows-verificatie en -poort delen bestaat ondersteunt. 

Kestrel wordt niet ondersteund als een edge (internetgerichte)-server op dit moment. Een reverse proxy-server zoals IIS of Nginx moet worden gebruikt toohandle verkeer van Hallo openbare Internet.
 
Wanneer moet blootgestelde toohello Internet, een stateless service een bekende en stabiele eindpunt dat bereikbaar is via een load balancer gebruiken. Dit is Hallo-URL die u biedt toousers van uw toepassing. Hallo na configuratie wordt aanbevolen:

|  |  | **Opmerkingen bij de** |
| --- | --- | --- |
| Webserver | WebListener | Als Hallo-service alleen weergegeven tooa vertrouwd netwerk, een intranet wordt kan Kestrel worden gebruikt. Anders is WebListener Hallo voorkeurs-optie. |
| Poortconfiguratie | Statische | Een bekende statische poort moet worden geconfigureerd in Hallo `Endpoints` configuratie van ServiceManifest.xml, zoals 80 voor HTTP en 443 voor HTTPS. |
| ServiceFabricIntegrationOptions | Geen | Hallo `ServiceFabricIntegrationOptions.None` moet worden gebruikt bij het configureren van Service Fabric-integratie middleware zodat Hallo-service niet toovalidate binnenkomende aanvragen voor een unieke id probeert. Externe gebruikers van uw toepassing weet niet Hallo unieke identificatiegegevens door Hallo middleware gebruikt. |
| Aantal exemplaren | -1 | In een typische gebruiksvoorbeelden Hallo-exemplaren instellen te moet worden ingesteld-"1" zodat er een exemplaar is beschikbaar op alle knooppunten die verkeer van een load balancer ontvangt. |

Als meerdere extern blootgestelde services dezelfde knooppunten set hello delen, kan een unieke maar stabiele URL-pad moet worden gebruikt. Dit kan worden bereikt door het Hallo-URL opgegeven tijdens het configureren van IWebHost wijzigen. Houd er rekening mee dat dit tooWebListener alleen van toepassing is.

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>Alleen intern staatloze ASP.NET Core-service
Stateless services die alleen worden aangeroepen vanuit binnen Hallo cluster unieke URL's moeten gebruiken en dynamisch toegewezen poorten tooensure samenwerking tussen meerdere services. Hallo na configuratie wordt aanbevolen:

|  |  | **Opmerkingen bij de** |
| --- | --- | --- |
| Webserver | kestrel | Hoewel WebListener kan worden gebruikt voor interne stateless services, is het Kestrel Hallo aanbevolen server tooallow meerdere service-exemplaren tooshare een host.  |
| Poortconfiguratie | dynamisch toegewezen | Meerdere replica's van een stateful service kunnen een hostproces of hostbesturingssysteem delen en moeten dus unieke poorten. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Bij toewijzing van de dynamische poort is deze instelling voorkomt dat Hallo verward identiteit probleem die eerder zijn beschreven. |
| InstanceCount | alle | Hallo-exemplaren instellen kan tooany waarde nodig toooperate Hallo service worden ingesteld. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Alleen intern stateful ASP.NET Core-service
Stateful services die alleen worden aangeroepen vanuit binnen Hallo cluster moeten dynamisch toegewezen poorten tooensure samenwerking tussen meerdere services gebruiken. Hallo na configuratie wordt aanbevolen:

|  |  | **Opmerkingen bij de** |
| --- | --- | --- |
| Webserver | kestrel | Hallo `WebListenerCommunicationListener` is niet ontworpen voor gebruik door stateful services waarin de replica's een hostproces delen. |
| Poortconfiguratie | dynamisch toegewezen | Meerdere replica's van een stateful service kunnen een hostproces of hostbesturingssysteem delen en moeten dus unieke poorten. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Bij toewijzing van de dynamische poort is deze instelling voorkomt dat Hallo verward identiteit probleem die eerder zijn beschreven. |

## <a name="next-steps"></a>Volgende stappen
[Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
