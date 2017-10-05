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
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="931ca-103">Aan de slag: Service Fabric-Web-API-services met OWIN zelf die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="931ca-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="931ca-104">Azure Service Fabric brengt de mogelijkheden in uw handen wanneer u bent bepalen hoe u wilt dat uw services met gebruikers en met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="931ca-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span></span> <span data-ttu-id="931ca-105">Deze zelfstudie richt zich op het gebruik van ASP.NET Web API met Open Web Interface voor .NET (OWIN) host zelf in Service Fabric van betrouwbare Services API servicecommunicatie implementeren.</span><span class="sxs-lookup"><span data-stu-id="931ca-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="931ca-106">We je dieper diep Reliable Services pluggable communicatie API.</span><span class="sxs-lookup"><span data-stu-id="931ca-106">We'll delve deeply into the Reliable Services pluggable communication API.</span></span> <span data-ttu-id="931ca-107">We ook gebruiken Web-API in het voorbeeld van een stapsgewijze aan hoe u een aangepaste communicatie-listener instellen.</span><span class="sxs-lookup"><span data-stu-id="931ca-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span></span>

## <a name="introduction-to-web-api-in-service-fabric"></a><span data-ttu-id="931ca-108">Inleiding tot Web-API in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="931ca-108">Introduction to Web API in Service Fabric</span></span>
<span data-ttu-id="931ca-109">ASP.NET-Web-API is een populair en krachtige framework voor het bouwen van HTTP-APIs boven op het .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="931ca-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span></span> <span data-ttu-id="931ca-110">Als u niet al bekend met het framework bent, Zie [aan de slag met ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="931ca-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span></span>

<span data-ttu-id="931ca-111">Web-API in Service Fabric is de dezelfde ASP.NET Web API-u bekend zijn en veel.</span><span class="sxs-lookup"><span data-stu-id="931ca-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="931ca-112">Het verschil is in hoe u *host* een Web-API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="931ca-112">The difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="931ca-113">Won't u Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="931ca-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="931ca-114">Voor meer informatie over het verschil, gaan we dit opsplitsen in twee delen:</span><span class="sxs-lookup"><span data-stu-id="931ca-114">To better understand the difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="931ca-115">De Web-API-toepassing (met inbegrip van domeincontrollers en modellen)</span><span class="sxs-lookup"><span data-stu-id="931ca-115">The Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="931ca-116">De host (de webserver, meestal IIS)</span><span class="sxs-lookup"><span data-stu-id="931ca-116">The host (the web server, usually IIS)</span></span>

<span data-ttu-id="931ca-117">Een Web-API-toepassing zelf niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="931ca-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="931ca-118">Het gaat niet anders Web API-toepassingen die u in het verleden hebt gemaakt en moet u kunnen gewoon plaatst u de meeste van uw toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="931ca-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span></span> <span data-ttu-id="931ca-119">Maar als u hebt op IIS, waar u de toepassing mogelijk host enigszins verschillen van bent u gewend om is host.</span><span class="sxs-lookup"><span data-stu-id="931ca-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span></span> <span data-ttu-id="931ca-120">Voordat we u naar de host deel, laten we beginnen met iets meer vertrouwde: de Web-API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="931ca-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="931ca-121">De toepassing maken</span><span class="sxs-lookup"><span data-stu-id="931ca-121">Create the application</span></span>
<span data-ttu-id="931ca-122">Start een nieuwe Service Fabric-toepassing maken met een enkele staatloze service in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="931ca-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="931ca-123">Visual Studio-sjabloon voor een stateless service met behulp van Web-API is voor u beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="931ca-123">A Visual Studio template for a stateless service using Web API is available to you.</span></span> <span data-ttu-id="931ca-124">In deze zelfstudie hebt gaan we verder met een Web API-project maken die resulteert in wat u krijgt als u deze sjabloon hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="931ca-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="931ca-125">Selecteer een lege staatloze Service-project voor informatie over het bouwen van een Web API-project maken of u kunt beginnen met een sjabloon voor de staatloze service-Web-API en te volgen.</span><span class="sxs-lookup"><span data-stu-id="931ca-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="931ca-126">De eerste stap is om op te halen in sommige NuGet-pakketten voor Web-API.</span><span class="sxs-lookup"><span data-stu-id="931ca-126">The first step is to pull in some NuGet packages for Web API.</span></span> <span data-ttu-id="931ca-127">Het pakket wilt gebruiken is Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="931ca-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="931ca-128">Dit pakket bevat alle benodigde pakketten voor Web-API en de *host* pakketten.</span><span class="sxs-lookup"><span data-stu-id="931ca-128">This package includes all the necessary Web API packages and the *host* packages.</span></span> <span data-ttu-id="931ca-129">Dit is belangrijk later.</span><span class="sxs-lookup"><span data-stu-id="931ca-129">This will be important later.</span></span>

