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
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="3bb40-103">Aan de slag: Service Fabric-Web-API-services met OWIN zelf die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="3bb40-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="3bb40-104">Azure Service Fabric activeert Hallo power in de hand wanneer u bent bepalen hoe u uw toocommunicate services wilt met gebruikers en met elkaar.</span><span class="sxs-lookup"><span data-stu-id="3bb40-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="3bb40-105">Deze zelfstudie richt zich op het gebruik van ASP.NET Web API met Open Web Interface voor .NET (OWIN) host zelf in Service Fabric van betrouwbare Services API servicecommunicatie implementeren.</span><span class="sxs-lookup"><span data-stu-id="3bb40-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="3bb40-106">We je dieper diep Hallo Reliable Services pluggable communicatie API.</span><span class="sxs-lookup"><span data-stu-id="3bb40-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="3bb40-107">Gebruiken we Web-API in een voorbeeld van stapsgewijze tooshow u hoe tooset een aangepaste communicatie-listener geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="3bb40-108">Inleiding tooWeb API in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3bb40-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="3bb40-109">ASP.NET-Web-API is een populair en krachtige framework voor het bouwen van HTTP APIs boven op Hallo .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3bb40-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="3bb40-110">Als u niet al bekend met het Hallo-framework bent, Zie [aan de slag met ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="3bb40-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="3bb40-111">Web-API in Service Fabric is dezelfde ASP.NET Web API u bekend zijn en veel Hallo.</span><span class="sxs-lookup"><span data-stu-id="3bb40-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="3bb40-112">Hallo verschil is in hoe u *host* een Web-API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3bb40-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="3bb40-113">Won't u Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="3bb40-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="3bb40-114">toobetter hello verschil, het laten we splitsen in twee onderdelen:</span><span class="sxs-lookup"><span data-stu-id="3bb40-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="3bb40-115">Hallo-Web-API-toepassing (met inbegrip van domeincontrollers en modellen)</span><span class="sxs-lookup"><span data-stu-id="3bb40-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="3bb40-116">Hallo-host (Hallo webserver, meestal IIS)</span><span class="sxs-lookup"><span data-stu-id="3bb40-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="3bb40-117">Een Web-API-toepassing zelf niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="3bb40-118">Het gaat niet anders Web API-toepassingen die u hebt gemaakt in de afgelopen Hallo en moet u kunnen toosimply verplaatsen via de meeste van uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="3bb40-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="3bb40-119">Maar als u hebt hosten op IIS, waar het hosten van de toepassing hello mogelijk enigszins verschillen van wat je zoekt gebruikt voor.</span><span class="sxs-lookup"><span data-stu-id="3bb40-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="3bb40-120">Voordat we u toohello onderdeel hosten, laten we beginnen met iets meer vertrouwde: Hallo Web API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3bb40-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="3bb40-121">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="3bb40-121">Create hello application</span></span>
<span data-ttu-id="3bb40-122">Start een nieuwe Service Fabric-toepassing maken met een enkele staatloze service in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3bb40-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="3bb40-123">Visual Studio-sjabloon voor een stateless service met behulp van Web-API is beschikbaar tooyou.</span><span class="sxs-lookup"><span data-stu-id="3bb40-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="3bb40-124">In deze zelfstudie hebt gaan we verder met een Web API-project maken die resulteert in wat u krijgt als u deze sjabloon hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="3bb40-125">Selecteer een lege toolearn staatloze Service-project hoe toobuild een Web API-project maakt, of u kunt beginnen met Hallo staatloze service-Web-API-sjabloon en te volgen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="3bb40-126">de eerste stap Hallo is toopull in sommige NuGet-pakketten voor Web-API.</span><span class="sxs-lookup"><span data-stu-id="3bb40-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="3bb40-127">Hallo-pakket willen we toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="3bb40-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="3bb40-128">Dit pakket bevat alle Hallo nodig Web API-pakketten en Hallo *host* pakketten.</span><span class="sxs-lookup"><span data-stu-id="3bb40-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="3bb40-129">Dit is belangrijk later.</span><span class="sxs-lookup"><span data-stu-id="3bb40-129">This will be important later.</span></span>

<span data-ttu-id="3bb40-130">Nadat hello-pakketten zijn geïnstalleerd, kunt u het opzetten van Hallo Web API-project basisstructuur beginnen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="3bb40-131">Als u Web-API hebt gebruikt, moet de structuur project Hallo bekend eruitzien.</span><span class="sxs-lookup"><span data-stu-id="3bb40-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="3bb40-132">Voeg eerst een `Controllers` directory en een eenvoudige waarden domeincontroller:</span><span class="sxs-lookup"><span data-stu-id="3bb40-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="3bb40-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="3bb40-133">**ValuesController.cs**</span></span>

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

<span data-ttu-id="3bb40-134">Voeg vervolgens een Opstartklasse op Hallo project hoofdmap tooregister Hallo routering, formatters en andere configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="3bb40-135">Dit is ook waar u Web-API op toohello aansluit *host*, die wordt later opnieuw worden herzien.</span><span class="sxs-lookup"><span data-stu-id="3bb40-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="3bb40-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="3bb40-136">**Startup.cs**</span></span>

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

<span data-ttu-id="3bb40-137">Dat is voor het toepassingsonderdeel Hallo.</span><span class="sxs-lookup"><span data-stu-id="3bb40-137">That's it for hello application part.</span></span> <span data-ttu-id="3bb40-138">We hebt op dit moment alleen Hallo Web API-project basisindeling ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3bb40-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="3bb40-139">Tot nu toe, mag niet deze anders zijn veel van de Web API-projecten die u hebt gemaakt in de afgelopen Hallo of Hallo basic Web API-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3bb40-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="3bb40-140">Uw bedrijfslogica gaat zoals gebruikelijk in Hallo-controllers en -modellen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="3bb40-141">Nu wat we doen over het hosten van zodat we kunnen het daadwerkelijk uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="3bb40-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="3bb40-142">Service die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="3bb40-142">Service hosting</span></span>
<span data-ttu-id="3bb40-143">In Service Fabric uw service wordt uitgevoerd in een *service hostproces*, een uitvoerbaar bestand dat uw servicecode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="3bb40-144">Bij het schrijven van een service met behulp van Hallo betrouwbare Services API compileert uw serviceproject NET tooan uitvoerbaar bestand dat uw servicetype registreert en uw code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="3bb40-145">Dit geldt in de meeste gevallen bij het schrijven van een service in de Service-infrastructuur in .NET.</span><span class="sxs-lookup"><span data-stu-id="3bb40-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="3bb40-146">Wanneer u Program.cs in Hallo staatloze serviceproject opent, ziet u op:</span><span class="sxs-lookup"><span data-stu-id="3bb40-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

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

<span data-ttu-id="3bb40-147">Als dat verdacht gedraagt ziet eruit als Hallo vermelding punt tooa-consoletoepassing, gebeurt dit omdat is.</span><span class="sxs-lookup"><span data-stu-id="3bb40-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="3bb40-148">Meer informatie over Hallo hostproces van de service en registratie van service zijn buiten bereik Hallo van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3bb40-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="3bb40-149">Maar het is belangrijk tooknow voor nu *uw servicecode wordt uitgevoerd in een eigen proces*.</span><span class="sxs-lookup"><span data-stu-id="3bb40-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="3bb40-150">Web-API met een OWIN-host zelf hosten</span><span class="sxs-lookup"><span data-stu-id="3bb40-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="3bb40-151">Gezien het feit dat de Web-API-toepassingscode wordt gehost in een eigen proces, hoe u koppelen tooa webserver?</span><span class="sxs-lookup"><span data-stu-id="3bb40-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="3bb40-152">Voer [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="3bb40-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="3bb40-153">OWIN is gewoon een overeenkomst tussen .NET-webtoepassingen en webservers.</span><span class="sxs-lookup"><span data-stu-id="3bb40-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="3bb40-154">Bij gebruik van ASP.NET (omhoog tooMVC 5) is Hallo webtoepassing oudsher nauw gekoppeld tooIIS via System.Web.</span><span class="sxs-lookup"><span data-stu-id="3bb40-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="3bb40-155">Web-API implementeert echter OWIN, dus u kunt een webtoepassing die wordt ontkoppeld schrijven van Hallo-webserver die als host fungeert.</span><span class="sxs-lookup"><span data-stu-id="3bb40-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="3bb40-156">Als gevolg hiervan kunt u een *zelf gehost* OWIN-webserver die u in uw eigen proces kan starten.</span><span class="sxs-lookup"><span data-stu-id="3bb40-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="3bb40-157">Hiermee past perfect bij Hallo Service Fabric hostingmodel die hierboven wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="3bb40-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="3bb40-158">In dit artikel gebruiken we Katana als Hallo OWIN host voor Web-API-toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="3bb40-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="3bb40-159">Katana is een open source OWIN host implementatie die is gebaseerd op [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) en Windows hello [HTTP-Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bb40-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3bb40-160">meer informatie over Katana, Ga toohello toolearn [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="3bb40-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="3bb40-161">Voor een snel overzicht van hoe toouse Katana tooself host Web-API, Zie [gebruik OWIN tooSelf Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="3bb40-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="3bb40-162">Hallo webserver instellen</span><span class="sxs-lookup"><span data-stu-id="3bb40-162">Set up hello web server</span></span>
<span data-ttu-id="3bb40-163">Hallo betrouwbare Services API biedt een communicatie-toegangspunt waar u communicatie stacks waarmee gebruikers en clients tooconnect toohello service kunt aansluiten:</span><span class="sxs-lookup"><span data-stu-id="3bb40-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="3bb40-164">Hallo webserver (en andere communicatiestack die u in toekomstige zoals WebSockets Hallo) te gebruiken Hallo ICommunicationListener interface toointegrate correct met Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="3bb40-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="3bb40-165">Hallo redenen hiervoor worden duidelijker in Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="3bb40-166">Maak eerst een klasse met de naam OwinCommunicationListener dat ICommunicationListener implementeert:</span><span class="sxs-lookup"><span data-stu-id="3bb40-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="3bb40-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="3bb40-167">**OwinCommunicationListener.cs**</span></span>

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

<span data-ttu-id="3bb40-168">Hallo ICommunicationListener interface biedt drie methoden toomanage een communicatie-listener voor uw service:</span><span class="sxs-lookup"><span data-stu-id="3bb40-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="3bb40-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="3bb40-169">*OpenAsync*.</span></span> <span data-ttu-id="3bb40-170">Beginnen met luisteren naar aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-170">Start listening for requests.</span></span>
* <span data-ttu-id="3bb40-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="3bb40-171">*CloseAsync*.</span></span> <span data-ttu-id="3bb40-172">Stoppen met luisteren naar aanvragen, verzoeken onderweg voltooien en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="3bb40-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="3bb40-173">*Afbreken*.</span><span class="sxs-lookup"><span data-stu-id="3bb40-173">*Abort*.</span></span> <span data-ttu-id="3bb40-174">Alles annuleren en onmiddellijk wilt stoppen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="3bb40-175">tooget gestart, persoonlijke klasseleden toevoegen voor dingen Hallo listener moet toofunction.</span><span class="sxs-lookup"><span data-stu-id="3bb40-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="3bb40-176">Deze wordt geïnitialiseerd via Hallo constructor en later wordt gebruikt bij het instellen van Hallo URL luisteren.</span><span class="sxs-lookup"><span data-stu-id="3bb40-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

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

## <a name="implement-openasync"></a><span data-ttu-id="3bb40-177">OpenAsync implementeren</span><span class="sxs-lookup"><span data-stu-id="3bb40-177">Implement OpenAsync</span></span>
<span data-ttu-id="3bb40-178">tooset Hallo-webserver, moet u twee soorten informatie:</span><span class="sxs-lookup"><span data-stu-id="3bb40-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="3bb40-179">*Een URL-voorvoegsel pad*.</span><span class="sxs-lookup"><span data-stu-id="3bb40-179">*A URL path prefix*.</span></span> <span data-ttu-id="3bb40-180">Hoewel dit optioneel is, is het geschikt is voor u tooset deze nu omhoog zodat u meerdere webservices veilig in uw toepassing hosten kunt.</span><span class="sxs-lookup"><span data-stu-id="3bb40-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="3bb40-181">*Een poort*.</span><span class="sxs-lookup"><span data-stu-id="3bb40-181">*A port*.</span></span>

<span data-ttu-id="3bb40-182">Voordat u een poort voor de webserver Hallo ontvangt, is het belangrijk dat u begrijpt dat Service Fabric een toepassingslaag die als een buffer tussen uw toepassing en het Hallo onderliggende besturingssysteem dat bevat fungeert op wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="3bb40-183">Als zodanig Service Fabric biedt een manier tooconfigure *eindpunten* voor uw services.</span><span class="sxs-lookup"><span data-stu-id="3bb40-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="3bb40-184">Service Fabric zorgt ervoor dat eindpunten beschikbaar voor uw service toouse zijn.</span><span class="sxs-lookup"><span data-stu-id="3bb40-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="3bb40-185">Deze manier kunnen er geen tooconfigure ze zelf in Hallo onderliggende OS-omgeving.</span><span class="sxs-lookup"><span data-stu-id="3bb40-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="3bb40-186">U kunt eenvoudig uw Service Fabric-toepassing in verschillende omgevingen zonder toomake alle wijzigingen tooyour toepassingen hosten.</span><span class="sxs-lookup"><span data-stu-id="3bb40-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="3bb40-187">(Bijvoorbeeld, u kunt hosten Hallo dezelfde toepassing in Azure of in uw eigen datacenter.)</span><span class="sxs-lookup"><span data-stu-id="3bb40-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="3bb40-188">Een HTTP-eindpunt in PackageRoot\ServiceManifest.xml configureren:</span><span class="sxs-lookup"><span data-stu-id="3bb40-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="3bb40-189">Deze stap is belangrijk omdat hostproces Hallo-service wordt uitgevoerd onder beperkte referenties (Network Service in Windows).</span><span class="sxs-lookup"><span data-stu-id="3bb40-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="3bb40-190">Dit betekent dat uw service geen toegang tooset u een HTTP-eindpunt op zichzelf hebt.</span><span class="sxs-lookup"><span data-stu-id="3bb40-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="3bb40-191">Met behulp van de eindpuntconfiguratie hello, Service Fabric tooset up Hallo juiste toegangsbeheerlijst (ACL) voor de URL die Hallo service luistert op Hallo kent.</span><span class="sxs-lookup"><span data-stu-id="3bb40-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="3bb40-192">Service Fabric biedt ook een standaardlocatie tooconfigure eindpunten.</span><span class="sxs-lookup"><span data-stu-id="3bb40-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="3bb40-193">Terug in OwinCommunicationListener.cs, kunt u beginnen OpenAsync implementeren.</span><span class="sxs-lookup"><span data-stu-id="3bb40-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="3bb40-194">Dit is waar u de webserver Hallo begint.</span><span class="sxs-lookup"><span data-stu-id="3bb40-194">This is where you start hello web server.</span></span> <span data-ttu-id="3bb40-195">Eerst Hallo eindpuntinformatie ophalen en Hallo-URL die Hallo-service controleert op maken.</span><span class="sxs-lookup"><span data-stu-id="3bb40-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="3bb40-196">Hallo-URL is verschillend, afhankelijk van of Hallo-listener wordt gebruikt in een stateless service of een stateful service.</span><span class="sxs-lookup"><span data-stu-id="3bb40-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="3bb40-197">Voor een stateful service moet Hallo listener toocreate een unieke adres voor elke replica stateful service deze luistert op.</span><span class="sxs-lookup"><span data-stu-id="3bb40-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="3bb40-198">Hallo-adres kan wel veel eenvoudiger voor stateless services.</span><span class="sxs-lookup"><span data-stu-id="3bb40-198">For stateless services, hello address can be much simpler.</span></span> 

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

<span data-ttu-id="3bb40-199">Houd er rekening mee dat 'http://+' Hier wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3bb40-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="3bb40-200">Dit is toomake ervoor dat de dat webserver Hallo luistert op alle beschikbare adressen, inclusief localhost, FQDN-naam en IP-Hallo-machine.</span><span class="sxs-lookup"><span data-stu-id="3bb40-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="3bb40-201">Hallo OpenAsync implementatie is een van de belangrijkste redenen Hallo waarom Hallo webserver (of een communicatiestack) is geïmplementeerd als een ICommunicationListener in plaats van dat deze rechtstreeks vanuit openen `RunAsync()` in Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="3bb40-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="3bb40-202">Hallo geretourneerde waarde van OpenAsync is Hallo-adres dat webserver Hallo luistert op.</span><span class="sxs-lookup"><span data-stu-id="3bb40-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="3bb40-203">Als dit adres wordt toohello system geretourneerd, registreert het Hallo-adres met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="3bb40-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="3bb40-204">Service Fabric bevat een API waarmee clients en andere services toothen vragen voor dit adres met de servicenaam.</span><span class="sxs-lookup"><span data-stu-id="3bb40-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="3bb40-205">Dit is belangrijk omdat Hallo-serviceadres niet statisch is.</span><span class="sxs-lookup"><span data-stu-id="3bb40-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="3bb40-206">Services worden in Hallo cluster voor netwerktaakverdeling en beschikbaarheid doeleinden van resource verplaatst.</span><span class="sxs-lookup"><span data-stu-id="3bb40-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="3bb40-207">Dit is Hallo-mechanisme waarmee clients tooresolve Hallo adres voor een service luistert.</span><span class="sxs-lookup"><span data-stu-id="3bb40-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="3bb40-208">Met die in gedachten OpenAsync Hallo webserver wordt gestart en retourneert Hallo-adres dat deze luistert op.</span><span class="sxs-lookup"><span data-stu-id="3bb40-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="3bb40-209">Houd er rekening mee dat deze op 'http://+ luistert', maar voordat OpenAsync wordt geretourneerd Hallo-adres, Hallo ' + ' wordt vervangen door Hallo IP of FQDN van Hallo knooppunt zich momenteel op.</span><span class="sxs-lookup"><span data-stu-id="3bb40-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="3bb40-210">Hallo-adres dat wordt geretourneerd door deze methode is wat geregistreerd bij Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="3bb40-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="3bb40-211">Het is ook wat clients en andere services zien wanneer ze voor een service-adres vragen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="3bb40-212">Voor clients toocorrectly verbinding tooit, moeten deze een werkelijke IP of FQDN Hallo-adres.</span><span class="sxs-lookup"><span data-stu-id="3bb40-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

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

<span data-ttu-id="3bb40-213">Houd er rekening mee dat deze verwijst naar Hallo-Opstartklasse toohello OwinCommunicationListener in Hallo-constructor is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="3bb40-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="3bb40-214">Dit exemplaar starten wordt gebruikt door Hallo web server toobootstrap Hallo Web API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3bb40-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="3bb40-215">Hallo `ServiceEventSource.Current.Message()` regel wordt weergegeven in Hallo diagnostische gebeurtenissen venster later bij het uitvoeren van Hallo toepassing tooconfirm Hallo webserver is gestart.</span><span class="sxs-lookup"><span data-stu-id="3bb40-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="3bb40-216">Implementeer CloseAsync en afbreken</span><span class="sxs-lookup"><span data-stu-id="3bb40-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="3bb40-217">Ten slotte implementeren CloseAsync zowel afbreken toostop Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="3bb40-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="3bb40-218">Hallo-webserver kan worden gestopt door Hallo server ingang die is gemaakt tijdens OpenAsync verwijdering.</span><span class="sxs-lookup"><span data-stu-id="3bb40-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

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

<span data-ttu-id="3bb40-219">In deze voorbeeldimplementatie CloseAsync zowel afbreken gewoon Hallo webserver stoppen.</span><span class="sxs-lookup"><span data-stu-id="3bb40-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="3bb40-220">U kunt ervoor kiezen tooperform meer probleemloos gecoördineerde afsluiten van de webserver Hallo in CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="3bb40-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="3bb40-221">Hallo afsluiten kan bijvoorbeeld, wacht u totdat onderweg aanvragen toobe voltooid voordat Hallo retourneren.</span><span class="sxs-lookup"><span data-stu-id="3bb40-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="3bb40-222">Hallo-webserver starten</span><span class="sxs-lookup"><span data-stu-id="3bb40-222">Start hello web server</span></span>
<span data-ttu-id="3bb40-223">U bent nu klaar toocreate en een OwinCommunicationListener toostart Hallo webserver-exemplaar geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="3bb40-224">Terug in Hallo serviceklasse (WebService.cs), overschrijven Hallo `CreateServiceInstanceListeners()` methode:</span><span class="sxs-lookup"><span data-stu-id="3bb40-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

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

<span data-ttu-id="3bb40-225">Dit is waar de Web-API Hallo *toepassing* en OWIN Hallo *host* ten slotte voldoen aan.</span><span class="sxs-lookup"><span data-stu-id="3bb40-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="3bb40-226">Hallo-host (OwinCommunicationListener) krijgt een exemplaar van Hallo *toepassing* (Web-API) via Hallo Opstartklasse.</span><span class="sxs-lookup"><span data-stu-id="3bb40-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="3bb40-227">Service Fabric worden vervolgens de levenscyclus beheert.</span><span class="sxs-lookup"><span data-stu-id="3bb40-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="3bb40-228">Dit patroon kan doorgaans worden gevolgd door een communicatiestack.</span><span class="sxs-lookup"><span data-stu-id="3bb40-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="3bb40-229">Alles samenvoegen</span><span class="sxs-lookup"><span data-stu-id="3bb40-229">Put it all together</span></span>
<span data-ttu-id="3bb40-230">In dit voorbeeld, u hoeft niet toodo alles in Hallo `RunAsync()` methode, zodat deze onderdrukking kan gewoon worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="3bb40-231">de laatste implementatie Hallo moet zeer eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="3bb40-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="3bb40-232">Alleen moet toocreate Hallo communicatie listener:</span><span class="sxs-lookup"><span data-stu-id="3bb40-232">It only needs toocreate hello communication listener:</span></span>

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

<span data-ttu-id="3bb40-233">Hallo voltooid `OwinCommunicationListener` klasse:</span><span class="sxs-lookup"><span data-stu-id="3bb40-233">hello complete `OwinCommunicationListener` class:</span></span>

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

<span data-ttu-id="3bb40-234">Nu dat alle Hallo stukken erin hebt geplaatst, wordt uw project moet eruitzien als een typische toepassing Web-API met betrouwbare Services API-toegangspunten en een OWIN-host.</span><span class="sxs-lookup"><span data-stu-id="3bb40-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="3bb40-235">Voer en verbinding maken via een webbrowser</span><span class="sxs-lookup"><span data-stu-id="3bb40-235">Run and connect through a web browser</span></span>
<span data-ttu-id="3bb40-236">Als u dit nog niet hebt gedaan, [uw ontwikkelomgeving instellen](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3bb40-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="3bb40-237">U kunt nu bouwen en implementeren van uw service.</span><span class="sxs-lookup"><span data-stu-id="3bb40-237">You can now build and deploy your service.</span></span> <span data-ttu-id="3bb40-238">Druk op **F5** in Visual Studio toobuild toepassing hello en implementeren.</span><span class="sxs-lookup"><span data-stu-id="3bb40-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="3bb40-239">Hallo diagnostische gebeurtenissen venster ziet u een bericht weergegeven dat Hallo webserver geopend op http://localhost:8281 aangeeft /.</span><span class="sxs-lookup"><span data-stu-id="3bb40-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="3bb40-240">Als het Hallo-poort is al geopend door een ander proces op uw computer, ziet u mogelijk een fout hier.</span><span class="sxs-lookup"><span data-stu-id="3bb40-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="3bb40-241">Hiermee wordt aangegeven dat Hallo-listener kan niet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="3bb40-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="3bb40-242">Als dat Hallo geval is, kunt u met behulp van een andere poort voor de eindpuntconfiguratie Hallo in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="3bb40-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="3bb40-243">Zodra het Hallo-service wordt uitgevoerd, open een browser en te navigeren[api-http://localhost:8281-waarden](http://localhost:8281/api/values) tootest deze.</span><span class="sxs-lookup"><span data-stu-id="3bb40-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="3bb40-244">Het uit te schalen</span><span class="sxs-lookup"><span data-stu-id="3bb40-244">Scale it out</span></span>
<span data-ttu-id="3bb40-245">Staatloze web-apps doorgaans uitbreiden betekent meer machines toe te voegen en up Hallo web-apps op deze draaien.</span><span class="sxs-lookup"><span data-stu-id="3bb40-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="3bb40-246">Service Fabric de orchestration-engine kunt dit doen voor u wanneer nieuwe knooppunten tooa cluster worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3bb40-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="3bb40-247">Als u exemplaren van een staatloze service maakt, kunt u Hallo-nummer opgeven van exemplaren die u wilt toocreate.</span><span class="sxs-lookup"><span data-stu-id="3bb40-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="3bb40-248">Service Fabric wordt dat aantal exemplaren op knooppunten in cluster Hallo geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3bb40-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="3bb40-249">En op deze manier niet toocreate meer dan één exemplaar op een willekeurig knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3bb40-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="3bb40-250">U kunt ook opgeven dat het Service Fabric tooalways geen exemplaar maken op elk knooppunt door te geven **-1** voor Hallo-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3bb40-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="3bb40-251">Dit zorgt ervoor dat als u knooppunten tooscale uit het cluster toevoegt, een exemplaar van uw stateless service wordt gemaakt op Hallo nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3bb40-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="3bb40-252">Deze waarde is een eigenschap van de service-exemplaar hello, zodat deze bij het maken van een service-exemplaar is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3bb40-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="3bb40-253">U kunt dit doen via PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3bb40-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="3bb40-254">U kunt dit ook doen wanneer u een standaard-service in een Visual Studio-project staatloze service definieert:</span><span class="sxs-lookup"><span data-stu-id="3bb40-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="3bb40-255">Voor meer informatie over hoe toocreate toepassing en service-exemplaren zien [implementeren van een toepassing](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="3bb40-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bb40-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3bb40-256">Next steps</span></span>
[<span data-ttu-id="3bb40-257">Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3bb40-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

