---
title: groepen met aaaDC/OS-agent voor Azure Container Service | Microsoft Docs
description: Hoe Hallo openbare en persoonlijke agent pools werken met een Azure Container Service DC/OS-cluster
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="6df36-104">Groepen met DC/OS-agent voor Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="6df36-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="6df36-105">DC/OS-clusters in Azure Container Service bevatten agent knooppunten in twee groepen, een openbare toepassingen en een persoonlijke toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6df36-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="6df36-106">Een toepassing kan worden geïmplementeerd tooeither groep, toegankelijkheid tussen computers in uw containerservice beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="6df36-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="6df36-107">Hallo machines kunnen worden blootgesteld toohello internet (openbaar) of interne (particuliere) wilt bewaren.</span><span class="sxs-lookup"><span data-stu-id="6df36-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="6df36-108">Dit artikel bevat een kort overzicht van waarom er groepen van openbare en persoonlijke zijn.</span><span class="sxs-lookup"><span data-stu-id="6df36-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="6df36-109">**Persoonlijke agents**: persoonlijke agent knooppunten uitvoeren via een niet-routeerbaar netwerk.</span><span class="sxs-lookup"><span data-stu-id="6df36-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="6df36-110">Dit netwerk is alleen toegankelijk vanuit Hallo beheerder zone of via Hallo openbare zone edge router.</span><span class="sxs-lookup"><span data-stu-id="6df36-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="6df36-111">Standaard start DC/OS-apps op persoonlijke agent knooppunten.</span><span class="sxs-lookup"><span data-stu-id="6df36-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="6df36-112">**Openbare agents**: openbare agent knooppunten uitvoeren DC/OS-apps en services via een openbaar toegankelijk netwerk.</span><span class="sxs-lookup"><span data-stu-id="6df36-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="6df36-113">Zie voor meer informatie over netwerkbeveiliging DC/OS Hallo [DC/OS-documentatie](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="6df36-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="6df36-114">Agent-groepen implementeren</span><span class="sxs-lookup"><span data-stu-id="6df36-114">Deploy agent pools</span></span>

<span data-ttu-id="6df36-115">Hallo DC/OS-agent van toepassingen In Azure Container Service gemaakt als volgt:</span><span class="sxs-lookup"><span data-stu-id="6df36-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="6df36-116">Hallo **persoonlijke groep** bevat Hallo-nummer van de agent-knooppunten opgeven wanneer u [Hallo DC/OS-cluster implementeren](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6df36-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="6df36-117">Hallo **openbare groep** in eerste instantie bevat een vooraf vastgesteld aantal knooppunten van de agent.</span><span class="sxs-lookup"><span data-stu-id="6df36-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="6df36-118">Deze groep wordt automatisch toegevoegd wanneer Hallo DC/OS-cluster is ingericht.</span><span class="sxs-lookup"><span data-stu-id="6df36-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="6df36-119">Hallo persoonlijke pool en Hallo van openbare toepassingen worden virtuele Azure-machine-schaalsets.</span><span class="sxs-lookup"><span data-stu-id="6df36-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="6df36-120">U kunt deze groepen wijzigen na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="6df36-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="6df36-121">Agent pools gebruiken</span><span class="sxs-lookup"><span data-stu-id="6df36-121">Use agent pools</span></span>
<span data-ttu-id="6df36-122">Standaard **Marathon** implementeert een nieuwe toepassing toohello *persoonlijke* agent knooppunten.</span><span class="sxs-lookup"><span data-stu-id="6df36-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="6df36-123">U hebt tooexplicitly Hallo toepassing toohello implementeren *openbare* knooppunten tijdens het maken van de toepassing hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="6df36-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="6df36-124">Selecteer Hallo **optioneel** tabblad en voer **slave_public** voor Hallo **geaccepteerde resourcerollen** waarde.</span><span class="sxs-lookup"><span data-stu-id="6df36-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="6df36-125">Dit proces wordt beschreven [hier](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) en in Hallo [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="6df36-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6df36-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6df36-126">Next steps</span></span>
* <span data-ttu-id="6df36-127">Lees meer over [beheer van uw DC/OS-containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="6df36-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="6df36-128">Meer informatie over hoe te[Hallo firewall openen](container-service-enable-public-access.md) verstrekt door Azure tooallow openbare toegang tooyour DC/OS containers.</span><span class="sxs-lookup"><span data-stu-id="6df36-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

