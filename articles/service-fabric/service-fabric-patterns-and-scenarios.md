---
title: Service Fabric aaaAzure scenario's en patronen | Microsoft Docs
description: Informatie over aanbevolen procedures en beproefde, herbruikbare patronen toodesign, ontwikkelen en beheren van uw microservices op Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="2521e-103">Service Fabric-patronen en scenario 's</span><span class="sxs-lookup"><span data-stu-id="2521e-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="2521e-104">Als u op zoek bent bij het bouwen van grootschalige microservices met behulp van Azure Service Fabric leren van Hallo-experts die ontwikkeld en gebouwd dit platform als een service (PaaS).</span><span class="sxs-lookup"><span data-stu-id="2521e-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="2521e-105">Aan de slag met de juiste architectuur en vervolgens de informatie over hoe toooptimize resources voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2521e-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="2521e-106">Hallo [Service Fabric Patterns and practice](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) loop beantwoordt Hallo vragen vaakst door de werkelijke klanten over Service Fabric-scenario's en modules.</span><span class="sxs-lookup"><span data-stu-id="2521e-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="2521e-107">Ontdek hoe toodesign, ontwikkelen en beheren van uw microservices op Service-infrastructuur met behulp van aanbevolen procedures en patronen beproefde, herbruikbare.</span><span class="sxs-lookup"><span data-stu-id="2521e-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="2521e-108">Een overzicht van Service Fabric en vervolgens meteen diep in de onderwerpen die betrekking hebben op cluster optimalisatie en beveiliging, migreren van oudere apps IoT op grote schaal, game motoren en meer te hosten.</span><span class="sxs-lookup"><span data-stu-id="2521e-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="2521e-109">Bekijk continue leveringsmethode voor verschillende werkbelastingen en zelfs Hallo-details op Linux-ondersteuning en containers ophalen.</span><span class="sxs-lookup"><span data-stu-id="2521e-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="2521e-110">Inleiding</span><span class="sxs-lookup"><span data-stu-id="2521e-110">Introduction</span></span>
<span data-ttu-id="2521e-111">Bekijk de aanbevolen procedures en informatie over het kiezen van platform als een service (PaaS) via infrastructuur als een service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="2521e-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="2521e-112">Hallo-details ophalen van volgende principes van de toepassing beproefde ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="2521e-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="2521e-113">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-113">Video</span></span></th><th><span data-ttu-id="2521e-114">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="2521e-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Inleiding tooService Fabric</a></span><span class="sxs-lookup"><span data-stu-id="2521e-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="2521e-116">Planning van de cluster en beheer</span><span class="sxs-lookup"><span data-stu-id="2521e-116">Cluster planning and management</span></span>
<span data-ttu-id="2521e-117">Meer informatie over het plannen van capaciteit, cluster-optimalisatie en clusterbeveiliging in deze kijken Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2521e-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="2521e-118">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-118">Video</span></span></th><th><span data-ttu-id="2521e-119">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="2521e-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Planning van de cluster en beheer</a></span><span class="sxs-lookup"><span data-stu-id="2521e-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="2521e-121">Grootschalige web</span><span class="sxs-lookup"><span data-stu-id="2521e-121">Hyper-scale web</span></span>
<span data-ttu-id="2521e-122">De basisbegrippen op hyperschaal web, met inbegrip van de beschikbaarheid en betrouwbaarheid, hyperschaal en statusbeheer.</span><span class="sxs-lookup"><span data-stu-id="2521e-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="2521e-123">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-123">Video</span></span></th><th><span data-ttu-id="2521e-124">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="2521e-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Grootschalige web</a></span><span class="sxs-lookup"><span data-stu-id="2521e-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="2521e-126">IoT</span><span class="sxs-lookup"><span data-stu-id="2521e-126">IoT</span></span>
<span data-ttu-id="2521e-127">Verken Hallo Internet der dingen (IoT) in de context Hallo van Azure Service Fabric, inclusief hello Azure IoT pipeline, multi-tenancymodus en IoT op grote schaal.</span><span class="sxs-lookup"><span data-stu-id="2521e-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="2521e-128">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-128">Video</span></span></th><th><span data-ttu-id="2521e-129">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="2521e-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="2521e-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="2521e-131">Gaming</span><span class="sxs-lookup"><span data-stu-id="2521e-131">Gaming</span></span>
<span data-ttu-id="2521e-132">Schakel gebaseerde games, interactieve games en die als host fungeert voor bestaande game engines kijken.</span><span class="sxs-lookup"><span data-stu-id="2521e-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="2521e-133">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-133">Video</span></span></th><th><span data-ttu-id="2521e-134">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="2521e-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Games</a></span><span class="sxs-lookup"><span data-stu-id="2521e-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="2521e-136">Onafgebroken levering</span><span class="sxs-lookup"><span data-stu-id="2521e-136">Continuous delivery</span></span>
<span data-ttu-id="2521e-137">Concepten, met inbegrip van continue integratie/continue levering met Visual Studio Team Services, werkstroom build, pakket/publiceren, meerdere omgeving in te stellen en service pakketshare verkennen.</span><span class="sxs-lookup"><span data-stu-id="2521e-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="2521e-138">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-138">Video</span></span></th><th><span data-ttu-id="2521e-139">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="2521e-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continue levering</a></span><span class="sxs-lookup"><span data-stu-id="2521e-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="2521e-141">Migratie</span><span class="sxs-lookup"><span data-stu-id="2521e-141">Migration</span></span>
<span data-ttu-id="2521e-142">Meer informatie over het migreren van een cloudservice bovendien toomigration van verouderde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2521e-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="2521e-143">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-143">Video</span></span></th><th><span data-ttu-id="2521e-144">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="2521e-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migratie</a></span><span class="sxs-lookup"><span data-stu-id="2521e-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="2521e-146">Containers en Linux-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="2521e-146">Containers and Linux support</span></span>
<span data-ttu-id="2521e-147">Hallo antwoord toohello vraag ophalen ' Waarom containers? '</span><span class="sxs-lookup"><span data-stu-id="2521e-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="2521e-148">Meer informatie over het Hallo-preview voor containers voor Windows, Linux-ondersteuning en Linux-containers orchestration.</span><span class="sxs-lookup"><span data-stu-id="2521e-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="2521e-149">Ontdek hoe u kunt bovendien toomigrate .NET Core apps tooLinux.</span><span class="sxs-lookup"><span data-stu-id="2521e-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="2521e-150">Video</span><span class="sxs-lookup"><span data-stu-id="2521e-150">Video</span></span></th><th><span data-ttu-id="2521e-151">PowerPoint dek</span><span class="sxs-lookup"><span data-stu-id="2521e-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="2521e-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers en Linux-ondersteuning</a></span><span class="sxs-lookup"><span data-stu-id="2521e-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="2521e-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2521e-153">Next steps</span></span>
<span data-ttu-id="2521e-154">Nu dat u hebt geleerd over scenario's en Service Fabric-patronen, lees meer informatie over hoe te[maken en beheren van clusters](service-fabric-deploy-anywhere.md), [Cloudservices apps tooService Fabric migreren](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [instellen continue levering](service-fabric-set-up-continuous-integration.md), en [containers implementeren](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2521e-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