<span data-ttu-id="931ca-130">Nadat de pakketten zijn geïnstalleerd, kunt u beginnen opzetten van de basisstructuur van de Web-API-project.</span><span class="sxs-lookup"><span data-stu-id="931ca-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span></span> <span data-ttu-id="931ca-131">Als u Web-API hebt gebruikt, moet de projectstructuur bekend eruitzien.</span><span class="sxs-lookup"><span data-stu-id="931ca-131">If you've used Web API, the project structure should look very familiar.</span></span> <span data-ttu-id="931ca-132">Voeg eerst een `Controllers` directory en een eenvoudige waarden domeincontroller:</span><span class="sxs-lookup"><span data-stu-id="931ca-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="931ca-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="931ca-133">**ValuesController.cs**</span></span>

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

<span data-ttu-id="931ca-134">Voeg vervolgens een Opstartklasse toe op de hoofdmap van het project te registreren met de routering, formatters en andere configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="931ca-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="931ca-135">Dit is ook waar Web-API op aansluit op de *host*, die wordt later opnieuw worden herzien.</span><span class="sxs-lookup"><span data-stu-id="931ca-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="931ca-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="931ca-136">**Startup.cs**</span></span>

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

<span data-ttu-id="931ca-137">Dat is voor de toepassing die deel uitmaken.</span><span class="sxs-lookup"><span data-stu-id="931ca-137">That's it for the application part.</span></span> <span data-ttu-id="931ca-138">We hebt op dit moment alleen de Web-API-project basisindeling ingesteld.</span><span class="sxs-lookup"><span data-stu-id="931ca-138">At this point, we've set up just the basic Web API project layout.</span></span> <span data-ttu-id="931ca-139">Tot nu toe, mag niet deze anders zijn veel van de Web API-projecten die u hebt gemaakt in het verleden of van de eenvoudige Web-API-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="931ca-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span></span> <span data-ttu-id="931ca-140">Uw bedrijfslogica gaat zoals gebruikelijk in de controllers en -modellen.</span><span class="sxs-lookup"><span data-stu-id="931ca-140">Your business logic goes in the controllers and models as usual.</span></span>

<span data-ttu-id="931ca-141">Nu wat we doen over het hosten van zodat we kunnen het daadwerkelijk uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="931ca-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="931ca-142">Service die als host fungeert</span><span class="sxs-lookup"><span data-stu-id="931ca-142">Service hosting</span></span>
<span data-ttu-id="931ca-143">In Service Fabric uw service wordt uitgevoerd in een *service hostproces*, een uitvoerbaar bestand dat uw servicecode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="931ca-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="931ca-144">Bij het schrijven van een service met behulp van de API voor betrouwbare Services compileert uw serviceproject net als een uitvoerbaar bestand dat uw servicetype registreert en uw code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="931ca-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="931ca-145">Dit geldt in de meeste gevallen bij het schrijven van een service in de Service-infrastructuur in .NET.</span><span class="sxs-lookup"><span data-stu-id="931ca-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="931ca-146">Wanneer u Program.cs in het serviceproject staatloze opent, ziet u op:</span><span class="sxs-lookup"><span data-stu-id="931ca-146">When you open Program.cs in the stateless service project, you should see:</span></span>

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

<span data-ttu-id="931ca-147">Als die eruit ziet verdacht gedraagt het toegangspunt voor een consoletoepassing, gebeurt dit omdat is.</span><span class="sxs-lookup"><span data-stu-id="931ca-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span></span>

