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
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="8026c-103">ASP.NET Core in Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8026c-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="8026c-104">ASP.NET Core is een nieuw open source en platformoverschrijdende framework voor het bouwen van moderne cloud-gebaseerde Internet verbonden toepassingen, zoals web-apps, IoT-apps en mobiele back-ends.</span><span class="sxs-lookup"><span data-stu-id="8026c-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="8026c-105">Dit artikel is een uitgebreidere handleiding toohosting ASP.NET Core services in Service Fabric Reliable Services met behulp van Hallo **Microsoft.ServiceFabric.AspNetCore.** * set NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="8026c-105">This article is an in-depth guide toohosting ASP.NET Core services in Service Fabric Reliable Services using hello **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="8026c-106">Zie voor een inleidende zelfstudie voor ASP.NET Core in Service Fabric en instructies over het ophalen van uw ontwikkelomgeving instellen [bouwen van een webfront-end voor uw toepassing met behulp van ASP.NET Core](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="8026c-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="8026c-107">Hallo rest van dit artikel wordt ervan uitgegaan dat u al bekend bent met ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8026c-107">hello rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="8026c-108">Als u niet het geval is, wordt aangeraden lezen via Hallo [ASP.NET Core grondbeginselen](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="8026c-108">If not, we recommend reading through hello [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-hello-service-fabric-environment"></a><span data-ttu-id="8026c-109">ASP.NET Core in Hallo Service Fabric-omgeving</span><span class="sxs-lookup"><span data-stu-id="8026c-109">ASP.NET Core in hello Service Fabric environment</span></span>

<span data-ttu-id="8026c-110">Terwijl ASP.NET Core apps kunnen worden uitgevoerd op .NET Core of volledige .NET Framework, Service Fabric-services momenteel kan alleen worden uitgevoerd op Hallo Hallo volledige .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8026c-110">While ASP.NET Core apps can run on .NET Core or on hello full .NET Framework, Service Fabric services currently can only run on hello full .NET Framework.</span></span> <span data-ttu-id="8026c-111">Dit betekent dat wanneer u een ASP.NET Core Service Fabric-service maakt, moet nog steeds gericht Hallo volledige .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8026c-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target hello full .NET Framework.</span></span>

<span data-ttu-id="8026c-112">ASP.NET Core kunnen worden gebruikt op twee verschillende manieren in Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="8026c-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="8026c-113">**Als het uitvoerbare bestand van een gast gehost**.</span><span class="sxs-lookup"><span data-stu-id="8026c-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="8026c-114">Dit is vooral gebruikte toorun bestaande ASP.NET Core toepassingen op Service Fabric zonder wijzigingen code.</span><span class="sxs-lookup"><span data-stu-id="8026c-114">This is primarily used toorun existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="8026c-115">**Uitgevoerd binnen een betrouwbare Service**.</span><span class="sxs-lookup"><span data-stu-id="8026c-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="8026c-116">Dit kunt betere integratie met Hallo Service Fabric-runtime en stateful ASP.NET Core services.</span><span class="sxs-lookup"><span data-stu-id="8026c-116">This allows better integration with hello Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="8026c-117">Hallo rest van dit artikel wordt uitgelegd hoe toouse ASP.NET Core binnen een betrouwbare Service met ASP.NET Core integratieonderdelen die worden geleverd met Service Fabric SDK Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8026c-117">hello rest of this article explains how toouse ASP.NET Core inside a Reliable Service using hello ASP.NET Core integration components that ship with hello Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="8026c-118">Hosting van service Fabric-service</span><span class="sxs-lookup"><span data-stu-id="8026c-118">Service Fabric service hosting</span></span>

<span data-ttu-id="8026c-119">In Service Fabric, een of meer exemplaren en/of replica's van uw service worden uitgevoerd in een *service hostproces*, een uitvoerbaar bestand dat uw servicecode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8026c-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="8026c-120">U, als de auteur van een service, de eigenaar hostproces Hallo-service en Service Fabric wordt geactiveerd en controleert u het voor u.</span><span class="sxs-lookup"><span data-stu-id="8026c-120">You, as a service author, own hello service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="8026c-121">Traditionele ASP.NET (omhoog tooMVC 5) is nauw gekoppeld tooIIS via System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="8026c-121">Traditional ASP.NET (up tooMVC 5) is tightly coupled tooIIS through System.Web.dll.</span></span> <span data-ttu-id="8026c-122">ASP.NET Core biedt een scheiding tussen Hallo-webserver en uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="8026c-122">ASP.NET Core provides a separation between hello web server and your web application.</span></span> <span data-ttu-id="8026c-123">Hiermee kan de web-toepassingen toobe draagbare tussen verschillende webservers en kunt u ook web servers toobe *zelf gehost*, wat betekent dat u kunt een webserver starten in uw eigen proces als tegengestelde tooa proces dat eigendom is van een specifieke web Server-software zoals IIS.</span><span class="sxs-lookup"><span data-stu-id="8026c-123">This allows web applications toobe portable between different web servers and also allows web servers toobe *self-hosted*, which means you can start a web server in your own process, as opposed tooa process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="8026c-124">U moet in volgorde toocombine een Service Fabric-service en ASP.NET als het uitvoerbare bestand van een gastbesturingssysteem of in een betrouwbare Service kunnen toostart ASP.NET zijn binnen het hostproces van uw service.</span><span class="sxs-lookup"><span data-stu-id="8026c-124">In order toocombine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able toostart ASP.NET inside your service host process.</span></span> <span data-ttu-id="8026c-125">ASP.NET Core zelf hosten, kunt u toodo dit.</span><span class="sxs-lookup"><span data-stu-id="8026c-125">ASP.NET Core self-hosting allows you toodo this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="8026c-126">Hosting van ASP.NET Core in een betrouwbare Service</span><span class="sxs-lookup"><span data-stu-id="8026c-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="8026c-127">Normaal gesproken zelf gehoste ASP.NET Core toepassingen een WebHost maken in het toegangspunt van een toepassing, zoals Hallo `static void Main()` methode in `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="8026c-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as hello `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="8026c-128">In dit geval is Hallo levenscyclus van Hallo WebHost gebonden toohello levenscyclus van Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="8026c-128">In this case, hello lifecycle of hello WebHost is bound toohello lifecycle of hello process.</span></span>

