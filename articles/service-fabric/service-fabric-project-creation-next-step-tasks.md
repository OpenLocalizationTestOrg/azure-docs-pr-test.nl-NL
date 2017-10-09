---
title: aaaService Fabric-project maken de volgende stappen | Microsoft Docs
description: Dit artikel bevat koppelingen tooa verzameling ontwikkeling kerntaken voor Service Fabric
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="b1ea0-103">Uw Service Fabric-toepassing en de volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1ea0-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="b1ea0-104">Uw Azure Service Fabric-toepassing is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="b1ea0-105">Hallo samenstelling van uw project en een aantal mogelijke volgende stappen wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="b1ea0-106">Uw toepassing</span><span class="sxs-lookup"><span data-stu-id="b1ea0-106">Your application</span></span>
<span data-ttu-id="b1ea0-107">Elke nieuwe toepassing bevat een toepassingsproject.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-107">Every new application includes an application project.</span></span> <span data-ttu-id="b1ea0-108">Er zijn een of twee extra projecten, afhankelijk van het Hallo-type van de service gekozen.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="b1ea0-109">Hallo-toepassingsproject</span><span class="sxs-lookup"><span data-stu-id="b1ea0-109">hello application project</span></span>
<span data-ttu-id="b1ea0-110">Hallo-toepassingsproject bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="b1ea0-110">hello application project consists of:</span></span>