<span data-ttu-id="931ca-148">Meer informatie over de hostproces van de service en de serviceregistratie zijn buiten het bereik van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="931ca-148">Further details about the service host process and service registration are beyond the scope of this article.</span></span> <span data-ttu-id="931ca-149">Maar het is belangrijk te weten voor nu *uw servicecode wordt uitgevoerd in een eigen proces*.</span><span class="sxs-lookup"><span data-stu-id="931ca-149">But it's important to know for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="931ca-150">Web-API met een OWIN-host zelf hosten</span><span class="sxs-lookup"><span data-stu-id="931ca-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="931ca-151">Gezien het feit dat de Web-API-toepassingscode wordt gehost in een eigen proces, hoe u koppelen naar een webserver?</span><span class="sxs-lookup"><span data-stu-id="931ca-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span></span> <span data-ttu-id="931ca-152">Voer [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="931ca-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="931ca-153">OWIN is gewoon een overeenkomst tussen .NET-webtoepassingen en webservers.</span><span class="sxs-lookup"><span data-stu-id="931ca-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="931ca-154">Traditioneel als ASP.NET (maximaal MVC 5) wordt gebruikt, wordt de webtoepassing is nauw aan IIS via System.Web gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="931ca-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span></span> <span data-ttu-id="931ca-155">Web-API implementeert echter OWIN, dus u kunt een webtoepassing die wordt ontkoppeld van de webserver die als host fungeert schrijven.</span><span class="sxs-lookup"><span data-stu-id="931ca-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span></span> <span data-ttu-id="931ca-156">Als gevolg hiervan kunt u een *zelf gehost* OWIN-webserver die u in uw eigen proces kan starten.</span><span class="sxs-lookup"><span data-stu-id="931ca-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="931ca-157">Hiermee past perfect bij het Service Fabric-hostingmodel dat hierboven wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="931ca-157">This fits perfectly with the Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="931ca-158">In dit artikel gebruiken we Katana als host voor OWIN voor de Web-API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="931ca-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span></span> <span data-ttu-id="931ca-159">Katana is een open source OWIN host implementatie die is gebaseerd op [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) en de Windows [HTTP-Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="931ca-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="931ca-160">Voor meer informatie over Katana, gaat u naar de [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="931ca-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="931ca-161">Zie voor een snel overzicht van het Katana gebruiken voor het hosten van Web-API zelf [OWIN gebruiken om te Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="931ca-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-the-web-server"></a><span data-ttu-id="931ca-162">De webserver instellen</span><span class="sxs-lookup"><span data-stu-id="931ca-162">Set up the web server</span></span>
<span data-ttu-id="931ca-163">De API voor betrouwbare Services biedt een communicatie-toegangspunt waar u communicatie stacks waarmee gebruikers en -clients verbinding maken met de service kunt aansluiten:</span><span class="sxs-lookup"><span data-stu-id="931ca-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="931ca-164">De webserver (en andere communicatiestack die u in de toekomst, zoals WebSockets) moeten de interface ICommunicationListener gebruiken correct integreren met het systeem.</span><span class="sxs-lookup"><span data-stu-id="931ca-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span></span> <span data-ttu-id="931ca-165">De redenen hiervoor worden meer zichtbaar in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="931ca-165">The reasons for this will become more apparent in the following steps.</span></span>

<span data-ttu-id="931ca-166">Maak eerst een klasse met de naam OwinCommunicationListener dat ICommunicationListener implementeert:</span><span class="sxs-lookup"><span data-stu-id="931ca-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="931ca-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="931ca-167">**OwinCommunicationListener.cs**</span></span>

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

<span data-ttu-id="931ca-168">De interface ICommunicationListener biedt drie methoden voor het beheren van een communicatie-listener voor uw service:</span><span class="sxs-lookup"><span data-stu-id="931ca-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span></span>

* <span data-ttu-id="931ca-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="931ca-169">*OpenAsync*.</span></span> <span data-ttu-id="931ca-170">Beginnen met luisteren naar aanvragen.</span><span class="sxs-lookup"><span data-stu-id="931ca-170">Start listening for requests.</span></span>
* <span data-ttu-id="931ca-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="931ca-171">*CloseAsync*.</span></span> <span data-ttu-id="931ca-172">Stoppen met luisteren naar aanvragen, verzoeken onderweg voltooien en afsluiten.</span><span class="sxs-lookup"><span data-stu-id="931ca-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="931ca-173">*Afbreken*.</span><span class="sxs-lookup"><span data-stu-id="931ca-173">*Abort*.</span></span> <span data-ttu-id="931ca-174">Alles annuleren en onmiddellijk wilt stoppen.</span><span class="sxs-lookup"><span data-stu-id="931ca-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="931ca-175">Toevoegen aan de slag persoonlijke klassenleden voor zaken die de listener moet werken.</span><span class="sxs-lookup"><span data-stu-id="931ca-175">To get started, add private class members for things the listener will need to function.</span></span> <span data-ttu-id="931ca-176">Deze wordt geïnitialiseerd door middel van de constructor en later wordt gebruikt bij het instellen van de luisterende URL.</span><span class="sxs-lookup"><span data-stu-id="931ca-176">These will be initialized through the constructor and used later when you set up the listening URL.</span></span>

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