![ASP.NET Core hosten in een proces][0]

<span data-ttu-id="8026c-130">Echter ingangspunt voor toepassing hello niet Hallo goede plek toocreate een WebHost in een betrouwbare Service, omdat het ingangspunt Hallo-toepassing wordt alleen gebruikt tooregister een service Typ met Hallo Service Fabric-runtime, zodat deze exemplaren van die service mogelijk maken type.</span><span class="sxs-lookup"><span data-stu-id="8026c-130">However, hello application entry point is not hello right place toocreate a WebHost in a Reliable Service, because hello application entry point is only used tooregister a service type with hello Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="8026c-131">Hallo WebHost moet worden gemaakt in een betrouwbare Service zelf.</span><span class="sxs-lookup"><span data-stu-id="8026c-131">hello WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="8026c-132">In hostproces Hallo-service, kunnen service-exemplaren en/of replica's doorlopen die meerdere levenscycli.</span><span class="sxs-lookup"><span data-stu-id="8026c-132">Within hello service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="8026c-133">Een betrouwbare Service-exemplaar wordt vertegenwoordigd door uw serviceklasse die zijn afgeleid van `StatelessService` of `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="8026c-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="8026c-134">Hallo communicatiestack voor een service deel uitmaakt van een `ICommunicationListener` -implementatie in uw serviceklasse.</span><span class="sxs-lookup"><span data-stu-id="8026c-134">hello communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="8026c-135">Hallo `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet-pakketten bevatten implementaties van `ICommunicationListener` die starten en te beheren Hallo ASP.NET Core WebHost voor Kestrel of WebListener in een betrouwbare Service.</span><span class="sxs-lookup"><span data-stu-id="8026c-135">hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage hello ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hosting van ASP.NET Core in een betrouwbare Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="8026c-137">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="8026c-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="8026c-138">Hallo `ICommunicationListener` implementaties voor Kestrel en WebListener in Hallo `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet-pakketten vergelijkbare gebruikspatronen hebben maar enigszins andere acties specifieke tooeach webserver uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8026c-138">hello `ICommunicationListener` implementations for Kestrel and WebListener in hello  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific tooeach web server.</span></span> 

