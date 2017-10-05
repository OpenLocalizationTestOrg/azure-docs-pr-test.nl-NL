---
title: Service-communicatie met de ASP.NET Core | Microsoft Docs
description: Informatie over het gebruik van ASP.NET Core in staatloze en stateful Reliable Services.
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
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="60aed-103">ASP.NET Core in Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="60aed-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="60aed-104">ASP.NET Core is een nieuw open source en platformoverschrijdende framework voor het bouwen van moderne cloud-gebaseerde Internet verbonden toepassingen, zoals web-apps, IoT-apps en mobiele back-ends.</span><span class="sxs-lookup"><span data-stu-id="60aed-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="60aed-105">In dit artikel is een uitgebreide handleiding voor ASP.NET Core hostingservices in Service Fabric Reliable Services met behulp van de **Microsoft.ServiceFabric.AspNetCore.** * set NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="60aed-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="60aed-106">Zie voor een inleidende zelfstudie voor ASP.NET Core in Service Fabric en instructies over het ophalen van uw ontwikkelomgeving instellen [bouwen van een webfront-end voor uw toepassing met behulp van ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="60aed-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="60aed-107">De rest van dit artikel wordt ervan uitgegaan dat u al bekend bent met ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="60aed-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="60aed-108">Als u niet het geval is, wordt aangeraden lezen via de [ASP.NET Core grondbeginselen](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="60aed-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="60aed-109">ASP.NET Core in de Service Fabric-omgeving</span><span class="sxs-lookup"><span data-stu-id="60aed-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="60aed-110">Hoewel ASP.NET Core apps op .NET Core of op het volledige .NET Framework uitvoeren kunnen, Service Fabric services momenteel kunnen alleen worden uitgevoerd op het volledige .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="60aed-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="60aed-111">Dit betekent dat wanneer u een ASP.NET Core Service Fabric-service maakt, moet u nog steeds het volledige .NET Framework richt.</span><span class="sxs-lookup"><span data-stu-id="60aed-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="60aed-112">ASP.NET Core kunnen worden gebruikt op twee verschillende manieren in Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="60aed-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="60aed-113">**Als het uitvoerbare bestand van een gast gehost**.</span><span class="sxs-lookup"><span data-stu-id="60aed-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="60aed-114">Dit is vooral op bestaande ASP.NET Core toepassingen uitvoeren op Service Fabric zonder wijzigingen code gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60aed-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="60aed-115">**Uitgevoerd binnen een betrouwbare Service**.</span><span class="sxs-lookup"><span data-stu-id="60aed-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="60aed-116">Dit kunt betere integratie met de Service Fabric-runtime en stateful ASP.NET Core services.</span><span class="sxs-lookup"><span data-stu-id="60aed-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="60aed-117">De rest van dit artikel wordt uitgelegd hoe u ASP.NET Core binnen een betrouwbare Service met de integratieonderdelen van ASP.NET Core die worden geleverd met de Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="60aed-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="60aed-118">Hosting van service Fabric-service</span><span class="sxs-lookup"><span data-stu-id="60aed-118">Service Fabric service hosting</span></span>

<span data-ttu-id="60aed-119">In Service Fabric, een of meer exemplaren en/of replica's van uw service worden uitgevoerd in een *service hostproces*, een uitvoerbaar bestand dat uw servicecode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60aed-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="60aed-120">U, als de auteur van een service, eigenaar van het hostproces van de service en Service Fabric wordt geactiveerd en wordt deze voor u bewaakt.</span><span class="sxs-lookup"><span data-stu-id="60aed-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="60aed-121">Traditionele ASP.NET (maximaal MVC 5) is nauw gekoppeld aan IIS via System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="60aed-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="60aed-122">ASP.NET Core biedt een scheiding tussen de webserver en uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="60aed-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="60aed-123">Hiermee kan webtoepassingen overdraagbaar tussen verschillende webservers en kunt u ook webservers *zelf gehost*, wat betekent dat u start een webserver in uw eigen proces, in plaats van een proces dat eigendom is van een specifieke web Server-software zoals IIS.</span><span class="sxs-lookup"><span data-stu-id="60aed-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="60aed-124">Om een combinatie van een Service Fabric-service en ASP.NET als het uitvoerbare bestand van een gastbesturingssysteem of in een betrouwbare Service, moet u ASP.NET binnen het hostproces van uw service te starten.</span><span class="sxs-lookup"><span data-stu-id="60aed-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="60aed-125">ASP.NET Core zelf hosting kunt u om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="60aed-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="60aed-126">Hosting van ASP.NET Core in een betrouwbare Service</span><span class="sxs-lookup"><span data-stu-id="60aed-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="60aed-127">Normaal gesproken zelf gehoste ASP.NET Core toepassingen maken een WebHost in het toegangspunt voor een toepassing, zoals de `static void Main()` methode in `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="60aed-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="60aed-128">In dit geval is de levenscyclus van de WebHost gebonden aan de levenscyclus van het proces.</span><span class="sxs-lookup"><span data-stu-id="60aed-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![ASP.NET Core hosten in een proces][0]