## <a name="implement-openasync"></a><span data-ttu-id="931ca-177">OpenAsync implementeren</span><span class="sxs-lookup"><span data-stu-id="931ca-177">Implement OpenAsync</span></span>
<span data-ttu-id="931ca-178">Als u de webserver instelt, moet u twee soorten informatie:</span><span class="sxs-lookup"><span data-stu-id="931ca-178">To set up the web server, you need two pieces of information:</span></span>

* <span data-ttu-id="931ca-179">*Een URL-voorvoegsel pad*.</span><span class="sxs-lookup"><span data-stu-id="931ca-179">*A URL path prefix*.</span></span> <span data-ttu-id="931ca-180">Hoewel dit optioneel is, is het geschikt is voor u dit nu zo ingesteld dat veilig u meerdere webservices in uw toepassing hosten kunt.</span><span class="sxs-lookup"><span data-stu-id="931ca-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="931ca-181">*Een poort*.</span><span class="sxs-lookup"><span data-stu-id="931ca-181">*A port*.</span></span>

<span data-ttu-id="931ca-182">Voordat u een poort voor de webserver krijgen, is het belangrijk dat u begrijpt dat Service Fabric een toepassingslaag die als een buffer tussen uw toepassing en het onderliggende besturingssysteem dat bevat fungeert op wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="931ca-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span></span> <span data-ttu-id="931ca-183">Als zodanig Service Fabric biedt een manier voor het configureren van *eindpunten* voor uw services.</span><span class="sxs-lookup"><span data-stu-id="931ca-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span></span> <span data-ttu-id="931ca-184">Service Fabric zorgt ervoor dat eindpunten beschikbaar voor uw service zijn te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="931ca-184">Service Fabric ensures that endpoints are available for your service to use.</span></span> <span data-ttu-id="931ca-185">Op deze manier u niet moet ze zelf configureren in de onderliggende OS-omgeving.</span><span class="sxs-lookup"><span data-stu-id="931ca-185">This way, you don't have to configure them yourself in the underlying OS environment.</span></span> <span data-ttu-id="931ca-186">U kunt eenvoudig uw Service Fabric-toepassing in verschillende omgevingen zonder wijzigingen aanbrengen in uw toepassing hosten.</span><span class="sxs-lookup"><span data-stu-id="931ca-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span></span> <span data-ttu-id="931ca-187">(Bijvoorbeeld, u kunt hosten dezelfde toepassing in Azure of in uw eigen datacenter.)</span><span class="sxs-lookup"><span data-stu-id="931ca-187">(For example, you can host the same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="931ca-188">Een HTTP-eindpunt in PackageRoot\ServiceManifest.xml configureren:</span><span class="sxs-lookup"><span data-stu-id="931ca-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="931ca-189">Deze stap is belangrijk, omdat het hostproces van de service wordt uitgevoerd onder beperkte referenties (Network Service in Windows).</span><span class="sxs-lookup"><span data-stu-id="931ca-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="931ca-190">Dit betekent dat er geen toegang voor het instellen van een HTTP-eindpunt op een eigen uw service.</span><span class="sxs-lookup"><span data-stu-id="931ca-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span></span> <span data-ttu-id="931ca-191">Met behulp van de eindpuntconfiguratie kent Service Fabric voor de URL die de service controleert op voor het instellen van de juiste toegangsbeheerlijst (ACL).</span><span class="sxs-lookup"><span data-stu-id="931ca-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span></span> <span data-ttu-id="931ca-192">Service Fabric biedt ook een standaardlocatie voor het configureren van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="931ca-192">Service Fabric also provides a standard place to configure endpoints.</span></span>