<span data-ttu-id="8026c-139">Beide communicatielisteners bieden een constructor die Hallo volgende argumenten:</span><span class="sxs-lookup"><span data-stu-id="8026c-139">Both communication listeners provide a constructor that takes hello following arguments:</span></span>
 - <span data-ttu-id="8026c-140">**`ServiceContext serviceContext`**: Hallo `ServiceContext` object dat informatie bevat over Hallo waarop service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8026c-140">**`ServiceContext serviceContext`**: hello `ServiceContext` object that contains information about hello running service.</span></span>
 - <span data-ttu-id="8026c-141">**`string endpointName`**: Hallo-naam van een `Endpoint` configuratie in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="8026c-141">**`string endpointName`**: hello name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="8026c-142">Dit is vooral waar Hallo twee communicatielisteners verschillen: WebListener **vereist** een `Endpoint` configuratie, maar niet door Kestrel.</span><span class="sxs-lookup"><span data-stu-id="8026c-142">This is primarily where hello two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="8026c-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: een lambda die u implementeert in die u maakt en retourneren een `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="8026c-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="8026c-144">Hiermee kunt u tooconfigure `IWebHost` Hallo manier u dat gewend bent in een toepassing ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8026c-144">This allows you tooconfigure `IWebHost` hello way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="8026c-145">Hallo lambda biedt een URL die wordt gegenereerd voor u, afhankelijk van de Service Fabric-integratie Hallo u opties gebruik en Hallo `Endpoint` configuratie die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="8026c-145">hello lambda provides a URL which is generated for you depending on hello Service Fabric integration options you use and hello `Endpoint` configuration you provide.</span></span> <span data-ttu-id="8026c-146">Dat URL vervolgens kan worden gewijzigd of als gebruikt-toostart Hallo web server.</span><span class="sxs-lookup"><span data-stu-id="8026c-146">That URL can then be modified or used as-is toostart hello web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="8026c-147">Service Fabric-integratie middleware</span><span class="sxs-lookup"><span data-stu-id="8026c-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="8026c-148">Hallo `Microsoft.ServiceFabric.Services.AspNetCore` NuGet-pakket bevat Hallo `UseServiceFabricIntegration` extensiemethode op `IWebHostBuilder` die Service Fabric-bewuste middleware toevoegt.</span><span class="sxs-lookup"><span data-stu-id="8026c-148">hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes hello `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="8026c-149">Deze middleware configureert Hallo Kestrel of WebListener `ICommunicationListener` tooregister een unieke service-URL met Service Fabric Naming Service Hallo en controleert vervolgens client aanvragen tooensure clients verbinding maken toohello juiste service.</span><span class="sxs-lookup"><span data-stu-id="8026c-149">This middleware configures hello Kestrel or WebListener `ICommunicationListener` tooregister a unique service URL with hello Service Fabric Naming Service and then validates client requests tooensure clients are connecting toohello right service.</span></span> <span data-ttu-id="8026c-150">Dit is nodig in een omgeving met gedeelde host zoals Service Fabric, waarbij meerdere webtoepassingen kunnen uitvoeren op Hallo dezelfde fysieke of virtuele machine, maar gebruik geen unieke hostnamen tooprevent clients per ongeluk de verkeerde service toohello verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="8026c-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on hello same physical or virtual machine but do not use unique host names, tooprevent clients from mistakenly connecting toohello wrong service.</span></span> <span data-ttu-id="8026c-151">Dit scenario wordt beschreven in de volgende sectie Hallo nader.</span><span class="sxs-lookup"><span data-stu-id="8026c-151">This scenario is described in more detail in hello next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="8026c-152">Een aanvraag van onjuiste identiteit</span><span class="sxs-lookup"><span data-stu-id="8026c-152">A case of mistaken identity</span></span>
<span data-ttu-id="8026c-153">Service-replica's, ongeacht het protocol, luisteren op de combinatie van een uniek IP: poort.</span><span class="sxs-lookup"><span data-stu-id="8026c-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="8026c-154">Wanneer een replica van de service is begonnen met luisteren op een eindpunt IP: poort, rapporteert dat eindpunt adres toohello Service Fabric Naming Service waar deze kan worden gedetecteerd door clients of andere services.</span><span class="sxs-lookup"><span data-stu-id="8026c-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address toohello Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="8026c-155">Als u services gebruiken toepassing dynamisch toegewezen poorten, een service-replica kunnen tegelijk gebruiken hetzelfde IP: poort eindpunt van een andere service die voorheen op Hallo Hallo dezelfde fysieke of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8026c-155">If services use dynamically-assigned application ports, a service replica may coincidentally use hello same IP:port endpoint of another service that was previously on hello same physical or virtual machine.</span></span> <span data-ttu-id="8026c-156">Dit kan ertoe leiden dat een client toomistakely verbinding maken met de verkeerde toohello-service.</span><span class="sxs-lookup"><span data-stu-id="8026c-156">This can cause a client toomistakely connect toohello wrong service.</span></span> <span data-ttu-id="8026c-157">Dit kan gebeuren als de volgende reeks gebeurtenissen Hallo optreden:</span><span class="sxs-lookup"><span data-stu-id="8026c-157">This can happen if hello following sequence of events occur:</span></span>

 1. <span data-ttu-id="8026c-158">Een service luistert op 10.0.0.1:30000 via HTTP.</span><span class="sxs-lookup"><span data-stu-id="8026c-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="8026c-159">Client-Service A wordt omgezet en adres 10.0.0.1:30000 opgehaald</span><span class="sxs-lookup"><span data-stu-id="8026c-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="8026c-160">Een ander knooppunt voor verplaatst tooa-service.</span><span class="sxs-lookup"><span data-stu-id="8026c-160">Service A moves tooa different node.</span></span>
 4. <span data-ttu-id="8026c-161">Service B 10.0.0.1 is geplaatst en tegelijk maakt gebruik van dezelfde poort 30000 Hallo.</span><span class="sxs-lookup"><span data-stu-id="8026c-161">Service B is placed on 10.0.0.1 and coincidentally uses hello same port 30000.</span></span>
 5. <span data-ttu-id="8026c-162">Client probeert tooconnect tooservice A met het adres in cache 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="8026c-162">Client attempts tooconnect tooservice A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="8026c-163">Client is nu is verbonden tooservice geen B is verbonden toohello verkeerde service.</span><span class="sxs-lookup"><span data-stu-id="8026c-163">Client is now successfully connected tooservice B not realizing it is connected toohello wrong service.</span></span>

<span data-ttu-id="8026c-164">Dit kan fouten veroorzaken op willekeurige tijdstippen die moeilijk toodiagnose kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="8026c-164">This can cause bugs at random times that can be difficult toodiagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="8026c-165">Met unieke service-URL 's</span><span class="sxs-lookup"><span data-stu-id="8026c-165">Using unique service URLs</span></span>
<span data-ttu-id="8026c-166">tooprevent deze services kunt plaatsen van een eindpunt toohello Naming Service met een unieke id en vervolgens valideren die de unieke id tijdens het aanvragen van clients.</span><span class="sxs-lookup"><span data-stu-id="8026c-166">tooprevent this, services can post an endpoint toohello Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="8026c-167">Dit is een gezamenlijke actie tussen services in een vertrouwde omgeving van niet-onveilige-tenant.</span><span class="sxs-lookup"><span data-stu-id="8026c-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="8026c-168">Dit biedt geen verificatie van de beveiligde service in een onveilige tenant-omgeving.</span><span class="sxs-lookup"><span data-stu-id="8026c-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="8026c-169">In een vertrouwde omgeving Hallo middleware die wordt toegevoegd door Hallo `UseServiceFabricIntegration` methode automatisch een unieke id toohello-adres dat wordt gepost toohello Naming Service en valideert die bij elke aanvraag-id worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8026c-169">In a trusted environment, hello middleware that's added by hello `UseServiceFabricIntegration` method automatically appends a unique identifier toohello address that is posted toohello Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="8026c-170">Als het Hallo-id komt niet overeen met, retourneert Hallo middleware onmiddellijk een antwoord HTTP 410 geworden.</span><span class="sxs-lookup"><span data-stu-id="8026c-170">If hello identifier does not match, hello middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="8026c-171">Services die gebruikmaken van een dynamisch toegewezen poort moet maken gebruik van deze middleware.</span><span class="sxs-lookup"><span data-stu-id="8026c-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="8026c-172">Services die gebruikmaken van een vaste unieke poort hoeft dit probleem niet in een gezamenlijke omgeving.</span><span class="sxs-lookup"><span data-stu-id="8026c-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="8026c-173">Een unieke vaste poort wordt doorgaans gebruikt voor extern gerichte services die voor client toepassingen tooconnect naar een bekende poort nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="8026c-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications tooconnect to.</span></span> <span data-ttu-id="8026c-174">Bijvoorbeeld: de meeste internetgerichte webtoepassingen poort 80 of 443 gebruikt voor web browser verbindingen.</span><span class="sxs-lookup"><span data-stu-id="8026c-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="8026c-175">In dit geval wordt worden de unieke id Hallo niet ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8026c-175">In this case, hello unique identifier should not be enabled.</span></span>

<span data-ttu-id="8026c-176">Hallo volgende diagram toont Hallo aanvragen bewegen met Hallo middleware ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="8026c-176">hello following diagram shows hello request flow with hello middleware enabled:</span></span>

![Service Fabric ASP.NET Core-integratie][2]

<span data-ttu-id="8026c-178">Zowel Kestrel als WebListener `ICommunicationListener` implementaties gebruikt dit mechanisme in exact Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="8026c-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly hello same way.</span></span> <span data-ttu-id="8026c-179">Hoewel WebListener kunt aanvragen op basis van unieke URL-paden met onderliggende hello intern onderscheiden *http.sys* poort functie die de functionaliteit voor het delen *niet* die wordt gebruikt door Hallo WebListener `ICommunicationListener` implementatie omdat die in een HTTP 503- en HTTP 404 status foutcodes in Hallo scenario eerder beschreven resulteert.</span><span class="sxs-lookup"><span data-stu-id="8026c-179">Although WebListener can internally differentiate requests based on unique URL paths using hello underlying *http.sys* port sharing feature, that functionality is *not* used by hello WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in hello scenario described earlier.</span></span> <span data-ttu-id="8026c-180">Op zijn beurt waardoor het moeilijk voor clients toodetermine Hallo bedoeling van Hallo fout, zoals HTTP 503- en HTTP 404 al veelgebruikte tooindicate zijn andere fouten.</span><span class="sxs-lookup"><span data-stu-id="8026c-180">That in turn makes it very difficult for clients toodetermine hello intent of hello error, as HTTP 503 and HTTP 404 are already commonly used tooindicate other errors.</span></span> <span data-ttu-id="8026c-181">Dus zowel Kestrel en WebListener `ICommunicationListener` implementaties standaardiseren op Hallo middleware geleverd door Hallo `UseServiceFabricIntegration` uitbreidingsmethode zodat clients alleen een service-eindpunt tooperform hoeft te zetten actie op 410 HTTP-antwoorden.</span><span class="sxs-lookup"><span data-stu-id="8026c-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on hello middleware provided by hello `UseServiceFabricIntegration` extension method so that clients only need tooperform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="8026c-182">WebListener in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8026c-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="8026c-183">WebListener kan worden gebruikt in een betrouwbare Service door het importeren van Hallo **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="8026c-183">WebListener can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="8026c-184">Dit pakket bevat `WebListenerCommunicationListener`, een implementatie van `ICommunicationListener`, waarmee u een ASP.NET Core WebHost binnen een betrouwbare Service toocreate WebListener gebruikt als Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="8026c-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using WebListener as hello web server.</span></span>

<span data-ttu-id="8026c-185">WebListener is gebouwd op Hallo [Windows HTTP-Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="8026c-185">WebListener is built on hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="8026c-186">Dit maakt gebruik van Hallo *http.sys* kernel-stuurprogramma die wordt gebruikt door IIS tooprocess HTTP-aanvragen en versturen ze tooprocesses waarop webtoepassingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8026c-186">This uses hello *http.sys* kernel driver used by IIS tooprocess HTTP requests and route them tooprocesses running web applications.</span></span> <span data-ttu-id="8026c-187">Hierdoor kunnen meerdere processen op Hallo dezelfde fysieke of virtuele machine toohost webtoepassingen op Hallo dezelfde poort, ondubbelzinnig gemaakt door een unieke URL-pad of de hostnaam.</span><span class="sxs-lookup"><span data-stu-id="8026c-187">This allows multiple processes on hello same physical or virtual machine toohost web applications on hello same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="8026c-188">Deze functies zijn handig in Service Fabric voor het hosten van meerdere websites in Hallo hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="8026c-188">These features are useful in Service Fabric for hosting multiple websites in hello same cluster.</span></span>

<span data-ttu-id="8026c-189">Hallo volgende diagram illustreert hoe WebListener Hallo gebruikt *http.sys* kernel-stuurprogramma in Windows voor het delen van poort:</span><span class="sxs-lookup"><span data-stu-id="8026c-189">hello following diagram illustrates how WebListener uses hello *http.sys* kernel driver on Windows for port sharing:</span></span>

![HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="8026c-191">WebListener in een stateless service</span><span class="sxs-lookup"><span data-stu-id="8026c-191">WebListener in a stateless service</span></span>
<span data-ttu-id="8026c-192">toouse `WebListener` in een stateless service overschrijven Hallo `CreateServiceInstanceListeners` methode en retourneren een `WebListenerCommunicationListener` exemplaar:</span><span class="sxs-lookup"><span data-stu-id="8026c-192">toouse `WebListener` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

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

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="8026c-193">WebListener in een stateful service</span><span class="sxs-lookup"><span data-stu-id="8026c-193">WebListener in a stateful service</span></span>

<span data-ttu-id="8026c-194">`WebListenerCommunicationListener`op dit moment niet is ontworpen voor gebruik in stateful services vanwege toocomplications met onderliggende hello *http.sys* poort functie voor het delen.</span><span class="sxs-lookup"><span data-stu-id="8026c-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due toocomplications with hello underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="8026c-195">Zie volgende sectie op dynamische poorttoewijzing met WebListener Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8026c-195">For more information, see hello following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="8026c-196">Voor stateful services is Kestrel Hallo aanbevolen webserver.</span><span class="sxs-lookup"><span data-stu-id="8026c-196">For stateful services, Kestrel is hello recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="8026c-197">Endpoint-configuratie</span><span class="sxs-lookup"><span data-stu-id="8026c-197">Endpoint configuration</span></span>

<span data-ttu-id="8026c-198">Een `Endpoint` configuratie is vereist voor webservers die gebruikmaken van Hallo Windows HTTP-Server API, met inbegrip van WebListener.</span><span class="sxs-lookup"><span data-stu-id="8026c-198">An `Endpoint` configuration is required for web servers that use hello Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="8026c-199">Webservers die gebruikmaken van Windows HTTP-Server API Hallo moeten eerst hun URL met reserveren *http.sys* (dit is normaal gesproken bewerkstelligd met Hallo [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span><span class="sxs-lookup"><span data-stu-id="8026c-199">Web servers that use hello Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="8026c-200">Deze actie is vereist voor verhoogde bevoegdheden die uw services standaard geen hebben.</span><span class="sxs-lookup"><span data-stu-id="8026c-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="8026c-201">Hallo 'http' of 'https'-opties voor Hallo `Protocol` eigenschap Hallo `Endpoint` configuratie in *ServiceManifest.xml* worden gebruikt specifiek tooinstruct Hallo Service Fabric-runtime tooregister een URL met *http.sys* namens jou Hallo met [ *sterk jokertekens* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL-voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="8026c-201">hello "http" or "https" options for hello `Protocol` property of hello `Endpoint` configuration in *ServiceManifest.xml* are used specifically tooinstruct hello Service Fabric runtime tooregister a URL with *http.sys* on your behalf using hello [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="8026c-202">Bijvoorbeeld: tooreserve `http://+:80` voor een service hello volgende configuratie moet worden gebruikt in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="8026c-202">For example, tooreserve `http://+:80` for a service, hello following configuration should be used in ServiceManifest.xml:</span></span>

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

