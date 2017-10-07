---
title: aaaAzure container register opslagplaatsen | Microsoft Docs
description: "Hoe toouse Azure Container register opslagplaatsen voor Docker-installatiekopieën"
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
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="14d52-103">Register-opslagplaatsen voor Azure-container</span><span class="sxs-lookup"><span data-stu-id="14d52-103">Azure container registry repositories</span></span>

<span data-ttu-id="14d52-104">Azure Container registers zijn compatibel met een groot aantal services en orchestrators.</span><span class="sxs-lookup"><span data-stu-id="14d52-104">Azure Container Registries are compatible with a multitude of services and orchestrators.</span></span> <span data-ttu-id="14d52-105">toomake deze eenvoudiger tootrack Hallo bron services en agents waaruit ACR wordt gebruikt, we hebt gestart met behulp van Docker-kopveld Hallo in Hallo Docker.config bestand.</span><span class="sxs-lookup"><span data-stu-id="14d52-105">toomake it easier tootrack hello source services and agents from which ACR is used, we have started using hello Docker header field in hello Docker.config file.</span></span>



## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="14d52-106">Opslagplaatsen in Hallo Portal weergeven</span><span class="sxs-lookup"><span data-stu-id="14d52-106">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="14d52-107">Hallo ACR headers volgt Hallo indeling:</span><span class="sxs-lookup"><span data-stu-id="14d52-107">hello ACR headers follow hello format:</span></span>
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* <span data-ttu-id="14d52-108">Cloud: Azure, Azure-Stack of andere government of land-specifieke Azure-clouds.</span><span class="sxs-lookup"><span data-stu-id="14d52-108">Cloud: Azure, Azure Stack, or other government or country-specific Azure clouds.</span></span> <span data-ttu-id="14d52-109">Hoewel Azure Stack en government clouds worden momenteel niet ondersteund, schakelt u deze parameter toekomstige ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="14d52-109">Although Azure Stack and government clouds are not currently supported, this parameter enables future support.</span></span>
* <span data-ttu-id="14d52-110">Service: de naam van van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="14d52-110">Service: name of hello service.</span></span>
* <span data-ttu-id="14d52-111">Optionalservicename: een optionele parameter voor services met subservices of toospecify een SKU (ex: web-apps overeenkomen met de Azure/app-service/web-apps).</span><span class="sxs-lookup"><span data-stu-id="14d52-111">Optionalservicename: optional parameter for services with subservices, or toospecify a SKU (ex: web apps correspond with Azure/app-service/web-apps).</span></span>

<span data-ttu-id="14d52-112">Partnerservices en orchestrators zijn aangemoedigd toouse specifieke koptekst waarden toohelp met onze telemetrie.</span><span class="sxs-lookup"><span data-stu-id="14d52-112">Partner services and orchestrators are encouraged toouse specific header values toohelp with our telemetry.</span></span> <span data-ttu-id="14d52-113">Gebruikers kunnen ook Hallo-waarde doorgegeven toohello header desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="14d52-113">Users can also modify hello value passed toohello header if they so desire.</span></span>

<span data-ttu-id="14d52-114">we willen ACR partners toouse toopopulate Hallo 'X-Meta-bron-Client' veld Hallo-waarden zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="14d52-114">hello values we want ACR partners toouse toopopulate hello "X-Meta-Source-Client" field are below:</span></span>