<span data-ttu-id="931ca-193">Terug in OwinCommunicationListener.cs, kunt u beginnen OpenAsync implementeren.</span><span class="sxs-lookup"><span data-stu-id="931ca-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="931ca-194">Dit is waar het starten van de webserver.</span><span class="sxs-lookup"><span data-stu-id="931ca-194">This is where you start the web server.</span></span> <span data-ttu-id="931ca-195">Eerst Lees de eindpuntinformatie voor het en maak de URL waarnaar de service wordt luisteren.</span><span class="sxs-lookup"><span data-stu-id="931ca-195">First, get the endpoint information and create the URL that the service will listen on.</span></span> <span data-ttu-id="931ca-196">De URL is verschillend, afhankelijk van of de listener wordt gebruikt in een stateless service of een stateful service.</span><span class="sxs-lookup"><span data-stu-id="931ca-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="931ca-197">De listener moet een unieke adres maken voor elke stateful service replica die deze luistert op voor een stateful service.</span><span class="sxs-lookup"><span data-stu-id="931ca-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="931ca-198">Het adres kan niet veel eenvoudiger voor stateless services.</span><span class="sxs-lookup"><span data-stu-id="931ca-198">For stateless services, the address can be much simpler.</span></span> 

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

<span data-ttu-id="931ca-199">Houd er rekening mee dat 'http://+' Hier wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="931ca-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="931ca-200">Dit is om ervoor te zorgen dat de webserver op alle beschikbare adressen luistert, inclusief localhost, FQDN-naam en het machine IP-adres.</span><span class="sxs-lookup"><span data-stu-id="931ca-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span></span>

<span data-ttu-id="931ca-201">De implementatie van OpenAsync is een van de belangrijkste redenen waarom de webserver (of een communicatiestack) is geïmplementeerd als een ICommunicationListener in plaats van dat deze rechtstreeks vanuit openen `RunAsync()` in de service.</span><span class="sxs-lookup"><span data-stu-id="931ca-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span></span> <span data-ttu-id="931ca-202">De geretourneerde waarde van OpenAsync is het adres dat op de webserver luistert.</span><span class="sxs-lookup"><span data-stu-id="931ca-202">The return value from OpenAsync is the address that the web server is listening on.</span></span> <span data-ttu-id="931ca-203">Als dit adres wordt geretourneerd met het systeem, wordt het adres geregistreerd bij de service.</span><span class="sxs-lookup"><span data-stu-id="931ca-203">When this address is returned to the system, it registers the address with the service.</span></span> <span data-ttu-id="931ca-204">Service Fabric biedt een API waarmee clients en andere services kunnen vervolgens vraagt u voor dit adres met de servicenaam.</span><span class="sxs-lookup"><span data-stu-id="931ca-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="931ca-205">Dit is belangrijk omdat het serviceadres niet statisch is.</span><span class="sxs-lookup"><span data-stu-id="931ca-205">This is important because the service address is not static.</span></span> <span data-ttu-id="931ca-206">Services worden in het cluster voor netwerktaakverdeling en beschikbaarheid doeleinden van resource verplaatst.</span><span class="sxs-lookup"><span data-stu-id="931ca-206">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="931ca-207">Dit is het mechanisme waarmee clients kunnen omzetten van het luisterende adres voor een service.</span><span class="sxs-lookup"><span data-stu-id="931ca-207">This is the mechanism that allows clients to resolve the listening address for a service.</span></span>

<span data-ttu-id="931ca-208">Met die in gedachten OpenAsync Start de webserver en retourneert het adres waarop wordt geluisterd.</span><span class="sxs-lookup"><span data-stu-id="931ca-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span></span> <span data-ttu-id="931ca-209">Opmerking dat deze luistert op 'http://+', maar voordat OpenAsync het adres retourneert, de '+' wordt vervangen door de IP- of FQDN van het knooppunt dat zich momenteel op.</span><span class="sxs-lookup"><span data-stu-id="931ca-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span></span> <span data-ttu-id="931ca-210">Het adres dat wordt geretourneerd door deze methode is wat geregistreerd bij het systeem.</span><span class="sxs-lookup"><span data-stu-id="931ca-210">The address that is returned by this method is what's registered with the system.</span></span> <span data-ttu-id="931ca-211">Het is ook wat clients en andere services zien wanneer ze voor een service-adres vragen.</span><span class="sxs-lookup"><span data-stu-id="931ca-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="931ca-212">Voor clients correct verbinding kunnen maken, moeten een werkelijke IP of FQDN-naam in het adres.</span><span class="sxs-lookup"><span data-stu-id="931ca-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span></span>

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