<span data-ttu-id="8026c-203">En de naam van het eindpunt Hallo toohello moet worden doorgegeven `WebListenerCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="8026c-203">And hello endpoint name must be passed toohello `WebListenerCommunicationListener` constructor:</span></span>

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

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="8026c-204">WebListener gebruiken met een statische poort</span><span class="sxs-lookup"><span data-stu-id="8026c-204">Use WebListener with a static port</span></span>
<span data-ttu-id="8026c-205">toouse een statische poort met WebListener, geef Hallo poortnummer in Hallo `Endpoint` configuratie:</span><span class="sxs-lookup"><span data-stu-id="8026c-205">toouse a static port with WebListener, provide hello port number in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="8026c-206">WebListener gebruiken met een dynamische poort</span><span class="sxs-lookup"><span data-stu-id="8026c-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="8026c-207">een dynamisch toegewezen poort met WebListener, toouse weglaten Hallo `Port` eigenschap in Hallo `Endpoint` configuratie:</span><span class="sxs-lookup"><span data-stu-id="8026c-207">toouse a dynamically assigned port with WebListener, omit hello `Port` property in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="8026c-208">Merk op dat een dynamische poort is toegewezen door een `Endpoint` configuratie biedt slechts één poort *per hostproces*.</span><span class="sxs-lookup"><span data-stu-id="8026c-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="8026c-209">Hallo huidige Service Fabric hostingmodel meerdere service-exemplaren en/of replica's toobe gehost in Hallo kunt dezelfde verwerken, wat betekent dat elke dezelfde poort delen als toegewezen via Hallo Hallo `Endpoint` configuratie.</span><span class="sxs-lookup"><span data-stu-id="8026c-209">hello current Service Fabric hosting model allows multiple service instances and/or replicas toobe hosted in hello same process, meaning that each one will share hello same port when allocated through hello `Endpoint` configuration.</span></span> <span data-ttu-id="8026c-210">Meerdere exemplaren van WebListener kunnen delen een poort met onderliggende hello *http.sys* poort delen onderdeel, maar die niet wordt ondersteund door `WebListenerCommunicationListener` vanwege toohello problemen hierdoor voor clientaanvragen.</span><span class="sxs-lookup"><span data-stu-id="8026c-210">Multiple WebListener instances can share a port using hello underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due toohello complications it introduces for client requests.</span></span> <span data-ttu-id="8026c-211">Voor het gebruik van dynamische poort is Kestrel Hallo aanbevolen webserver.</span><span class="sxs-lookup"><span data-stu-id="8026c-211">For dynamic port usage, Kestrel is hello recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="8026c-212">Kestrel in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8026c-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="8026c-213">Kestrel kan worden gebruikt in een betrouwbare Service door het importeren van Hallo **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="8026c-213">Kestrel can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="8026c-214">Dit pakket bevat `KestrelCommunicationListener`, een implementatie van `ICommunicationListener`, waarmee u een ASP.NET Core WebHost binnen een betrouwbare Service toocreate Kestrel gebruikt als Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="8026c-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using Kestrel as hello web server.</span></span>

<span data-ttu-id="8026c-215">Kestrel is dat een platformoverschrijdende webserver voor ASP.NET Core op basis van libuv, een platformoverschrijdende asynchrone i/o-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="8026c-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="8026c-216">In tegenstelling tot WebListener, Kestrel gebruikt geen een gecentraliseerde eindpunt manager zoals *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="8026c-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="8026c-217">En in tegenstelling tot WebListener, Kestrel biedt geen ondersteuning voor poort delen tussen meerdere processen.</span><span class="sxs-lookup"><span data-stu-id="8026c-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="8026c-218">Elk exemplaar van Kestrel moet een unieke poort gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8026c-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="8026c-220">Kestrel in een stateless service</span><span class="sxs-lookup"><span data-stu-id="8026c-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="8026c-221">toouse `Kestrel` in een stateless service overschrijven Hallo `CreateServiceInstanceListeners` methode en retourneren een `KestrelCommunicationListener` exemplaar:</span><span class="sxs-lookup"><span data-stu-id="8026c-221">toouse `Kestrel` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="8026c-222">Kestrel in een stateful service</span><span class="sxs-lookup"><span data-stu-id="8026c-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="8026c-223">toouse `Kestrel` in een stateful service overschrijven Hallo `CreateServiceReplicaListeners` methode en retourneren een `KestrelCommunicationListener` exemplaar:</span><span class="sxs-lookup"><span data-stu-id="8026c-223">toouse `Kestrel` in a stateful service, override hello `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

