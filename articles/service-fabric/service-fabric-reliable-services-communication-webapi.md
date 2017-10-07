---
title: aaaService communicatie met de Hallo ASP.NET Web API | Microsoft Docs
description: Meer informatie over hoe tooimplement servicecommunicatie stapsgewijze met behulp van ASP.NET Web API Hallo met OWIN host zelf in Hallo betrouwbare Services-API.
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
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Aan de slag: Service Fabric-Web-API-services met OWIN zelf die als host fungeert
Azure Service Fabric activeert Hallo power in de hand wanneer u bent bepalen hoe u uw toocommunicate services wilt met gebruikers en met elkaar. Deze zelfstudie richt zich op het gebruik van ASP.NET Web API met Open Web Interface voor .NET (OWIN) host zelf in Service Fabric van betrouwbare Services API servicecommunicatie implementeren. We je dieper diep Hallo Reliable Services pluggable communicatie API. Gebruiken we Web-API in een voorbeeld van stapsgewijze tooshow u hoe tooset een aangepaste communicatie-listener geïnstalleerd.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Inleiding tooWeb API in Service Fabric
ASP.NET-Web-API is een populair en krachtige framework voor het bouwen van HTTP APIs boven op Hallo .NET Framework. Als u niet al bekend met het Hallo-framework bent, Zie [aan de slag met ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn meer.

Web-API in Service Fabric is dezelfde ASP.NET Web API u bekend zijn en veel Hallo. Hallo verschil is in hoe u *host* een Web-API-toepassing. Won't u Microsoft Internet Information Services (IIS). toobetter hello verschil, het laten we splitsen in twee onderdelen:

1. Hallo-Web-API-toepassing (met inbegrip van domeincontrollers en modellen)
2. Hallo-host (Hallo webserver, meestal IIS)

Een Web-API-toepassing zelf niet gewijzigd. Het gaat niet anders Web API-toepassingen die u hebt gemaakt in de afgelopen Hallo en moet u kunnen toosimply verplaatsen via de meeste van uw toepassingscode. Maar als u hebt hosten op IIS, waar het hosten van de toepassing hello mogelijk enigszins verschillen van wat je zoekt gebruikt voor. Voordat we u toohello onderdeel hosten, laten we beginnen met iets meer vertrouwde: Hallo Web API-toepassing.

## <a name="create-hello-application"></a>Hallo-toepassing maken
Start een nieuwe Service Fabric-toepassing maken met een enkele staatloze service in Visual Studio 2015.

Visual Studio-sjabloon voor een stateless service met behulp van Web-API is beschikbaar tooyou. In deze zelfstudie hebt gaan we verder met een Web API-project maken die resulteert in wat u krijgt als u deze sjabloon hebt geselecteerd.

Selecteer een lege toolearn staatloze Service-project hoe toobuild een Web API-project maakt, of u kunt beginnen met Hallo staatloze service-Web-API-sjabloon en te volgen.  

de eerste stap Hallo is toopull in sommige NuGet-pakketten voor Web-API. Hallo-pakket willen we toouse is Microsoft.AspNet.WebApi.OwinSelfHost. Dit pakket bevat alle Hallo nodig Web API-pakketten en Hallo *host* pakketten. Dit is belangrijk later.

Nadat hello-pakketten zijn geïnstalleerd, kunt u het opzetten van Hallo Web API-project basisstructuur beginnen. Als u Web-API hebt gebruikt, moet de structuur project Hallo bekend eruitzien. Voeg eerst een `Controllers` directory en een eenvoudige waarden domeincontroller:

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

Voeg vervolgens een Opstartklasse op Hallo project hoofdmap tooregister Hallo routering, formatters en andere configuratie-instellingen. Dit is ook waar u Web-API op toohello aansluit *host*, die wordt later opnieuw worden herzien. 

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

Dat is voor het toepassingsonderdeel Hallo. We hebt op dit moment alleen Hallo Web API-project basisindeling ingesteld. Tot nu toe, mag niet deze anders zijn veel van de Web API-projecten die u hebt gemaakt in de afgelopen Hallo of Hallo basic Web API-sjabloon. Uw bedrijfslogica gaat zoals gebruikelijk in Hallo-controllers en -modellen.

Nu wat we doen over het hosten van zodat we kunnen het daadwerkelijk uitvoeren?

## <a name="service-hosting"></a>Service die als host fungeert
In Service Fabric uw service wordt uitgevoerd in een *service hostproces*, een uitvoerbaar bestand dat uw servicecode wordt uitgevoerd. Bij het schrijven van een service met behulp van Hallo betrouwbare Services API compileert uw serviceproject NET tooan uitvoerbaar bestand dat uw servicetype registreert en uw code wordt uitgevoerd. Dit geldt in de meeste gevallen bij het schrijven van een service in de Service-infrastructuur in .NET. Wanneer u Program.cs in Hallo staatloze serviceproject opent, ziet u op:

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

Als dat verdacht gedraagt ziet eruit als Hallo vermelding punt tooa-consoletoepassing, gebeurt dit omdat is.

Meer informatie over Hallo hostproces van de service en registratie van service zijn buiten bereik Hallo van dit artikel. Maar het is belangrijk tooknow voor nu *uw servicecode wordt uitgevoerd in een eigen proces*.

## <a name="self-host-web-api-with-an-owin-host"></a>Web-API met een OWIN-host zelf hosten
Gezien het feit dat de Web-API-toepassingscode wordt gehost in een eigen proces, hoe u koppelen tooa webserver? Voer [OWIN](http://owin.org/). OWIN is gewoon een overeenkomst tussen .NET-webtoepassingen en webservers. Bij gebruik van ASP.NET (omhoog tooMVC 5) is Hallo webtoepassing oudsher nauw gekoppeld tooIIS via System.Web. Web-API implementeert echter OWIN, dus u kunt een webtoepassing die wordt ontkoppeld schrijven van Hallo-webserver die als host fungeert. Als gevolg hiervan kunt u een *zelf gehost* OWIN-webserver die u in uw eigen proces kan starten. Hiermee past perfect bij Hallo Service Fabric hostingmodel die hierboven wordt beschreven.

In dit artikel gebruiken we Katana als Hallo OWIN host voor Web-API-toepassing hello. Katana is een open source OWIN host implementatie die is gebaseerd op [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) en Windows hello [HTTP-Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> meer informatie over Katana, Ga toohello toolearn [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Voor een snel overzicht van hoe toouse Katana tooself host Web-API, Zie [gebruik OWIN tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Hallo webserver instellen
Hallo betrouwbare Services API biedt een communicatie-toegangspunt waar u communicatie stacks waarmee gebruikers en clients tooconnect toohello service kunt aansluiten:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

Hallo webserver (en andere communicatiestack die u in toekomstige zoals WebSockets Hallo) te gebruiken Hallo ICommunicationListener interface toointegrate correct met Hallo-systeem. Hallo redenen hiervoor worden duidelijker in Hallo stappen te volgen.

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

Hallo ICommunicationListener interface biedt drie methoden toomanage een communicatie-listener voor uw service:

* *OpenAsync*. Beginnen met luisteren naar aanvragen.
* *CloseAsync*. Stoppen met luisteren naar aanvragen, verzoeken onderweg voltooien en afsluiten.
* *Afbreken*. Alles annuleren en onmiddellijk wilt stoppen.

tooget gestart, persoonlijke klasseleden toevoegen voor dingen Hallo listener moet toofunction. Deze wordt geïnitialiseerd via Hallo constructor en later wordt gebruikt bij het instellen van Hallo URL luisteren.

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
tooset Hallo-webserver, moet u twee soorten informatie:

* *Een URL-voorvoegsel pad*. Hoewel dit optioneel is, is het geschikt is voor u tooset deze nu omhoog zodat u meerdere webservices veilig in uw toepassing hosten kunt.
* *Een poort*.

Voordat u een poort voor de webserver Hallo ontvangt, is het belangrijk dat u begrijpt dat Service Fabric een toepassingslaag die als een buffer tussen uw toepassing en het Hallo onderliggende besturingssysteem dat bevat fungeert op wordt uitgevoerd. Als zodanig Service Fabric biedt een manier tooconfigure *eindpunten* voor uw services. Service Fabric zorgt ervoor dat eindpunten beschikbaar voor uw service toouse zijn. Deze manier kunnen er geen tooconfigure ze zelf in Hallo onderliggende OS-omgeving. U kunt eenvoudig uw Service Fabric-toepassing in verschillende omgevingen zonder toomake alle wijzigingen tooyour toepassingen hosten. (Bijvoorbeeld, u kunt hosten Hallo dezelfde toepassing in Azure of in uw eigen datacenter.)

Een HTTP-eindpunt in PackageRoot\ServiceManifest.xml configureren:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Deze stap is belangrijk omdat hostproces Hallo-service wordt uitgevoerd onder beperkte referenties (Network Service in Windows). Dit betekent dat uw service geen toegang tooset u een HTTP-eindpunt op zichzelf hebt. Met behulp van de eindpuntconfiguratie hello, Service Fabric tooset up Hallo juiste toegangsbeheerlijst (ACL) voor de URL die Hallo service luistert op Hallo kent. Service Fabric biedt ook een standaardlocatie tooconfigure eindpunten.

Terug in OwinCommunicationListener.cs, kunt u beginnen OpenAsync implementeren. Dit is waar u de webserver Hallo begint. Eerst Hallo eindpuntinformatie ophalen en Hallo-URL die Hallo-service controleert op maken. Hallo-URL is verschillend, afhankelijk van of Hallo-listener wordt gebruikt in een stateless service of een stateful service. Voor een stateful service moet Hallo listener toocreate een unieke adres voor elke replica stateful service deze luistert op. Hallo-adres kan wel veel eenvoudiger voor stateless services. 

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

Houd er rekening mee dat 'http://+' Hier wordt gebruikt. Dit is toomake ervoor dat de dat webserver Hallo luistert op alle beschikbare adressen, inclusief localhost, FQDN-naam en IP-Hallo-machine.

Hallo OpenAsync implementatie is een van de belangrijkste redenen Hallo waarom Hallo webserver (of een communicatiestack) is geïmplementeerd als een ICommunicationListener in plaats van dat deze rechtstreeks vanuit openen `RunAsync()` in Hallo-service. Hallo geretourneerde waarde van OpenAsync is Hallo-adres dat webserver Hallo luistert op. Als dit adres wordt toohello system geretourneerd, registreert het Hallo-adres met Hallo-service. Service Fabric bevat een API waarmee clients en andere services toothen vragen voor dit adres met de servicenaam. Dit is belangrijk omdat Hallo-serviceadres niet statisch is. Services worden in Hallo cluster voor netwerktaakverdeling en beschikbaarheid doeleinden van resource verplaatst. Dit is Hallo-mechanisme waarmee clients tooresolve Hallo adres voor een service luistert.

Met die in gedachten OpenAsync Hallo webserver wordt gestart en retourneert Hallo-adres dat deze luistert op. Houd er rekening mee dat deze op 'http://+ luistert', maar voordat OpenAsync wordt geretourneerd Hallo-adres, Hallo ' + ' wordt vervangen door Hallo IP of FQDN van Hallo knooppunt zich momenteel op. Hallo-adres dat wordt geretourneerd door deze methode is wat geregistreerd bij Hallo-systeem. Het is ook wat clients en andere services zien wanneer ze voor een service-adres vragen. Voor clients toocorrectly verbinding tooit, moeten deze een werkelijke IP of FQDN Hallo-adres.

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
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

Houd er rekening mee dat deze verwijst naar Hallo-Opstartklasse toohello OwinCommunicationListener in Hallo-constructor is doorgegeven. Dit exemplaar starten wordt gebruikt door Hallo web server toobootstrap Hallo Web API-toepassing.

Hallo `ServiceEventSource.Current.Message()` regel wordt weergegeven in Hallo diagnostische gebeurtenissen venster later bij het uitvoeren van Hallo toepassing tooconfirm Hallo webserver is gestart.

## <a name="implement-closeasync-and-abort"></a>Implementeer CloseAsync en afbreken
Ten slotte implementeren CloseAsync zowel afbreken toostop Hallo-webserver. Hallo-webserver kan worden gestopt door Hallo server ingang die is gemaakt tijdens OpenAsync verwijdering.

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

In deze voorbeeldimplementatie CloseAsync zowel afbreken gewoon Hallo webserver stoppen. U kunt ervoor kiezen tooperform meer probleemloos gecoördineerde afsluiten van de webserver Hallo in CloseAsync. Hallo afsluiten kan bijvoorbeeld, wacht u totdat onderweg aanvragen toobe voltooid voordat Hallo retourneren.

## <a name="start-hello-web-server"></a>Hallo-webserver starten
U bent nu klaar toocreate en een OwinCommunicationListener toostart Hallo webserver-exemplaar geretourneerd. Terug in Hallo serviceklasse (WebService.cs), overschrijven Hallo `CreateServiceInstanceListeners()` methode:

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

Dit is waar de Web-API Hallo *toepassing* en OWIN Hallo *host* ten slotte voldoen aan. Hallo-host (OwinCommunicationListener) krijgt een exemplaar van Hallo *toepassing* (Web-API) via Hallo Opstartklasse. Service Fabric worden vervolgens de levenscyclus beheert. Dit patroon kan doorgaans worden gevolgd door een communicatiestack.

## <a name="put-it-all-together"></a>Alles samenvoegen
In dit voorbeeld, u hoeft niet toodo alles in Hallo `RunAsync()` methode, zodat deze onderdrukking kan gewoon worden verwijderd.

de laatste implementatie Hallo moet zeer eenvoudig. Alleen moet toocreate Hallo communicatie listener:

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

Hallo voltooid `OwinCommunicationListener` klasse:

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
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

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

Nu dat alle Hallo stukken erin hebt geplaatst, wordt uw project moet eruitzien als een typische toepassing Web-API met betrouwbare Services API-toegangspunten en een OWIN-host.

## <a name="run-and-connect-through-a-web-browser"></a>Voer en verbinding maken via een webbrowser
Als u dit nog niet hebt gedaan, [uw ontwikkelomgeving instellen](service-fabric-get-started.md).

U kunt nu bouwen en implementeren van uw service. Druk op **F5** in Visual Studio toobuild toepassing hello en implementeren. Hallo diagnostische gebeurtenissen venster ziet u een bericht weergegeven dat Hallo webserver geopend op http://localhost:8281 aangeeft /.

> [!NOTE]
> Als het Hallo-poort is al geopend door een ander proces op uw computer, ziet u mogelijk een fout hier. Hiermee wordt aangegeven dat Hallo-listener kan niet worden geopend. Als dat Hallo geval is, kunt u met behulp van een andere poort voor de eindpuntconfiguratie Hallo in ServiceManifest.xml.
> 
> 

Zodra het Hallo-service wordt uitgevoerd, open een browser en te navigeren[api-http://localhost:8281-waarden](http://localhost:8281/api/values) tootest deze.

## <a name="scale-it-out"></a>Het uit te schalen
Staatloze web-apps doorgaans uitbreiden betekent meer machines toe te voegen en up Hallo web-apps op deze draaien. Service Fabric de orchestration-engine kunt dit doen voor u wanneer nieuwe knooppunten tooa cluster worden toegevoegd. Als u exemplaren van een staatloze service maakt, kunt u Hallo-nummer opgeven van exemplaren die u wilt toocreate. Service Fabric wordt dat aantal exemplaren op knooppunten in cluster Hallo geplaatst. En op deze manier niet toocreate meer dan één exemplaar op een willekeurig knooppunt. U kunt ook opgeven dat het Service Fabric tooalways geen exemplaar maken op elk knooppunt door te geven **-1** voor Hallo-exemplaren. Dit zorgt ervoor dat als u knooppunten tooscale uit het cluster toevoegt, een exemplaar van uw stateless service wordt gemaakt op Hallo nieuwe knooppunten. Deze waarde is een eigenschap van de service-exemplaar hello, zodat deze bij het maken van een service-exemplaar is ingesteld. U kunt dit doen via PowerShell:

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

Voor meer informatie over hoe toocreate toepassing en service-exemplaren zien [implementeren van een toepassing](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Volgende stappen
[Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio](service-fabric-debugging-your-application.md)