<span data-ttu-id="931ca-213">Houd er rekening mee dat deze verwijst naar het starten van de klasse die is doorgegeven aan de OwinCommunicationListener in de constructor.</span><span class="sxs-lookup"><span data-stu-id="931ca-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span></span> <span data-ttu-id="931ca-214">Dit exemplaar starten wordt gebruikt door de webserver voor de bootstrap van de Web-API-toepassing.</span><span class="sxs-lookup"><span data-stu-id="931ca-214">This startup instance is used by the web server to bootstrap the Web API application.</span></span>

<span data-ttu-id="931ca-215">De `ServiceEventSource.Current.Message()` regel wordt weergegeven in het venster diagnostische gebeurtenissen later, wanneer het uitvoeren van de toepassing om te bevestigen dat de webserver is gestart.</span><span class="sxs-lookup"><span data-stu-id="931ca-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="931ca-216">Implementeer CloseAsync en afbreken</span><span class="sxs-lookup"><span data-stu-id="931ca-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="931ca-217">Ten slotte CloseAsync en afbreken om te stoppen van de webserver worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="931ca-217">Finally, implement both CloseAsync and Abort to stop the web server.</span></span> <span data-ttu-id="931ca-218">De webserver kan worden gestopt door de server-ingang die is gemaakt tijdens OpenAsync verwijdering.</span><span class="sxs-lookup"><span data-stu-id="931ca-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span></span>

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

<span data-ttu-id="931ca-219">In deze voorbeeldimplementatie stopt CloseAsync zowel afbreken gewoon u de webserver.</span><span class="sxs-lookup"><span data-stu-id="931ca-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span></span> <span data-ttu-id="931ca-220">U kan ervoor kiezen om een meer probleemloos gecoördineerde afsluiten van de webserver in CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="931ca-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span></span> <span data-ttu-id="931ca-221">Bijvoorbeeld, kan het afsluiten wacht tot onderweg aanvragen om te worden voltooid voordat het rendement.</span><span class="sxs-lookup"><span data-stu-id="931ca-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span></span>

## <a name="start-the-web-server"></a><span data-ttu-id="931ca-222">Start de webserver</span><span class="sxs-lookup"><span data-stu-id="931ca-222">Start the web server</span></span>
<span data-ttu-id="931ca-223">U bent nu klaar om te maken en een exemplaar van OwinCommunicationListener starten van de webserver wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="931ca-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span></span> <span data-ttu-id="931ca-224">Terug in de Service-klasse (WebService.cs), overschrijven de `CreateServiceInstanceListeners()` methode:</span><span class="sxs-lookup"><span data-stu-id="931ca-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span></span>

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

<span data-ttu-id="931ca-225">Dit is wanneer de Web-API *toepassing* en de OWIN *host* ten slotte voldoen aan.</span><span class="sxs-lookup"><span data-stu-id="931ca-225">This is where the Web API *application* and the OWIN *host* finally meet.</span></span> <span data-ttu-id="931ca-226">De host (OwinCommunicationListener) krijgt een exemplaar van de *toepassing* (Web-API) via het starten van de klasse.</span><span class="sxs-lookup"><span data-stu-id="931ca-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span></span> <span data-ttu-id="931ca-227">Service Fabric worden vervolgens de levenscyclus beheert.</span><span class="sxs-lookup"><span data-stu-id="931ca-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="931ca-228">Dit patroon kan doorgaans worden gevolgd door een communicatiestack.</span><span class="sxs-lookup"><span data-stu-id="931ca-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="931ca-229">Alles samenvoegen</span><span class="sxs-lookup"><span data-stu-id="931ca-229">Put it all together</span></span>
<span data-ttu-id="931ca-230">In dit voorbeeld niet hoeft verder niets te doen de `RunAsync()` methode, zodat deze onderdrukking kan gewoon worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="931ca-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="931ca-231">De laatste service-implementatie moet zeer eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="931ca-231">The final service implementation should be very simple.</span></span> <span data-ttu-id="931ca-232">Dit hoeft alleen te maken van de listener communicatie:</span><span class="sxs-lookup"><span data-stu-id="931ca-232">It only needs to create the communication listener:</span></span>

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

<span data-ttu-id="931ca-233">De volledige `OwinCommunicationListener` klasse:</span><span class="sxs-lookup"><span data-stu-id="931ca-233">The complete `OwinCommunicationListener` class:</span></span>

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