* <span data-ttu-id="b1ea0-111">Een aantal verwijzingen toohello services die gezamenlijk uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="b1ea0-112">Drie publiceren profielen (1-knooppunt lokale, 5-knooppunt lokale en Cloud) waarmee u toomaintain voorkeuren kunt voor het werken met verschillende omgevingen--zoals voorkeuren gerelateerde tooa clustereindpunt en Hiermee wordt aangegeven of tooperform implementaties upgrade standaard.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="b1ea0-113">Drie parameter voor toepassingsbestanden (zelfde als hierboven) waarmee u toomaintain toepassing omgeving-specifieke configuraties, zoals Hallo aantal partities toocreate voor een service kunt.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="b1ea0-114">Het script voor een implementatie waarmee u toodeploy uw toepassing vanaf de opdrachtregel Hallo of als onderdeel van een geautomatiseerde continue integratie en implementatie-pijplijn kunt.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="b1ea0-115">Hallo toepassingsmanifest, waarin wordt beschreven Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="b1ea0-116">U vindt Hallo manifest onder Hallo ApplicationPackageRoot map.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="b1ea0-117">Staatloze service</span><span class="sxs-lookup"><span data-stu-id="b1ea0-117">Stateless service</span></span>
<span data-ttu-id="b1ea0-118">Wanneer u een nieuwe staatloze service toevoegt, Visual Studio wordt toegevoegd een oplossing voor service-project tooyour met een type dat is afgeleid van `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="b1ea0-119">Hallo-service wordt een lokale variabele in een teller verhoogd.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="b1ea0-120">Stateful service</span><span class="sxs-lookup"><span data-stu-id="b1ea0-120">Stateful service</span></span>
<span data-ttu-id="b1ea0-121">Wanneer u een nieuwe stateful service toevoegt, Visual Studio wordt toegevoegd een oplossing voor service-project tooyour met een type dat is afgeleid van `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="b1ea0-122">Hallo service verhoogt een item in de `RunAsync` methode en winkels Hallo resulteren in een `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="b1ea0-123">Actor-service</span><span class="sxs-lookup"><span data-stu-id="b1ea0-123">Actor service</span></span>
<span data-ttu-id="b1ea0-124">Wanneer u een nieuwe betrouwbare actor toevoegt, Visual Studio twee projecten tooyour oplossing voegt: een actor-project en een interface-project.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="b1ea0-125">Hallo actor project biedt methoden voor het instellen en betrouwbaar binnen Hallo actorstatus ophalen van Hallo-waarde van een prestatiemeteritem dat wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="b1ea0-126">Hallo project interface biedt een interface die andere services tooinvoke Hallo actor kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="b1ea0-127">Staatloze Web-API</span><span class="sxs-lookup"><span data-stu-id="b1ea0-127">Stateless Web API</span></span>
<span data-ttu-id="b1ea0-128">Hallo staatloze Web API-project biedt een eenvoudige webservice waarmee u tooopen uw toepassing tooexternal-clients kunt.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="b1ea0-129">Zie voor meer informatie over de structuur van Hallo project [Service Fabric-Web-API-services met OWIN zelf hosting](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="b1ea0-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="b1ea0-130">ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="b1ea0-130">ASP.NET core</span></span>
<span data-ttu-id="b1ea0-131">Hallo Service Fabric SDK bevat Hallo dezelfde set van ASP.NET Core sjablonen die beschikbaar zijn voor zelfstandige ASP.NET Core projecten: leeg is, [Web API][aspnet-webapi], en [webtoepassing][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="b1ea0-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="b1ea0-132">Gast uitvoerbare bestanden en de Gast-containers</span><span class="sxs-lookup"><span data-stu-id="b1ea0-132">Guest executables and guest containers</span></span>

<span data-ttu-id="b1ea0-133">Een Service Fabric 'gast' is een service die niet is gebouwd met programmeermodellen Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="b1ea0-134">Kunt u een pakket Hallo binaire bestanden voor een gast ofwel [rechtstreeks in het toepassingspakket Hallo](service-fabric-deploy-existing-app.md) of [via een installatiekopie van een container](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="b1ea0-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="b1ea0-135">In beide gevallen Visual Studio maakt Hallo nodig artefacten in Hallo **ApplicationPackageRoot** map van het toepassingsproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="b1ea0-136">Visual Studio wordt een nieuw serviceproject niet maken omdat Hallo code al elders bestaat.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="b1ea0-137">Als u uw gast naast Hallo Service Fabric-toepassingsproject projecten toomanage wilt, kunt u deze toevoegen toohello dezelfde Visual Studio-oplossing.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1ea0-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1ea0-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="b1ea0-139">Een Azure-cluster maken</span><span class="sxs-lookup"><span data-stu-id="b1ea0-139">Create an Azure cluster</span></span>
<span data-ttu-id="b1ea0-140">Hallo Service Fabric SDK bevat een lokaal cluster voor ontwikkeling en testen.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="b1ea0-141">Zie voor een cluster in Azure, toocreate [instellen van een Service Fabric-cluster van hello Azure-portal][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="b1ea0-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="b1ea0-142">Uw toepassing tooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="b1ea0-142">Publish your application tooAzure</span></span>
<span data-ttu-id="b1ea0-143">U kunt uw toepassing rechtstreeks vanuit Visual Studio tooan Azure cluster publiceren.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="b1ea0-144">toolearn Zie [publiceren van uw toepassing tooAzure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="b1ea0-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="b1ea0-145">Uw cluster Service Fabric Explorer toovisualize gebruiken</span><span class="sxs-lookup"><span data-stu-id="b1ea0-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="b1ea0-146">Service Fabric Explorer biedt een eenvoudige manier toovisualize uw cluster, inclusief geïmplementeerde toepassingen en de fysieke indeling.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="b1ea0-147">toolearn meer, Zie [uw cluster visualiseren met behulp van Service Fabric Explorer][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="b1ea0-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="b1ea0-148">Versie en werk uw services</span><span class="sxs-lookup"><span data-stu-id="b1ea0-148">Version and upgrade your services</span></span>
<span data-ttu-id="b1ea0-149">Service Fabric kunnen onafhankelijke versioning en upgraden van onafhankelijke services in een toepassing.</span><span class="sxs-lookup"><span data-stu-id="b1ea0-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="b1ea0-150">toolearn meer, Zie [versiebeheer en upgraden van uw services][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="b1ea0-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="b1ea0-151">Continue integratie met Visual Studio Team Services configureren</span><span class="sxs-lookup"><span data-stu-id="b1ea0-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="b1ea0-152">toolearn hoe u een continue integratie-proces kan instellen voor uw Service Fabric-toepassing raadpleegt [continue integratie met Visual Studio Team Services configureren][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="b1ea0-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