<span data-ttu-id="8026c-224">In dit voorbeeld wordt een singleton-instantie van `IReliableStateManager` toohello WebHost afhankelijkheid injectie container is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8026c-224">In this example, a singleton instance of `IReliableStateManager` is provided toohello WebHost dependency injection container.</span></span> <span data-ttu-id="8026c-225">Dit is niet strikt noodzakelijk zijn, maar kunt u toouse `IReliableStateManager` en betrouwbare verzamelingen in uw MVC-controller-actiemethoden.</span><span class="sxs-lookup"><span data-stu-id="8026c-225">This is not strictly necessary, but it allows you toouse `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="8026c-226">Houd er rekening mee dat een `Endpoint` configuratienaam is **niet** te opgegeven`KestrelCommunicationListener` in een stateful service.</span><span class="sxs-lookup"><span data-stu-id="8026c-226">Note that an `Endpoint` configuration name is **not** provided too`KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="8026c-227">Dit wordt nader beschreven in de volgende sectie Hallo uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="8026c-227">This is explained in more detail in hello following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="8026c-228">Endpoint-configuratie</span><span class="sxs-lookup"><span data-stu-id="8026c-228">Endpoint configuration</span></span>
<span data-ttu-id="8026c-229">Een `Endpoint` configuratie is niet vereist toouse Kestrel.</span><span class="sxs-lookup"><span data-stu-id="8026c-229">An `Endpoint` configuration is not required toouse Kestrel.</span></span> 