| <span data-ttu-id="14d52-115">Naam service</span><span class="sxs-lookup"><span data-stu-id="14d52-115">Service Name</span></span>              | <span data-ttu-id="14d52-116">Koptekst</span><span class="sxs-lookup"><span data-stu-id="14d52-116">Header</span></span>                                |
| ------------------------- | ------------------------------------- |
| <span data-ttu-id="14d52-117">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="14d52-117">Azure Container Service</span></span>   | <span data-ttu-id="14d52-118">Azure/compute/azure-container-service</span><span class="sxs-lookup"><span data-stu-id="14d52-118">azure/compute/azure-container-service</span></span> |
| <span data-ttu-id="14d52-119">App Service - Web-Apps</span><span class="sxs-lookup"><span data-stu-id="14d52-119">App Service - Web Apps</span></span>    | <span data-ttu-id="14d52-120">Azure /-/ web-apps van app service</span><span class="sxs-lookup"><span data-stu-id="14d52-120">azure/app-service/web-apps</span></span>            |
| <span data-ttu-id="14d52-121">App Service - Logic Apps</span><span class="sxs-lookup"><span data-stu-id="14d52-121">App Service - Logic Apps</span></span>  | <span data-ttu-id="14d52-122">Azure /-/ logic-apps van app service</span><span class="sxs-lookup"><span data-stu-id="14d52-122">azure/app-service/logic-apps</span></span>          |
| <span data-ttu-id="14d52-123">Batch</span><span class="sxs-lookup"><span data-stu-id="14d52-123">Batch</span></span>                     | <span data-ttu-id="14d52-124">compute-Azure/batch</span><span class="sxs-lookup"><span data-stu-id="14d52-124">azure/compute/batch</span></span>                   |
| <span data-ttu-id="14d52-125">Cloud-Console</span><span class="sxs-lookup"><span data-stu-id="14d52-125">Cloud Console</span></span>             | <span data-ttu-id="14d52-126">Azure-cloud-console</span><span class="sxs-lookup"><span data-stu-id="14d52-126">azure/cloud-console</span></span>                   |
| <span data-ttu-id="14d52-127">Functies</span><span class="sxs-lookup"><span data-stu-id="14d52-127">Functions</span></span>                 | <span data-ttu-id="14d52-128">compute-Azure-functies</span><span class="sxs-lookup"><span data-stu-id="14d52-128">azure/compute/functions</span></span>               |
| <span data-ttu-id="14d52-129">Internet der dingen - Hub</span><span class="sxs-lookup"><span data-stu-id="14d52-129">Internet of Things - Hub</span></span>  | <span data-ttu-id="14d52-130">iot-Azure-hub</span><span class="sxs-lookup"><span data-stu-id="14d52-130">azure/iot/hub</span></span>                         |
| <span data-ttu-id="14d52-131">HDInsight</span><span class="sxs-lookup"><span data-stu-id="14d52-131">HDInsight</span></span>                 | <span data-ttu-id="14d52-132">data-Azure/hdinsight</span><span class="sxs-lookup"><span data-stu-id="14d52-132">azure/data/hdinsight</span></span>                  |
| <span data-ttu-id="14d52-133">Jenkins</span><span class="sxs-lookup"><span data-stu-id="14d52-133">Jenkins</span></span>                   | <span data-ttu-id="14d52-134">Azure/jenkins</span><span class="sxs-lookup"><span data-stu-id="14d52-134">azure/jenkins</span></span>                         |
| <span data-ttu-id="14d52-135">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="14d52-135">Machine Learning</span></span>          | <span data-ttu-id="14d52-136">Azure/data/machile-learning</span><span class="sxs-lookup"><span data-stu-id="14d52-136">azure/data/machile-learning</span></span>           |
| <span data-ttu-id="14d52-137">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="14d52-137">Service Fabric</span></span>            | <span data-ttu-id="14d52-138">Azure/compute/service-infrastructuur</span><span class="sxs-lookup"><span data-stu-id="14d52-138">azure/compute/service-fabric</span></span>          |
| <span data-ttu-id="14d52-139">VSTS</span><span class="sxs-lookup"><span data-stu-id="14d52-139">VSTS</span></span>                      | <span data-ttu-id="14d52-140">Azure/vsts</span><span class="sxs-lookup"><span data-stu-id="14d52-140">azure/vsts</span></span>                            |


## <a name="next-steps"></a><span data-ttu-id="14d52-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14d52-141">Next steps</span></span>
[<span data-ttu-id="14d52-142">Meer informatie over registers en Hallo ondersteund services en orchestrators</span><span class="sxs-lookup"><span data-stu-id="14d52-142">Learn more about registries and hello supported services and orchestrators</span></span>](container-registry-intro.md)