<span data-ttu-id="931ca-234">Nu dat alle benodigde onderdelen erin hebt geplaatst, wordt uw project moet eruitzien als een typische toepassing Web-API met betrouwbare Services API-toegangspunten en een OWIN-host.</span><span class="sxs-lookup"><span data-stu-id="931ca-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="931ca-235">Voer en verbinding maken via een webbrowser</span><span class="sxs-lookup"><span data-stu-id="931ca-235">Run and connect through a web browser</span></span>
<span data-ttu-id="931ca-236">Als u dit nog niet hebt gedaan, [uw ontwikkelomgeving instellen](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="931ca-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="931ca-237">U kunt nu bouwen en implementeren van uw service.</span><span class="sxs-lookup"><span data-stu-id="931ca-237">You can now build and deploy your service.</span></span> <span data-ttu-id="931ca-238">Druk op **F5** in Visual Studio kunnen bouwen en implementeren van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="931ca-238">Press **F5** in Visual Studio to build and deploy the application.</span></span> <span data-ttu-id="931ca-239">In het venster diagnostische gebeurtenissen ziet u een bericht weergegeven dat aangeeft dat de webserver wordt geopend op http://localhost:8281 /.</span><span class="sxs-lookup"><span data-stu-id="931ca-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="931ca-240">Als de poort is al geopend door een ander proces op uw computer, wordt er een fout hier.</span><span class="sxs-lookup"><span data-stu-id="931ca-240">If the port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="931ca-241">Hiermee wordt aangegeven dat de listener kan niet worden geopend.</span><span class="sxs-lookup"><span data-stu-id="931ca-241">This indicates that the listener couldn't be opened.</span></span> <span data-ttu-id="931ca-242">Als dat het geval is, probeert u een andere poort voor de eindpuntconfiguratie in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="931ca-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="931ca-243">Zodra de service wordt uitgevoerd, open een browser en Ga naar [api-http://localhost:8281-waarden](http://localhost:8281/api/values) te testen.</span><span class="sxs-lookup"><span data-stu-id="931ca-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="931ca-244">Het uit te schalen</span><span class="sxs-lookup"><span data-stu-id="931ca-244">Scale it out</span></span>
<span data-ttu-id="931ca-245">Staatloze web-apps doorgaans uitbreiden betekent meer machines toe te voegen en van de web-apps op deze draaien.</span><span class="sxs-lookup"><span data-stu-id="931ca-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span></span> <span data-ttu-id="931ca-246">Service Fabric de orchestration-engine kunt dit doen voor u wanneer nieuwe knooppunten worden toegevoegd aan een cluster.</span><span class="sxs-lookup"><span data-stu-id="931ca-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span></span> <span data-ttu-id="931ca-247">Als u exemplaren van een staatloze service maakt, kunt u het aantal exemplaren dat u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="931ca-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span></span> <span data-ttu-id="931ca-248">Service Fabric wordt dat aantal exemplaren op knooppunten in het cluster geplaatst.</span><span class="sxs-lookup"><span data-stu-id="931ca-248">Service Fabric places that number of instances on nodes in the cluster.</span></span> <span data-ttu-id="931ca-249">En ervoor dat u niet meer dan één exemplaar maken op een willekeurig knooppunt maakt.</span><span class="sxs-lookup"><span data-stu-id="931ca-249">And it makes sure not to create more than one instance on any one node.</span></span> <span data-ttu-id="931ca-250">U kunt ook opgeven dat het Service Fabric altijd een exemplaar te maken op elk knooppunt door te geven **-1** voor het aantal exemplaren.</span><span class="sxs-lookup"><span data-stu-id="931ca-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span></span> <span data-ttu-id="931ca-251">Dit zorgt ervoor dat als u knooppunten voor het schalen van uw cluster toevoegt, een exemplaar van uw stateless service wordt gemaakt op de nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="931ca-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span></span> <span data-ttu-id="931ca-252">Deze waarde is een eigenschap van het service-exemplaar, zodat deze bij het maken van een service-exemplaar is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="931ca-252">This value is a property of the service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="931ca-253">U kunt dit doen via PowerShell:</span><span class="sxs-lookup"><span data-stu-id="931ca-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="931ca-254">U kunt dit ook doen wanneer u een standaard-service in een Visual Studio-project staatloze service definieert:</span><span class="sxs-lookup"><span data-stu-id="931ca-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="931ca-255">Zie voor meer informatie over het maken van de toepassing en service-exemplaren [implementeren van een toepassing](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="931ca-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="931ca-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="931ca-256">Next steps</span></span>
[<span data-ttu-id="931ca-257">Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="931ca-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

