---
title: Service-communicatie met de ASP.NET-Web-API | Microsoft Docs
description: Informatie over het servicecommunicatie stapsgewijze implementeren met behulp van de ASP.NET-Web-API met OWIN zelf host in de betrouwbare Services-API.
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 73b7e1c0cb93ae7c54780a3aab837b0e5bcdb0a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Aan de slag: Service Fabric-Web-API-services met OWIN zelf die als host fungeert
Azure Service Fabric brengt de mogelijkheden in uw handen wanneer u bent bepalen hoe u wilt dat uw services met gebruikers en met elkaar communiceren. Deze zelfstudie richt zich op het gebruik van ASP.NET Web API met Open Web Interface voor .NET (OWIN) host zelf in Service Fabric van betrouwbare Services API servicecommunicatie implementeren. We je dieper diep Reliable Services pluggable communicatie API. We ook gebruiken Web-API in het voorbeeld van een stapsgewijze aan hoe u een aangepaste communicatie-listener instellen.

## <a name="introduction-to-web-api-in-service-fabric"></a>Inleiding tot Web-API in Service Fabric
ASP.NET-Web-API is een populair en krachtige framework voor het bouwen van HTTP-APIs boven op het .NET Framework. Als u niet al bekend met het framework bent, Zie [aan de slag met ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) voor meer informatie.

Web-API in Service Fabric is de dezelfde ASP.NET Web API-u bekend zijn en veel. Het verschil is in hoe u *host* een Web-API-toepassing. Won't u Microsoft Internet Information Services (IIS). Voor meer informatie over het verschil, gaan we dit opsplitsen in twee delen:

1. De Web-API-toepassing (met inbegrip van domeincontrollers en modellen)
2. De host (de webserver, meestal IIS)

Een Web-API-toepassing zelf niet gewijzigd. Het gaat niet anders Web API-toepassingen die u in het verleden hebt gemaakt en moet u kunnen gewoon plaatst u de meeste van uw toepassingscode. Maar als u hebt op IIS, waar u de toepassing mogelijk host enigszins verschillen van bent u gewend om is host. Voordat we u naar de host deel, laten we beginnen met iets meer vertrouwde: de Web-API-toepassing.

## <a name="create-the-application"></a>De toepassing maken
Start een nieuwe Service Fabric-toepassing maken met een enkele staatloze service in Visual Studio 2015.

Visual Studio-sjabloon voor een stateless service met behulp van Web-API is voor u beschikbaar. In deze zelfstudie hebt gaan we verder met een Web API-project maken die resulteert in wat u krijgt als u deze sjabloon hebt geselecteerd.

Selecteer een lege staatloze Service-project voor informatie over het bouwen van een Web API-project maken of u kunt beginnen met een sjabloon voor de staatloze service-Web-API en te volgen.  

De eerste stap is om op te halen in sommige NuGet-pakketten voor Web-API. Het pakket wilt gebruiken is Microsoft.AspNet.WebApi.OwinSelfHost. Dit pakket bevat alle benodigde pakketten voor Web-API en de *host* pakketten. Dit is belangrijk later.

Nadat de pakketten zijn geïnstalleerd, kunt u beginnen opzetten van de basisstructuur van de Web-API-project. Als u Web-API hebt gebruikt, moet de projectstructuur bekend eruitzien. Voeg eerst een `Controllers` directory en een eenvoudige waarden domeincontroller:

**ValuesController.cs**

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

Voeg vervolgens een Opstartklasse toe op de hoofdmap van het project te registreren met de routering, formatters en andere configuratie-instellingen. Dit is ook waar Web-API op aansluit op de *host*, die wordt later opnieuw worden herzien. 

**Startup.cs**

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

Dat is voor de toepassing die deel uitmaken. We hebt op dit moment alleen de Web-API-project basisindeling ingesteld. Tot nu toe, mag niet deze anders zijn veel van de Web API-projecten die u hebt gemaakt in het verleden of van de eenvoudige Web-API-sjabloon. Uw bedrijfslogica gaat zoals gebruikelijk in de controllers en -modellen.