<span data-ttu-id="8026c-230">Kestrel is een eenvoudige zelfstandige webserver; in tegenstelling tot WebListener (of HttpListener), hoeft deze niet een `Endpoint` configuratie in *ServiceManifest.xml* omdat er geen URL registratie eerdere toostarting nodig.</span><span class="sxs-lookup"><span data-stu-id="8026c-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior toostarting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="8026c-231">Kestrel gebruiken met een statische poort</span><span class="sxs-lookup"><span data-stu-id="8026c-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="8026c-232">Een statische poort kan worden geconfigureerd in Hallo `Endpoint` ServiceManifest.xml-configuratie voor gebruik met Kestrel.</span><span class="sxs-lookup"><span data-stu-id="8026c-232">A static port can be configured in hello `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="8026c-233">Hoewel dit niet strikt noodzakelijk is, heeft deze twee mogelijke voordelen:</span><span class="sxs-lookup"><span data-stu-id="8026c-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="8026c-234">Als Hallo poort niet in Hallo toepassingspoortbereik valt, wordt dit door de Service Fabric via Hallo OS firewall geopend.</span><span class="sxs-lookup"><span data-stu-id="8026c-234">If hello port does not fall in hello application port range, it is opened through hello OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="8026c-235">Hallo-URL opgegeven tooyou via `KestrelCommunicationListener` deze poort wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8026c-235">hello URL provided tooyou through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="8026c-236">Als een `Endpoint` is geconfigureerd, de naam moet worden doorgegeven in Hallo `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="8026c-236">If an `Endpoint` is configured, its name must be passed into hello `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="8026c-237">Als een `Endpoint` configuratie wordt niet gebruikt, laat u Hallo-naam in Hallo `KestrelCommunicationListener` constructor.</span><span class="sxs-lookup"><span data-stu-id="8026c-237">If an `Endpoint` configuration is not used, omit hello name in hello `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="8026c-238">In dit geval wordt een dynamische poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8026c-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="8026c-239">Zie de volgende sectie Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8026c-239">See hello next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="8026c-240">Kestrel gebruiken met een dynamische poort</span><span class="sxs-lookup"><span data-stu-id="8026c-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="8026c-241">Kestrel hello automatische poorttoewijzing van Hallo niet gebruiken `Endpoint` configuratie in ServiceManifest.xml, omdat automatische poorttoewijzing van een `Endpoint` configuratie wijst een unieke poort per *hosten proces* , en een proces voor één host meerdere exemplaren van Kestrel kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="8026c-241">Kestrel cannot use hello automatic port assignment from hello `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="8026c-242">Aangezien Kestrel biedt geen ondersteuning voor het delen van de poort, werkt dit niet zoals elk exemplaar Kestrel moet worden geopend op een unieke poort.</span><span class="sxs-lookup"><span data-stu-id="8026c-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="8026c-243">toewijzing van de dynamische poort toouse met Kestrel, weglaten gewoon Hallo `Endpoint` configuratie in ServiceManifest.xml volledig, en een eindpunt naam toohello niet doorgegeven `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="8026c-243">toouse dynamic port assignment with Kestrel, simply omit hello `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name toohello `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="8026c-244">In deze configuratie `KestrelCommunicationListener` automatisch een niet-gebruikte poort van Hallo toepassingspoortbereik selecteert.</span><span class="sxs-lookup"><span data-stu-id="8026c-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from hello application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="8026c-245">Scenario's en configuraties</span><span class="sxs-lookup"><span data-stu-id="8026c-245">Scenarios and configurations</span></span>
<span data-ttu-id="8026c-246">Deze sectie wordt beschreven Hallo volgen scenario's en biedt Hallo aanbevolen combinatie van de webserver, poortconfiguratie, opties voor Service Fabric-integratie en diverse instellingen tooachieve een service naar behoren werkt:</span><span class="sxs-lookup"><span data-stu-id="8026c-246">This section describes hello following scenarios and provides hello recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings tooachieve a properly functioning service:</span></span>
 - <span data-ttu-id="8026c-247">Extern blootgesteld ASP.NET Core staatloze service</span><span class="sxs-lookup"><span data-stu-id="8026c-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="8026c-248">Alleen intern-ASP.NET Core staatloze service</span><span class="sxs-lookup"><span data-stu-id="8026c-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="8026c-249">Alleen intern-ASP.NET Core stateful service</span><span class="sxs-lookup"><span data-stu-id="8026c-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="8026c-250">Een **extern blootgesteld** -service maakt dat toegang biedt tot een eindpunt dat bereikbaar is vanaf buiten Hallo-cluster, meestal via een load balancer.</span><span class="sxs-lookup"><span data-stu-id="8026c-250">An **externally exposed** service is one that exposes an endpoint reachable from outside hello cluster, usually through a load balancer.</span></span>