<span data-ttu-id="60aed-130">Het toegangspunt dat van toepassing is echter niet de juiste plaats te maken van een WebHost in een betrouwbare Service omdat het toegangspunt voor de toepassing alleen gebruikt wordt voor een servicetype registreren bij de Service Fabric-runtime, zodat deze exemplaren van dat servicetype kan maken.</span><span class="sxs-lookup"><span data-stu-id="60aed-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="60aed-131">De WebHost moet worden gemaakt in een betrouwbare Service zelf.</span><span class="sxs-lookup"><span data-stu-id="60aed-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="60aed-132">Binnen het hostproces van de service, kunnen service-exemplaren en/of replica's doorlopen die meerdere levenscycli.</span><span class="sxs-lookup"><span data-stu-id="60aed-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="60aed-133">Een betrouwbare Service-exemplaar wordt vertegenwoordigd door uw serviceklasse die zijn afgeleid van `StatelessService` of `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="60aed-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="60aed-134">De communicatiestack voor een service deel uitmaakt van een `ICommunicationListener` -implementatie in uw serviceklasse.</span><span class="sxs-lookup"><span data-stu-id="60aed-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="60aed-135">De `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet-pakketten bevatten implementaties van `ICommunicationListener` die starten en beheren van de ASP.NET Core WebHost voor Kestrel of WebListener in een betrouwbare Service.</span><span class="sxs-lookup"><span data-stu-id="60aed-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hosting van ASP.NET Core in een betrouwbare Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="60aed-137">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="60aed-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="60aed-138">De `ICommunicationListener` implementaties voor Kestrel en WebListener in de `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet-pakketten hebben vergelijkbare gebruikspatronen maar enigszins verschillende acties die specifiek zijn voor elke webserver worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60aed-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="60aed-139">Beide communicatielisteners bieden een constructor die de volgende argumenten:</span><span class="sxs-lookup"><span data-stu-id="60aed-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="60aed-140">**`ServiceContext serviceContext`**: De `ServiceContext` object dat informatie over de service bevat.</span><span class="sxs-lookup"><span data-stu-id="60aed-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="60aed-141">**`string endpointName`**: de naam van een `Endpoint` configuratie in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="60aed-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="60aed-142">Dit is vooral waarbij de twee communicatielisteners verschillen: WebListener **vereist** een `Endpoint` configuratie, maar niet door Kestrel.</span><span class="sxs-lookup"><span data-stu-id="60aed-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="60aed-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: een lambda die u implementeert in die u maakt en retourneren een `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="60aed-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="60aed-144">Hiermee kunt u configureren `IWebHost` de manier waarop u dat gewend bent in een toepassing ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="60aed-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="60aed-145">De lambda biedt een URL die wordt gegenereerd voor u, afhankelijk van de Service Fabric-integratie u opties gebruiken en de `Endpoint` configuratie die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="60aed-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="60aed-146">Dat URL vervolgens kan worden gewijzigd of als gebruikt-is het starten van de webserver.</span><span class="sxs-lookup"><span data-stu-id="60aed-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="60aed-147">Service Fabric-integratie middleware</span><span class="sxs-lookup"><span data-stu-id="60aed-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="60aed-148">De `Microsoft.ServiceFabric.Services.AspNetCore` NuGet-pakket bevat de `UseServiceFabricIntegration` extensiemethode op `IWebHostBuilder` die Service Fabric-bewuste middleware toevoegt.</span><span class="sxs-lookup"><span data-stu-id="60aed-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="60aed-149">Deze middleware configureert u de Kestrel of WebListener `ICommunicationListener` een unieke URL registreren bij de Service Fabric Naming Service en controleert vervolgens clientaanvragen zodat clients verbinding maken met de juiste service.</span><span class="sxs-lookup"><span data-stu-id="60aed-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="60aed-150">Dit is nodig in een omgeving met gedeelde host zoals Service Fabric, waarbij meerdere webtoepassingen kunnen uitvoeren op de dezelfde fysieke of virtuele machine, maar gebruik geen unieke hostnamen, om te voorkomen dat clients per ongeluk verbinding maken met de verkeerde service.</span><span class="sxs-lookup"><span data-stu-id="60aed-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="60aed-151">Dit scenario wordt in de volgende sectie uitvoeriger beschreven.</span><span class="sxs-lookup"><span data-stu-id="60aed-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="60aed-152">Een aanvraag van onjuiste identiteit</span><span class="sxs-lookup"><span data-stu-id="60aed-152">A case of mistaken identity</span></span>
<span data-ttu-id="60aed-153">Service-replica's, ongeacht het protocol, luisteren op de combinatie van een uniek IP: poort.</span><span class="sxs-lookup"><span data-stu-id="60aed-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="60aed-154">Wanneer een replica van de service is begonnen met luisteren op een eindpunt IP: poort, rapporteert dat eindpuntadres dat de Service Fabric Naming Service waar deze kan worden gedetecteerd door clients of andere services.</span><span class="sxs-lookup"><span data-stu-id="60aed-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="60aed-155">Als services toepassing dynamisch toegewezen poorten, kan een service-replica hetzelfde IP: poort eindpunt van een andere service die op de dezelfde fysieke of virtuele machine voorheen tegelijk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60aed-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="60aed-156">Dit kan ertoe leiden dat een client mistakely verbinding met de verkeerde service.</span><span class="sxs-lookup"><span data-stu-id="60aed-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="60aed-157">Dit kan gebeuren als de volgende reeks gebeurtenissen optreden:</span><span class="sxs-lookup"><span data-stu-id="60aed-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="60aed-158">Een service luistert op 10.0.0.1:30000 via HTTP.</span><span class="sxs-lookup"><span data-stu-id="60aed-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="60aed-159">Client-Service A wordt omgezet en adres 10.0.0.1:30000 opgehaald</span><span class="sxs-lookup"><span data-stu-id="60aed-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="60aed-160">Een service wordt verplaatst naar een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="60aed-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="60aed-161">Service B 10.0.0.1 is geplaatst en dezelfde poort 30000 tegelijk worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60aed-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="60aed-162">Client probeert verbinding maken met een service met het adres in cache 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="60aed-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="60aed-163">Client is nu is verbonden met de service geen B is verbonden met de verkeerde service.</span><span class="sxs-lookup"><span data-stu-id="60aed-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="60aed-164">Dit kan fouten veroorzaken op willekeurige tijdstippen die mogelijk moeilijk op te sporen.</span><span class="sxs-lookup"><span data-stu-id="60aed-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="60aed-165">Met unieke service-URL 's</span><span class="sxs-lookup"><span data-stu-id="60aed-165">Using unique service URLs</span></span>
<span data-ttu-id="60aed-166">Om dit te voorkomen, kunnen services een eindpunt posten naar de Naming Service met een unieke id en vervolgens valideren die de unieke id tijdens het aanvragen van clients.</span><span class="sxs-lookup"><span data-stu-id="60aed-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="60aed-167">Dit is een gezamenlijke actie tussen services in een vertrouwde omgeving van niet-onveilige-tenant.</span><span class="sxs-lookup"><span data-stu-id="60aed-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="60aed-168">Dit biedt geen verificatie van de beveiligde service in een onveilige tenant-omgeving.</span><span class="sxs-lookup"><span data-stu-id="60aed-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="60aed-169">In een vertrouwde omgeving, de middleware die wordt toegevoegd door de `UseServiceFabricIntegration` methode wordt een unieke id automatisch toegevoegd aan het adres dat is verzonden naar de Naming Service en valideert die bij elke aanvraag-id.</span><span class="sxs-lookup"><span data-stu-id="60aed-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="60aed-170">Als de id komt niet overeen met, retourneert de middleware onmiddellijk een antwoord HTTP 410 geworden.</span><span class="sxs-lookup"><span data-stu-id="60aed-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="60aed-171">Services die gebruikmaken van een dynamisch toegewezen poort moet maken gebruik van deze middleware.</span><span class="sxs-lookup"><span data-stu-id="60aed-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="60aed-172">Services die gebruikmaken van een vaste unieke poort hoeft dit probleem niet in een gezamenlijke omgeving.</span><span class="sxs-lookup"><span data-stu-id="60aed-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="60aed-173">Een unieke vaste poort wordt doorgaans gebruikt voor extern gerichte services die een bekende poort clienttoepassingen die verbinding maken met nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="60aed-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="60aed-174">Bijvoorbeeld: de meeste internetgerichte webtoepassingen poort 80 of 443 gebruikt voor web browser verbindingen.</span><span class="sxs-lookup"><span data-stu-id="60aed-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="60aed-175">In dit geval wordt worden de unieke id niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="60aed-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="60aed-176">Het volgende diagram toont de aanvraagstroom met de middleware ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="60aed-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Service Fabric ASP.NET Core-integratie][2]

