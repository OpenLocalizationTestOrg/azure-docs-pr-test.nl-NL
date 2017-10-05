---
title: Azure-container register opslagplaatsen | Microsoft Docs
description: "Het gebruik van Azure Container register-opslagplaatsen voor Docker-installatiekopieën"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: dd4feff057269ed7106990bb63eed7fcffa2dbec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="405e2-103">Register-opslagplaatsen voor Azure-container</span><span class="sxs-lookup"><span data-stu-id="405e2-103">Azure container registry repositories</span></span>

<span data-ttu-id="405e2-104">Azure Container registers zijn compatibel met een groot aantal services en orchestrators.</span><span class="sxs-lookup"><span data-stu-id="405e2-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="405e2-105">We zijn begonnen met de Docker-header-veld in het Docker.config-bestand voor het bijhouden van de bron-services en -agenten waaruit ACR wordt gebruikt te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="405e2-105">To make it easier to track the source services and agents from which ACR is used, we have started using the Docker header field in the Docker.config file.</span></span>



## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="405e2-106">Opslagplaatsen weergeven in de Portal</span><span class="sxs-lookup"><span data-stu-id="405e2-106">Viewing repositories in the Portal</span></span>

<span data-ttu-id="405e2-107">De headers ACR volgt u de indeling:</span><span class="sxs-lookup"><span data-stu-id="405e2-107">The ACR headers follow the format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="405e2-108">Cloud: Azure, Azure-Stack of andere government of land-specifieke Azure-clouds.</span><span class="sxs-lookup"><span data-stu-id="405e2-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="405e2-109">Hoewel Azure Stack en government clouds worden momenteel niet ondersteund, schakelt u deze parameter toekomstige ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="405e2-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="405e2-110">Service: de naam van de service.</span><span class="sxs-lookup"><span data-stu-id="405e2-110">Service: name of the service.</span></span>
* <span data-ttu-id="405e2-111">Optionalservicename: een optionele parameter voor services met subservices of om op te geven van een SKU (ex: web-apps overeenkomen met de Azure/app-service/web-apps).</span><span class="sxs-lookup"><span data-stu-id="405e2-111">Optionalservicename: optional parameter for services with subservices, or to specify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="405e2-112">Partnerservices en orchestrators aangemoedigd specifieke headerwaarden gebruiken om u te helpen met onze telemetrie.</span><span class="sxs-lookup"><span data-stu-id="405e2-112">Partner services and orchestrators are encouraged to use specific header values to help with our telemetry.</span></span> <span data-ttu-id="405e2-113">Gebruikers kunnen ook de waarde die is doorgegeven aan de header desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="405e2-113">Users can also modify the value passed to the header if they so desire.</span></span>

<span data-ttu-id="405e2-114">De waarden willen we ACR-partners gebruiken om te vullen van het veld 'X-Meta-bron-Client' worden hieronder:</span><span class="sxs-lookup"><span data-stu-id="405e2-114">The values we want ACR partners to use to populate the "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="405e2-115">Naam service</span><span class="sxs-lookup"><span data-stu-id="405e2-115">Service Name</span></span>              | <span data-ttu-id="405e2-116">Koptekst</span><span class="sxs-lookup"><span data-stu-id="405e2-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="405e2-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="405e2-117">Azure Container Service</span></span>   | <span data-ttu-id="405e2-118">Azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="405e2-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="405e2-119">App Service - Web-Apps</span><span class="sxs-lookup"><span data-stu-id="405e2-119">App Service - Web Apps</span></span>    | <span data-ttu-id="405e2-120">Azure /-/ web-apps van app service</span><span class="sxs-lookup"><span data-stu-id="405e2-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="405e2-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="405e2-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="405e2-122">Azure /-/ logic-apps van app service</span><span class="sxs-lookup"><span data-stu-id="405e2-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="405e2-123">Batch</span><span class="sxs-lookup"><span data-stu-id="405e2-123">Batch</span></span>                     | <span data-ttu-id="405e2-124">compute-Azure/batch</span><span class="sxs-lookup"><span data-stu-id="405e2-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="405e2-125">Cloud-Console</span><span class="sxs-lookup"><span data-stu-id="405e2-125">Cloud Console</span></span>             | <span data-ttu-id="405e2-126">Azure-cloud-console</span><span class="sxs-lookup"><span data-stu-id="405e2-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="405e2-127">Functies</span><span class="sxs-lookup"><span data-stu-id="405e2-127">Functions</span></span>                 | <span data-ttu-id="405e2-128">compute-Azure-functies</span><span class="sxs-lookup"><span data-stu-id="405e2-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="405e2-129">Internet der dingen - Hub</span><span class="sxs-lookup"><span data-stu-id="405e2-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="405e2-130">iot-Azure-hub</span><span class="sxs-lookup"><span data-stu-id="405e2-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="405e2-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="405e2-131">HDInsight</span></span>                 | <span data-ttu-id="405e2-132">data-Azure/hdinsight</span><span class="sxs-lookup"><span data-stu-id="405e2-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="405e2-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="405e2-133">Jenkins</span></span>                   | <span data-ttu-id="405e2-134">Azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="405e2-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="405e2-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="405e2-135">Machine Learning</span></span>          | <span data-ttu-id="405e2-136">Azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="405e2-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="405e2-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="405e2-137">Service Fabric</span></span>            | <span data-ttu-id="405e2-138">Azure/compute/service-infrastructuur</span><span class="sxs-lookup"><span data-stu-id="405e2-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="405e2-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="405e2-139">VSTS</span></span>                      | <span data-ttu-id="405e2-140">Azure/vsts</span><span class="sxs-lookup"><span data-stu-id="405e2-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="405e2-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="405e2-141">Next steps</span></span>
[<span data-ttu-id="405e2-142">Meer informatie over registers en de ondersteunde services orchestrators</span><span class="sxs-lookup"><span data-stu-id="405e2-142">Learn more about registries and the supported services and orchestrators</span></span>](container-registry-intro.md)