<span data-ttu-id="8026c-251">Een **alleen interne** -service is een waarvan eindpunt alleen bereikbaar is vanaf binnen Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="8026c-251">An **internal-only** service is one whose endpoint is only reachable from within hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8026c-252">Stateful service eindpunten in het algemeen niet moeten worden blootgesteld toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="8026c-252">Stateful service endpoints generally should not be exposed toohello Internet.</span></span> <span data-ttu-id="8026c-253">Clusters die zich achter de load balancers die zich niet bewust zijn van de oplossing van het Service Fabric-service, zoals hello Azure Load Balancer worden stateful services kan geen tooexpose omdat Hallo load balancer wordt niet kunnen toolocate en toohello verkeer routeren de replica van de juiste stateful service.</span><span class="sxs-lookup"><span data-stu-id="8026c-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as hello Azure Load Balancer, will be unable tooexpose stateful services because hello load balancer will not be able toolocate and route traffic toohello appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="8026c-254">Extern blootgesteld ASP.NET Core stateless services</span><span class="sxs-lookup"><span data-stu-id="8026c-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="8026c-255">WebListener wordt aanbevolen webserver voor de front-end-services die externe, internetgerichte HTTP-eindpunten op Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8026c-255">WebListener is hello recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="8026c-256">Dit biedt betere bescherming tegen aanvallen en functies die Kestrel niet, zoals Windows-verificatie en -poort delen bestaat ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="8026c-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="8026c-257">Kestrel wordt niet ondersteund als een edge (internetgerichte)-server op dit moment.</span><span class="sxs-lookup"><span data-stu-id="8026c-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="8026c-258">Een reverse proxy-server zoals IIS of Nginx moet worden gebruikt toohandle verkeer van Hallo openbare Internet.</span><span class="sxs-lookup"><span data-stu-id="8026c-258">A reverse proxy server such as IIS or Nginx must be used toohandle traffic from hello public Internet.</span></span>
 