Nu wat we doen over het hosten van zodat we kunnen het daadwerkelijk uitvoeren?

## <a name="service-hosting"></a>Service die als host fungeert
In Service Fabric uw service wordt uitgevoerd in een *service hostproces*, een uitvoerbaar bestand dat uw servicecode wordt uitgevoerd. Bij het schrijven van een service met behulp van de API voor betrouwbare Services compileert uw serviceproject net als een uitvoerbaar bestand dat uw servicetype registreert en uw code wordt uitgevoerd. Dit geldt in de meeste gevallen bij het schrijven van een service in de Service-infrastructuur in .NET. Wanneer u Program.cs in het serviceproject staatloze opent, ziet u op:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Als die eruit ziet verdacht gedraagt het toegangspunt voor een consoletoepassing, gebeurt dit omdat is.

Meer informatie over de hostproces van de service en de serviceregistratie zijn buiten het bereik van dit artikel. Maar het is belangrijk te weten voor nu *uw servicecode wordt uitgevoerd in een eigen proces*.

## <a name="self-host-web-api-with-an-owin-host"></a>Web-API met een OWIN-host zelf hosten
Gezien het feit dat de Web-API-toepassingscode wordt gehost in een eigen proces, hoe u koppelen naar een webserver? Voer [OWIN](http://owin.org/). OWIN is gewoon een overeenkomst tussen .NET-webtoepassingen en webservers. Traditioneel als ASP.NET (maximaal MVC 5) wordt gebruikt, wordt de webtoepassing is nauw aan IIS via System.Web gekoppeld. Web-API implementeert echter OWIN, dus u kunt een webtoepassing die wordt ontkoppeld van de webserver die als host fungeert schrijven. Als gevolg hiervan kunt u een *zelf gehost* OWIN-webserver die u in uw eigen proces kan starten. Hiermee past perfect bij het Service Fabric-hostingmodel dat hierboven wordt beschreven.

In dit artikel gebruiken we Katana als host voor OWIN voor de Web-API-toepassing. Katana is een open source OWIN host implementatie die is gebaseerd op [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) en de Windows [HTTP-Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> Voor meer informatie over Katana, gaat u naar de [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Zie voor een snel overzicht van het Katana gebruiken voor het hosten van Web-API zelf [OWIN gebruiken om te Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-the-web-server"></a>De webserver instellen
De API voor betrouwbare Services biedt een communicatie-toegangspunt waar u communicatie stacks waarmee gebruikers en -clients verbinding maken met de service kunt aansluiten:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

De webserver (en andere communicatiestack die u in de toekomst, zoals WebSockets) moeten de interface ICommunicationListener gebruiken correct integreren met het systeem. De redenen hiervoor worden meer zichtbaar in de volgende stappen.

Maak eerst een klasse met de naam OwinCommunicationListener dat ICommunicationListener implementeert:

**OwinCommunicationListener.cs**

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

De interface ICommunicationListener biedt drie methoden voor het beheren van een communicatie-listener voor uw service:

* *OpenAsync*. Beginnen met luisteren naar aanvragen.
* *CloseAsync*. Stoppen met luisteren naar aanvragen, verzoeken onderweg voltooien en afsluiten.
* *Afbreken*. Alles annuleren en onmiddellijk wilt stoppen.

Toevoegen aan de slag persoonlijke klassenleden voor zaken die de listener moet werken. Deze wordt geïnitialiseerd door middel van de constructor en later wordt gebruikt bij het instellen van de luisterende URL.

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a>OpenAsync implementeren
Als u de webserver instelt, moet u twee soorten informatie:

* *Een URL-voorvoegsel pad*. Hoewel dit optioneel is, is het geschikt is voor u dit nu zo ingesteld dat veilig u meerdere webservices in uw toepassing hosten kunt.
* *Een poort*.

Voordat u een poort voor de webserver krijgen, is het belangrijk dat u begrijpt dat Service Fabric een toepassingslaag die als een buffer tussen uw toepassing en het onderliggende besturingssysteem dat bevat fungeert op wordt uitgevoerd. Als zodanig Service Fabric biedt een manier voor het configureren van *eindpunten* voor uw services. Service Fabric zorgt ervoor dat eindpunten beschikbaar voor uw service zijn te gebruiken. Op deze manier u niet moet ze zelf configureren in de onderliggende OS-omgeving. U kunt eenvoudig uw Service Fabric-toepassing in verschillende omgevingen zonder wijzigingen aanbrengen in uw toepassing hosten. (Bijvoorbeeld, u kunt hosten dezelfde toepassing in Azure of in uw eigen datacenter.)

Een HTTP-eindpunt in PackageRoot\ServiceManifest.xml configureren:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Deze stap is belangrijk, omdat het hostproces van de service wordt uitgevoerd onder beperkte referenties (Network Service in Windows). Dit betekent dat er geen toegang voor het instellen van een HTTP-eindpunt op een eigen uw service. Met behulp van de eindpuntconfiguratie kent Service Fabric voor de URL die de service controleert op voor het instellen van de juiste toegangsbeheerlijst (ACL). Service Fabric biedt ook een standaardlocatie voor het configureren van eindpunten.

Terug in OwinCommunicationListener.cs, kunt u beginnen OpenAsync implementeren. Dit is waar het starten van de webserver. Eerst Lees de eindpuntinformatie voor het en maak de URL waarnaar de service wordt luisteren. De URL is verschillend, afhankelijk van of de listener wordt gebruikt in een stateless service of een stateful service. De listener moet een unieke adres maken voor elke stateful service replica die deze luistert op voor een stateful service. Het adres kan niet veel eenvoudiger voor stateless services. 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

Houd er rekening mee dat 'http://+' Hier wordt gebruikt. Dit is om ervoor te zorgen dat de webserver op alle beschikbare adressen luistert, inclusief localhost, FQDN-naam en het machine IP-adres.

De implementatie van OpenAsync is een van de belangrijkste redenen waarom de webserver (of een communicatiestack) is geïmplementeerd als een ICommunicationListener in plaats van dat deze rechtstreeks vanuit openen `RunAsync()` in de service. De geretourneerde waarde van OpenAsync is het adres dat op de webserver luistert. Als dit adres wordt geretourneerd met het systeem, wordt het adres geregistreerd bij de service. Service Fabric biedt een API waarmee clients en andere services kunnen vervolgens vraagt u voor dit adres met de servicenaam. Dit is belangrijk omdat het serviceadres niet statisch is. Services worden in het cluster voor netwerktaakverdeling en beschikbaarheid doeleinden van resource verplaatst. Dit is het mechanisme waarmee clients kunnen omzetten van het luisterende adres voor een service.

Met die in gedachten OpenAsync Start de webserver en retourneert het adres waarop wordt geluisterd. Opmerking dat deze luistert op 'http://+', maar voordat OpenAsync het adres retourneert, de '+' wordt vervangen door de IP- of FQDN van het knooppunt dat zich momenteel op. Het adres dat wordt geretourneerd door deze methode is wat geregistreerd bij het systeem. Het is ook wat clients en andere services zien wanneer ze voor een service-adres vragen. Voor clients correct verbinding kunnen maken, moeten een werkelijke IP of FQDN-naam in het adres.

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

Houd er rekening mee dat deze verwijst naar het starten van de klasse die is doorgegeven aan de OwinCommunicationListener in de constructor. Dit exemplaar starten wordt gebruikt door de webserver voor de bootstrap van de Web-API-toepassing.

De `ServiceEventSource.Current.Message()` regel wordt weergegeven in het venster diagnostische gebeurtenissen later, wanneer het uitvoeren van de toepassing om te bevestigen dat de webserver is gestart.

## <a name="implement-closeasync-and-abort"></a>Implementeer CloseAsync en afbreken
Ten slotte CloseAsync en afbreken om te stoppen van de webserver worden geïmplementeerd. De webserver kan worden gestopt door de server-ingang die is gemaakt tijdens OpenAsync verwijdering.

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

In deze voorbeeldimplementatie stopt CloseAsync zowel afbreken gewoon u de webserver. U kan ervoor kiezen om een meer probleemloos gecoördineerde afsluiten van de webserver in CloseAsync. Bijvoorbeeld, kan het afsluiten wacht tot onderweg aanvragen om te worden voltooid voordat het rendement.

## <a name="start-the-web-server"></a>Start de webserver
U bent nu klaar om te maken en een exemplaar van OwinCommunicationListener starten van de webserver wordt geretourneerd. Terug in de Service-klasse (WebService.cs), overschrijven de `CreateServiceInstanceListeners()` methode:

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

Dit is wanneer de Web-API *toepassing* en de OWIN *host* ten slotte voldoen aan. De host (OwinCommunicationListener) krijgt een exemplaar van de *toepassing* (Web-API) via het starten van de klasse. Service Fabric worden vervolgens de levenscyclus beheert. Dit patroon kan doorgaans worden gevolgd door een communicatiestack.

## <a name="put-it-all-together"></a>Alles samenvoegen
In dit voorbeeld niet hoeft verder niets te doen de `RunAsync()` methode, zodat deze onderdrukking kan gewoon worden verwijderd.

De laatste service-implementatie moet zeer eenvoudig. Dit hoeft alleen te maken van de listener communicatie:

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

De volledige `OwinCommunicationListener` klasse:

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

Nu dat alle benodigde onderdelen erin hebt geplaatst, wordt uw project moet eruitzien als een typische toepassing Web-API met betrouwbare Services API-toegangspunten en een OWIN-host.

## <a name="run-and-connect-through-a-web-browser"></a>Voer en verbinding maken via een webbrowser
Als u dit nog niet hebt gedaan, [uw ontwikkelomgeving instellen](service-fabric-get-started.md).

U kunt nu bouwen en implementeren van uw service. Druk op **F5** in Visual Studio kunnen bouwen en implementeren van de toepassing. In het venster diagnostische gebeurtenissen ziet u een bericht weergegeven dat aangeeft dat de webserver wordt geopend op http://localhost:8281 /.

> [!NOTE]
> Als de poort is al geopend door een ander proces op uw computer, wordt er een fout hier. Hiermee wordt aangegeven dat de listener kan niet worden geopend. Als dat het geval is, probeert u een andere poort voor de eindpuntconfiguratie in ServiceManifest.xml.
> 
> 

Zodra de service wordt uitgevoerd, open een browser en Ga naar [api-http://localhost:8281-waarden](http://localhost:8281/api/values) te testen.

## <a name="scale-it-out"></a>Het uit te schalen
Staatloze web-apps doorgaans uitbreiden betekent meer machines toe te voegen en van de web-apps op deze draaien. Service Fabric de orchestration-engine kunt dit doen voor u wanneer nieuwe knooppunten worden toegevoegd aan een cluster. Als u exemplaren van een staatloze service maakt, kunt u het aantal exemplaren dat u wilt maken. Service Fabric wordt dat aantal exemplaren op knooppunten in het cluster geplaatst. En ervoor dat u niet meer dan één exemplaar maken op een willekeurig knooppunt maakt. U kunt ook opgeven dat het Service Fabric altijd een exemplaar te maken op elk knooppunt door te geven **-1** voor het aantal exemplaren. Dit zorgt ervoor dat als u knooppunten voor het schalen van uw cluster toevoegt, een exemplaar van uw stateless service wordt gemaakt op de nieuwe knooppunten. Deze waarde is een eigenschap van het service-exemplaar, zodat deze bij het maken van een service-exemplaar is ingesteld. U kunt dit doen via PowerShell:

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

U kunt dit ook doen wanneer u een standaard-service in een Visual Studio-project staatloze service definieert:

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Zie voor meer informatie over het maken van de toepassing en service-exemplaren [implementeren van een toepassing](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Volgende stappen
[Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio](service-fabric-debugging-your-application.md)