<span data-ttu-id="60aed-178">Zowel Kestrel als WebListener `ICommunicationListener` implementaties dit mechanisme op exact dezelfde manier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60aed-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="60aed-179">Hoewel WebListener kunt aanvragen op basis van unieke URL-paden door de onderliggende intern onderscheiden *http.sys* poort functie die de functionaliteit voor het delen *niet* die wordt gebruikt door de WebListener `ICommunicationListener` implementatie omdat die in een HTTP 503- en HTTP 404 fout statuscodes in het scenario dat eerder is beschreven resulteert.</span><span class="sxs-lookup"><span data-stu-id="60aed-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="60aed-180">Op zijn beurt waardoor het moeilijk voor clients om te bepalen van de intentie van de fout, zoals HTTP 503- en HTTP 404 al vaak gebruikt wordt om aan te geven van andere fouten.</span><span class="sxs-lookup"><span data-stu-id="60aed-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="60aed-181">Dus zowel Kestrel en WebListener `ICommunicationListener` implementaties standaardiseren op de middleware geleverd door de `UseServiceFabricIntegration` uitbreidingsmethode zodat clients alleen hoeft uit te voeren een service-eindpunt te zetten actie op 410 HTTP-antwoorden.</span><span class="sxs-lookup"><span data-stu-id="60aed-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="60aed-182">WebListener in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="60aed-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="60aed-183">WebListener kan worden gebruikt in een betrouwbare Service door het importeren van de **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="60aed-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="60aed-184">Dit pakket bevat `WebListenerCommunicationListener`, een implementatie van `ICommunicationListener`, waarmee u een ASP.NET Core WebHost binnen een betrouwbare Service maken WebListener gebruikt als de webserver.</span><span class="sxs-lookup"><span data-stu-id="60aed-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="60aed-185">WebListener is gebaseerd op de [Windows HTTP-Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="60aed-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="60aed-186">Dit maakt gebruik van de *http.sys* kernel-stuurprogramma dat door IIS wordt gebruikt voor het verwerken van HTTP-aanvragen en deze doorsturen naar webtoepassingen die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60aed-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="60aed-187">Hierdoor kunnen meerdere processen op de dezelfde fysieke of virtuele machine naar een host-webtoepassingen op dezelfde poort ondubbelzinnig gemaakt door een unieke URL-pad of de hostnaam.</span><span class="sxs-lookup"><span data-stu-id="60aed-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="60aed-188">Deze functies zijn nuttig in Service Fabric voor het hosten van meerdere websites in hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="60aed-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="60aed-189">Het volgende diagram illustreert hoe WebListener gebruikt de *http.sys* kernel-stuurprogramma in Windows voor het delen van poort:</span><span class="sxs-lookup"><span data-stu-id="60aed-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="60aed-191">WebListener in een stateless service</span><span class="sxs-lookup"><span data-stu-id="60aed-191">WebListener in a stateless service</span></span>
<span data-ttu-id="60aed-192">Te gebruiken `WebListener` in een stateless service overschrijven de `CreateServiceInstanceListeners` methode en retourneren een `WebListenerCommunicationListener` exemplaar:</span><span class="sxs-lookup"><span data-stu-id="60aed-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

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

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="60aed-193">WebListener in een stateful service</span><span class="sxs-lookup"><span data-stu-id="60aed-193">WebListener in a stateful service</span></span>

<span data-ttu-id="60aed-194">`WebListenerCommunicationListener`op dit moment niet is ontworpen voor gebruik in stateful services vanwege problemen met de onderliggende *http.sys* poort functie voor het delen.</span><span class="sxs-lookup"><span data-stu-id="60aed-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="60aed-195">Zie voor meer informatie de volgende sectie op dynamische poorttoewijzing met WebListener.</span><span class="sxs-lookup"><span data-stu-id="60aed-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="60aed-196">Kestrel is de aanbevolen webserver voor stateful services.</span><span class="sxs-lookup"><span data-stu-id="60aed-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="60aed-197">Endpoint-configuratie</span><span class="sxs-lookup"><span data-stu-id="60aed-197">Endpoint configuration</span></span>

<span data-ttu-id="60aed-198">Een `Endpoint` configuratie is vereist voor webservers die gebruikmaken van de Windows HTTP-Server API, met inbegrip van WebListener.</span><span class="sxs-lookup"><span data-stu-id="60aed-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="60aed-199">Webservers die gebruikmaken van de Windows HTTP-Server API moeten eerst hun URL met reserveren *http.sys* (dit is normaal gesproken bewerkstelligd met de [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span><span class="sxs-lookup"><span data-stu-id="60aed-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="60aed-200">Deze actie is vereist voor verhoogde bevoegdheden die uw services standaard geen hebben.</span><span class="sxs-lookup"><span data-stu-id="60aed-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="60aed-201">De opties 'http' of 'https' voor de `Protocol` eigenschap van de `Endpoint` configuratie in *ServiceManifest.xml* worden gebruikt om specifiek te instrueren van de Service Fabric-runtime registratie van een URL met  *HTTP.sys* op uw rekening met de [ *sterk jokertekens* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL-voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="60aed-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="60aed-202">Om bijvoorbeeld te reserveren `http://+:80` voor een service de volgende configuratie moet worden gebruikt in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="60aed-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

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

<span data-ttu-id="60aed-203">En de naam van het eindpunt moet worden doorgegeven aan de `WebListenerCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="60aed-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

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

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="60aed-204">WebListener gebruiken met een statische poort</span><span class="sxs-lookup"><span data-stu-id="60aed-204">Use WebListener with a static port</span></span>
<span data-ttu-id="60aed-205">Als u wilt gebruiken een statische poort met WebListener, geef het poortnummer in de `Endpoint` configuratie:</span><span class="sxs-lookup"><span data-stu-id="60aed-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="60aed-206">WebListener gebruiken met een dynamische poort</span><span class="sxs-lookup"><span data-stu-id="60aed-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="60aed-207">Als u wilt gebruiken een dynamisch toegewezen poort met WebListener, laat de `Port` eigenschap in de `Endpoint` configuratie:</span><span class="sxs-lookup"><span data-stu-id="60aed-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="60aed-208">Merk op dat een dynamische poort is toegewezen door een `Endpoint` configuratie biedt slechts één poort *per hostproces*.</span><span class="sxs-lookup"><span data-stu-id="60aed-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="60aed-209">Het huidige model van de Service Fabric-hosting kunt meerdere exemplaren van de service en/of replica's worden gehost in hetzelfde proces, wat betekent dat elke dezelfde poort delen als toegewezen via de `Endpoint` configuratie.</span><span class="sxs-lookup"><span data-stu-id="60aed-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="60aed-210">Meerdere exemplaren van WebListener kunnen delen een poort die door de onderliggende *http.sys* poort delen onderdeel, maar die niet wordt ondersteund door `WebListenerCommunicationListener` vanwege de problemen die het geeft voor clientaanvragen.</span><span class="sxs-lookup"><span data-stu-id="60aed-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="60aed-211">Voor het gebruik van dynamische poort is Kestrel de aanbevolen webserver.</span><span class="sxs-lookup"><span data-stu-id="60aed-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="60aed-212">Kestrel in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="60aed-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="60aed-213">Kestrel kan worden gebruikt in een betrouwbare Service door het importeren van de **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="60aed-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="60aed-214">Dit pakket bevat `KestrelCommunicationListener`, een implementatie van `ICommunicationListener`, waarmee u een ASP.NET Core WebHost binnen een betrouwbare Service maken Kestrel gebruikt als de webserver.</span><span class="sxs-lookup"><span data-stu-id="60aed-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="60aed-215">Kestrel is dat een platformoverschrijdende webserver voor ASP.NET Core op basis van libuv, een platformoverschrijdende asynchrone i/o-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="60aed-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="60aed-216">In tegenstelling tot WebListener, Kestrel gebruikt geen een gecentraliseerde eindpunt manager zoals *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="60aed-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="60aed-217">En in tegenstelling tot WebListener, Kestrel biedt geen ondersteuning voor poort delen tussen meerdere processen.</span><span class="sxs-lookup"><span data-stu-id="60aed-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="60aed-218">Elk exemplaar van Kestrel moet een unieke poort gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60aed-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="60aed-220">Kestrel in een stateless service</span><span class="sxs-lookup"><span data-stu-id="60aed-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="60aed-221">Te gebruiken `Kestrel` in een stateless service overschrijven de `CreateServiceInstanceListeners` methode en retourneren een `KestrelCommunicationListener` exemplaar:</span><span class="sxs-lookup"><span data-stu-id="60aed-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="60aed-222">Kestrel in een stateful service</span><span class="sxs-lookup"><span data-stu-id="60aed-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="60aed-223">Te gebruiken `Kestrel` in een stateful service overschrijven de `CreateServiceReplicaListeners` methode en retourneren een `KestrelCommunicationListener` exemplaar:</span><span class="sxs-lookup"><span data-stu-id="60aed-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

<span data-ttu-id="60aed-224">In dit voorbeeld wordt een singleton-instantie van `IReliableStateManager` is opgegeven voor de WebHost afhankelijkheid injectie container.</span><span class="sxs-lookup"><span data-stu-id="60aed-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="60aed-225">Dit is niet strikt noodzakelijk zijn, maar Hiermee kunt u gebruiken `IReliableStateManager` en betrouwbare verzamelingen in uw MVC-controller-actiemethoden.</span><span class="sxs-lookup"><span data-stu-id="60aed-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="60aed-226">Houd er rekening mee dat een `Endpoint` configuratienaam is **niet** opgegeven voor `KestrelCommunicationListener` in een stateful service.</span><span class="sxs-lookup"><span data-stu-id="60aed-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="60aed-227">Dit wordt uitgelegd in de volgende sectie uitvoeriger.</span><span class="sxs-lookup"><span data-stu-id="60aed-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="60aed-228">Endpoint-configuratie</span><span class="sxs-lookup"><span data-stu-id="60aed-228">Endpoint configuration</span></span>
<span data-ttu-id="60aed-229">Een `Endpoint` configuratie is niet vereist voor het gebruik van Kestrel.</span><span class="sxs-lookup"><span data-stu-id="60aed-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="60aed-230">Kestrel is een eenvoudige zelfstandige webserver; in tegenstelling tot WebListener (of HttpListener), hoeft deze niet een `Endpoint` configuratie in *ServiceManifest.xml* omdat er geen registratie voorafgaand aan de URL nodig.</span><span class="sxs-lookup"><span data-stu-id="60aed-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="60aed-231">Kestrel gebruiken met een statische poort</span><span class="sxs-lookup"><span data-stu-id="60aed-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="60aed-232">Een statische poort kan worden geconfigureerd in de `Endpoint` ServiceManifest.xml-configuratie voor gebruik met Kestrel.</span><span class="sxs-lookup"><span data-stu-id="60aed-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="60aed-233">Hoewel dit niet strikt noodzakelijk is, heeft deze twee mogelijke voordelen:</span><span class="sxs-lookup"><span data-stu-id="60aed-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="60aed-234">Als de poort niet in het poortbereik van de toepassing valt, wordt het geopend via de firewall van het besturingssysteem door de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="60aed-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="60aed-235">De URL die u via `KestrelCommunicationListener` deze poort wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60aed-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="60aed-236">Als een `Endpoint` is geconfigureerd, de naam moet worden doorgegeven in de `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="60aed-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="60aed-237">Als een `Endpoint` configuratie wordt niet gebruikt, laat u de naam in de `KestrelCommunicationListener` constructor.</span><span class="sxs-lookup"><span data-stu-id="60aed-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="60aed-238">In dit geval wordt een dynamische poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60aed-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="60aed-239">Zie de volgende sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="60aed-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="60aed-240">Kestrel gebruiken met een dynamische poort</span><span class="sxs-lookup"><span data-stu-id="60aed-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="60aed-241">Kestrel niet gebruiken de automatische poorttoewijzing van de `Endpoint` configuratie in ServiceManifest.xml, omdat automatische poorttoewijzing van een `Endpoint` configuratie wijst een unieke poort per *proces host*, en een proces voor één host kan meerdere exemplaren van Kestrel bevatten.</span><span class="sxs-lookup"><span data-stu-id="60aed-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="60aed-242">Aangezien Kestrel biedt geen ondersteuning voor het delen van de poort, werkt dit niet zoals elk exemplaar Kestrel moet worden geopend op een unieke poort.</span><span class="sxs-lookup"><span data-stu-id="60aed-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="60aed-243">Voor het gebruik van dynamische poorttoewijzing met Kestrel, laat u gewoon de `Endpoint` configuratie in ServiceManifest.xml volledig, en geeft u de naam van een eindpunt niet door de `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="60aed-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="60aed-244">In deze configuratie `KestrelCommunicationListener` wordt automatisch een niet-gebruikte poort selecteren in het poortbereik van toepassing.</span><span class="sxs-lookup"><span data-stu-id="60aed-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="60aed-245">Scenario's en configuraties</span><span class="sxs-lookup"><span data-stu-id="60aed-245">Scenarios and configurations</span></span>
<span data-ttu-id="60aed-246">In deze sectie worden de volgende scenario's beschreven en de aanbevolen combinatie van de webserver, poortconfiguratie, opties voor Service Fabric-integratie en diverse instellingen voor een goed functionerende service biedt:</span><span class="sxs-lookup"><span data-stu-id="60aed-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="60aed-247">Extern blootgesteld ASP.NET Core staatloze service</span><span class="sxs-lookup"><span data-stu-id="60aed-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="60aed-248">Alleen intern-ASP.NET Core staatloze service</span><span class="sxs-lookup"><span data-stu-id="60aed-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="60aed-249">Alleen intern-ASP.NET Core stateful service</span><span class="sxs-lookup"><span data-stu-id="60aed-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="60aed-250">Een **extern blootgesteld** -service maakt dat toegang biedt tot een eindpunt dat bereikbaar is vanaf buiten het cluster, meestal via een load balancer.</span><span class="sxs-lookup"><span data-stu-id="60aed-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="60aed-251">Een **alleen interne** -service is een waarvan eindpunt alleen bereikbaar is vanaf binnen het cluster is.</span><span class="sxs-lookup"><span data-stu-id="60aed-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="60aed-252">Stateful service-eindpunten moeten in het algemeen niet worden blootgesteld aan Internet.</span><span class="sxs-lookup"><span data-stu-id="60aed-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="60aed-253">Clusters die zich achter de load balancers die zich niet bewust zijn van de oplossing van het Service Fabric-service, zoals Azure Load Balancer, zich niet meer zichtbaar stateful services maken, omdat de load balancer kan niet worden om te zoeken en verkeer naar de juiste sturen stateful service-replica.</span><span class="sxs-lookup"><span data-stu-id="60aed-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="60aed-254">Extern blootgesteld ASP.NET Core stateless services</span><span class="sxs-lookup"><span data-stu-id="60aed-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="60aed-255">WebListener is de aanbevolen webserver voor front-end-services die externe, internetgerichte HTTP-eindpunten in Windows.</span><span class="sxs-lookup"><span data-stu-id="60aed-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="60aed-256">Dit biedt betere bescherming tegen aanvallen en functies die Kestrel niet, zoals Windows-verificatie en -poort delen bestaat ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="60aed-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="60aed-257">Kestrel wordt niet ondersteund als een edge (internetgerichte)-server op dit moment.</span><span class="sxs-lookup"><span data-stu-id="60aed-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="60aed-258">Een reverse proxy-server zoals IIS of Nginx moet worden gebruikt voor het afhandelen van verkeer van het openbare Internet.</span><span class="sxs-lookup"><span data-stu-id="60aed-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="60aed-259">Wanneer blootgesteld aan Internet, moet een stateless service een bekende en stabiele eindpunt dat bereikbaar is via een load balancer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60aed-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="60aed-260">Dit is de URL die u aan gebruikers van uw toepassing biedt.</span><span class="sxs-lookup"><span data-stu-id="60aed-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="60aed-261">De volgende configuratie wordt aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="60aed-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="60aed-262">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="60aed-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60aed-263">Webserver</span><span class="sxs-lookup"><span data-stu-id="60aed-263">Web server</span></span> | <span data-ttu-id="60aed-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="60aed-264">WebListener</span></span> | <span data-ttu-id="60aed-265">Als de service is alleen beschikbaar worden gemaakt met een vertrouwd netwerk, een intranet kan Kestrel worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60aed-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="60aed-266">Anders is WebListener de gewenste optie.</span><span class="sxs-lookup"><span data-stu-id="60aed-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="60aed-267">Poortconfiguratie</span><span class="sxs-lookup"><span data-stu-id="60aed-267">Port configuration</span></span> | <span data-ttu-id="60aed-268">Statische</span><span class="sxs-lookup"><span data-stu-id="60aed-268">static</span></span> | <span data-ttu-id="60aed-269">Een bekende statische poort moet worden geconfigureerd in de `Endpoints` configuratie van ServiceManifest.xml, zoals 80 voor HTTP en 443 voor HTTPS.</span><span class="sxs-lookup"><span data-stu-id="60aed-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="60aed-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="60aed-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="60aed-271">Geen</span><span class="sxs-lookup"><span data-stu-id="60aed-271">None</span></span> | <span data-ttu-id="60aed-272">De `ServiceFabricIntegrationOptions.None` moet worden gebruikt bij het Service Fabric-integratie middleware configureren zodat de service niet probeert te valideren van binnenkomende aanvragen voor een unieke id.</span><span class="sxs-lookup"><span data-stu-id="60aed-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="60aed-273">Externe gebruikers van uw toepassing weet niet de unieke gegevens die worden gebruikt door de middleware.</span><span class="sxs-lookup"><span data-stu-id="60aed-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="60aed-274">Aantal exemplaren</span><span class="sxs-lookup"><span data-stu-id="60aed-274">Instance Count</span></span> | <span data-ttu-id="60aed-275">-1</span><span class="sxs-lookup"><span data-stu-id="60aed-275">-1</span></span> | <span data-ttu-id="60aed-276">In een typische gebruiksvoorbeelden, moet het aantal exemplaren instellen '1' worden ingesteld zodat een exemplaar is beschikbaar op alle knooppunten die verkeer van een load balancer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="60aed-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="60aed-277">Als meerdere extern blootgestelde services dezelfde set knooppunten delen, moet een unieke maar stabiele URL-pad worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60aed-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="60aed-278">Dit kan worden bereikt door het wijzigen van de URL die is opgegeven bij het configureren van IWebHost.</span><span class="sxs-lookup"><span data-stu-id="60aed-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="60aed-279">Houd er rekening mee dat dit alleen van toepassing op WebListener.</span><span class="sxs-lookup"><span data-stu-id="60aed-279">Note this applies to WebListener only.</span></span>

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

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="60aed-280">Alleen intern staatloze ASP.NET Core-service</span><span class="sxs-lookup"><span data-stu-id="60aed-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="60aed-281">Stateless services die alleen worden aangeroepen vanuit binnen het cluster moeten unieke URL's gebruiken en dynamisch toegewezen poorten om ervoor te zorgen samenwerking tussen meerdere services.</span><span class="sxs-lookup"><span data-stu-id="60aed-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="60aed-282">De volgende configuratie wordt aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="60aed-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="60aed-283">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="60aed-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60aed-284">Webserver</span><span class="sxs-lookup"><span data-stu-id="60aed-284">Web server</span></span> | <span data-ttu-id="60aed-285">kestrel</span><span class="sxs-lookup"><span data-stu-id="60aed-285">Kestrel</span></span> | <span data-ttu-id="60aed-286">Hoewel WebListener kan worden gebruikt voor interne stateless services, is Kestrel de aanbevolen server zodat meerdere exemplaren van de service voor het delen van een host.</span><span class="sxs-lookup"><span data-stu-id="60aed-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="60aed-287">Poortconfiguratie</span><span class="sxs-lookup"><span data-stu-id="60aed-287">Port configuration</span></span> | <span data-ttu-id="60aed-288">dynamisch toegewezen</span><span class="sxs-lookup"><span data-stu-id="60aed-288">dynamically assigned</span></span> | <span data-ttu-id="60aed-289">Meerdere replica's van een stateful service kunnen een hostproces of hostbesturingssysteem delen en moeten dus unieke poorten.</span><span class="sxs-lookup"><span data-stu-id="60aed-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="60aed-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="60aed-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="60aed-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="60aed-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="60aed-292">Bij toewijzing van de dynamische poort is deze instelling voorkomt dat het probleem onjuiste identiteit is eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="60aed-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="60aed-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="60aed-293">InstanceCount</span></span> | <span data-ttu-id="60aed-294">alle</span><span class="sxs-lookup"><span data-stu-id="60aed-294">any</span></span> | <span data-ttu-id="60aed-295">Het aantal exemplaren instelling kan worden ingesteld op een andere waarde nodig om de service.</span><span class="sxs-lookup"><span data-stu-id="60aed-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="60aed-296">Alleen intern stateful ASP.NET Core-service</span><span class="sxs-lookup"><span data-stu-id="60aed-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="60aed-297">Stateful services die alleen worden aangeroepen vanuit binnen het cluster moeten dynamisch toegewezen poorten gebruiken om ervoor te zorgen samenwerking tussen meerdere services.</span><span class="sxs-lookup"><span data-stu-id="60aed-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="60aed-298">De volgende configuratie wordt aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="60aed-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="60aed-299">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="60aed-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60aed-300">Webserver</span><span class="sxs-lookup"><span data-stu-id="60aed-300">Web server</span></span> | <span data-ttu-id="60aed-301">kestrel</span><span class="sxs-lookup"><span data-stu-id="60aed-301">Kestrel</span></span> | <span data-ttu-id="60aed-302">De `WebListenerCommunicationListener` is niet ontworpen voor gebruik door stateful services waarin de replica's een hostproces delen.</span><span class="sxs-lookup"><span data-stu-id="60aed-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="60aed-303">Poortconfiguratie</span><span class="sxs-lookup"><span data-stu-id="60aed-303">Port configuration</span></span> | <span data-ttu-id="60aed-304">dynamisch toegewezen</span><span class="sxs-lookup"><span data-stu-id="60aed-304">dynamically assigned</span></span> | <span data-ttu-id="60aed-305">Meerdere replica's van een stateful service kunnen een hostproces of hostbesturingssysteem delen en moeten dus unieke poorten.</span><span class="sxs-lookup"><span data-stu-id="60aed-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="60aed-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="60aed-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="60aed-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="60aed-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="60aed-308">Bij toewijzing van de dynamische poort is deze instelling voorkomt dat het probleem onjuiste identiteit is eerder beschreven.</span><span class="sxs-lookup"><span data-stu-id="60aed-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="60aed-309">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60aed-309">Next steps</span></span>
[<span data-ttu-id="60aed-310">Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="60aed-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