<span data-ttu-id="8026c-259">Wanneer moet blootgestelde toohello Internet, een stateless service een bekende en stabiele eindpunt dat bereikbaar is via een load balancer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8026c-259">When exposed toohello Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="8026c-260">Dit is Hallo-URL die u biedt toousers van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8026c-260">This is hello URL you will provide toousers of your application.</span></span> <span data-ttu-id="8026c-261">Hallo na configuratie wordt aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="8026c-261">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="8026c-262">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="8026c-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8026c-263">Webserver</span><span class="sxs-lookup"><span data-stu-id="8026c-263">Web server</span></span> | <span data-ttu-id="8026c-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="8026c-264">WebListener</span></span> | <span data-ttu-id="8026c-265">Als Hallo-service alleen weergegeven tooa vertrouwd netwerk, een intranet wordt kan Kestrel worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8026c-265">If hello service is only exposed tooa trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="8026c-266">Anders is WebListener Hallo voorkeurs-optie.</span><span class="sxs-lookup"><span data-stu-id="8026c-266">Otherwise, WebListener is hello preferred option.</span></span> |
| <span data-ttu-id="8026c-267">Poortconfiguratie</span><span class="sxs-lookup"><span data-stu-id="8026c-267">Port configuration</span></span> | <span data-ttu-id="8026c-268">Statische</span><span class="sxs-lookup"><span data-stu-id="8026c-268">static</span></span> | <span data-ttu-id="8026c-269">Een bekende statische poort moet worden geconfigureerd in Hallo `Endpoints` configuratie van ServiceManifest.xml, zoals 80 voor HTTP en 443 voor HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8026c-269">A well-known static port should be configured in hello `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="8026c-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="8026c-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="8026c-271">Geen</span><span class="sxs-lookup"><span data-stu-id="8026c-271">None</span></span> | <span data-ttu-id="8026c-272">Hallo `ServiceFabricIntegrationOptions.None` moet worden gebruikt bij het configureren van Service Fabric-integratie middleware zodat Hallo-service niet toovalidate binnenkomende aanvragen voor een unieke id probeert.</span><span class="sxs-lookup"><span data-stu-id="8026c-272">hello `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that hello service does not attempt toovalidate incoming requests for a unique identifier.</span></span> <span data-ttu-id="8026c-273">Externe gebruikers van uw toepassing weet niet Hallo unieke identificatiegegevens door Hallo middleware gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8026c-273">External users of your application will not know hello unique identifying information used by hello middleware.</span></span> |
| <span data-ttu-id="8026c-274">Aantal exemplaren</span><span class="sxs-lookup"><span data-stu-id="8026c-274">Instance Count</span></span> | <span data-ttu-id="8026c-275">-1</span><span class="sxs-lookup"><span data-stu-id="8026c-275">-1</span></span> | <span data-ttu-id="8026c-276">In een typische gebruiksvoorbeelden Hallo-exemplaren instellen te moet worden ingesteld-"1" zodat er een exemplaar is beschikbaar op alle knooppunten die verkeer van een load balancer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="8026c-276">In typical use cases, hello instance count setting should be set too"-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="8026c-277">Als meerdere extern blootgestelde services dezelfde knooppunten set hello delen, kan een unieke maar stabiele URL-pad moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8026c-277">If multiple externally exposed services share hello same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="8026c-278">Dit kan worden bereikt door het Hallo-URL opgegeven tijdens het configureren van IWebHost wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8026c-278">This can be accomplished by modifying hello URL provided when configuring IWebHost.</span></span> <span data-ttu-id="8026c-279">Houd er rekening mee dat dit tooWebListener alleen van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="8026c-279">Note this applies tooWebListener only.</span></span>

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

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="8026c-280">Alleen intern staatloze ASP.NET Core-service</span><span class="sxs-lookup"><span data-stu-id="8026c-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="8026c-281">Stateless services die alleen worden aangeroepen vanuit binnen Hallo cluster unieke URL's moeten gebruiken en dynamisch toegewezen poorten tooensure samenwerking tussen meerdere services.</span><span class="sxs-lookup"><span data-stu-id="8026c-281">Stateless services that are only called from within hello cluster should use unique URLs and dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="8026c-282">Hallo na configuratie wordt aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="8026c-282">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="8026c-283">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="8026c-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8026c-284">Webserver</span><span class="sxs-lookup"><span data-stu-id="8026c-284">Web server</span></span> | <span data-ttu-id="8026c-285">kestrel</span><span class="sxs-lookup"><span data-stu-id="8026c-285">Kestrel</span></span> | <span data-ttu-id="8026c-286">Hoewel WebListener kan worden gebruikt voor interne stateless services, is het Kestrel Hallo aanbevolen server tooallow meerdere service-exemplaren tooshare een host.</span><span class="sxs-lookup"><span data-stu-id="8026c-286">Although WebListener may be used for internal stateless services, Kestrel is hello recommended server tooallow multiple service instances tooshare a host.</span></span>  |
| <span data-ttu-id="8026c-287">Poortconfiguratie</span><span class="sxs-lookup"><span data-stu-id="8026c-287">Port configuration</span></span> | <span data-ttu-id="8026c-288">dynamisch toegewezen</span><span class="sxs-lookup"><span data-stu-id="8026c-288">dynamically assigned</span></span> | <span data-ttu-id="8026c-289">Meerdere replica's van een stateful service kunnen een hostproces of hostbesturingssysteem delen en moeten dus unieke poorten.</span><span class="sxs-lookup"><span data-stu-id="8026c-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="8026c-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="8026c-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="8026c-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="8026c-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="8026c-292">Bij toewijzing van de dynamische poort is deze instelling voorkomt dat Hallo verward identiteit probleem die eerder zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="8026c-292">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="8026c-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="8026c-293">InstanceCount</span></span> | <span data-ttu-id="8026c-294">alle</span><span class="sxs-lookup"><span data-stu-id="8026c-294">any</span></span> | <span data-ttu-id="8026c-295">Hallo-exemplaren instellen kan tooany waarde nodig toooperate Hallo service worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8026c-295">hello instance count setting can be set tooany value necessary toooperate hello service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="8026c-296">Alleen intern stateful ASP.NET Core-service</span><span class="sxs-lookup"><span data-stu-id="8026c-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="8026c-297">Stateful services die alleen worden aangeroepen vanuit binnen Hallo cluster moeten dynamisch toegewezen poorten tooensure samenwerking tussen meerdere services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8026c-297">Stateful services that are only called from within hello cluster should use dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="8026c-298">Hallo na configuratie wordt aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="8026c-298">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="8026c-299">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="8026c-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8026c-300">Webserver</span><span class="sxs-lookup"><span data-stu-id="8026c-300">Web server</span></span> | <span data-ttu-id="8026c-301">kestrel</span><span class="sxs-lookup"><span data-stu-id="8026c-301">Kestrel</span></span> | <span data-ttu-id="8026c-302">Hallo `WebListenerCommunicationListener` is niet ontworpen voor gebruik door stateful services waarin de replica's een hostproces delen.</span><span class="sxs-lookup"><span data-stu-id="8026c-302">hello `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="8026c-303">Poortconfiguratie</span><span class="sxs-lookup"><span data-stu-id="8026c-303">Port configuration</span></span> | <span data-ttu-id="8026c-304">dynamisch toegewezen</span><span class="sxs-lookup"><span data-stu-id="8026c-304">dynamically assigned</span></span> | <span data-ttu-id="8026c-305">Meerdere replica's van een stateful service kunnen een hostproces of hostbesturingssysteem delen en moeten dus unieke poorten.</span><span class="sxs-lookup"><span data-stu-id="8026c-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="8026c-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="8026c-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="8026c-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="8026c-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="8026c-308">Bij toewijzing van de dynamische poort is deze instelling voorkomt dat Hallo verward identiteit probleem die eerder zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="8026c-308">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8026c-309">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8026c-309">Next steps</span></span>
[<span data-ttu-id="8026c-310">Fouten opsporen in uw Service Fabric-toepassing met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8026c-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
