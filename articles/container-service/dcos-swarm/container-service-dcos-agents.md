---
title: Groepen met DC/OS-agent voor Azure Container Service | Microsoft Docs
description: De werking van de openbare en persoonlijke agent-adresgroepen met een Azure Container Service DC/OS-cluster
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
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="85733-104">Groepen met DC/OS-agent voor Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="85733-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="85733-105">DC/OS-clusters in Azure Container Service bevatten agent knooppunten in twee groepen, een openbare toepassingen en een persoonlijke toepassingen.</span><span class="sxs-lookup"><span data-stu-id="85733-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="85733-106">Een toepassing kan worden geïmplementeerd aan de groep, toegankelijkheid tussen computers in uw containerservice beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="85733-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="85733-107">De machines kunnen worden blootgesteld aan internet (openbaar) of interne (particuliere) bewaard.</span><span class="sxs-lookup"><span data-stu-id="85733-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="85733-108">Dit artikel bevat een kort overzicht van waarom er groepen van openbare en persoonlijke zijn.</span><span class="sxs-lookup"><span data-stu-id="85733-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="85733-109">**Persoonlijke agents**: persoonlijke agent knooppunten uitvoeren via een niet-routeerbaar netwerk.</span><span class="sxs-lookup"><span data-stu-id="85733-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="85733-110">Dit netwerk is alleen toegankelijk vanuit de zone van de beheerder of via de router van de rand openbare zone.</span><span class="sxs-lookup"><span data-stu-id="85733-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="85733-111">Standaard start DC/OS-apps op persoonlijke agent knooppunten.</span><span class="sxs-lookup"><span data-stu-id="85733-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="85733-112">**Openbare agents**: openbare agent knooppunten uitvoeren DC/OS-apps en services via een openbaar toegankelijk netwerk.</span><span class="sxs-lookup"><span data-stu-id="85733-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="85733-113">Zie voor meer informatie over netwerkbeveiliging DC/OS de [DC/OS-documentatie](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span><span class="sxs-lookup"><span data-stu-id="85733-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="85733-114">Agent-groepen implementeren</span><span class="sxs-lookup"><span data-stu-id="85733-114">Deploy agent pools</span></span>

<span data-ttu-id="85733-115">De DC/OS-agent van toepassingen In Azure Container Service gemaakt als volgt:</span><span class="sxs-lookup"><span data-stu-id="85733-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="85733-116">De **persoonlijke groep** bevat het nummer van de agent-knooppunten opgeven wanneer u [de DC/OS-cluster implementeren](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="85733-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="85733-117">De **openbare groep** in eerste instantie bevat een vooraf vastgesteld aantal knooppunten van de agent.</span><span class="sxs-lookup"><span data-stu-id="85733-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="85733-118">Deze groep wordt automatisch toegevoegd wanneer de DC/OS-cluster is ingericht.</span><span class="sxs-lookup"><span data-stu-id="85733-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="85733-119">De persoonlijke groep en de openbare toepassingen worden virtuele Azure-machine-schaalsets.</span><span class="sxs-lookup"><span data-stu-id="85733-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="85733-120">U kunt deze groepen wijzigen na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="85733-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="85733-121">Agent pools gebruiken</span><span class="sxs-lookup"><span data-stu-id="85733-121">Use agent pools</span></span>
<span data-ttu-id="85733-122">Standaard **Marathon** implementeert een nieuwe toepassing aan de *persoonlijke* agent knooppunten.</span><span class="sxs-lookup"><span data-stu-id="85733-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="85733-123">U moet expliciet de toepassing implementeren naar de *openbare* knooppunten tijdens het maken van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="85733-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="85733-124">Selecteer de **optioneel** tabblad en voer **slave_public** voor de **geaccepteerde resourcerollen** waarde.</span><span class="sxs-lookup"><span data-stu-id="85733-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="85733-125">Dit proces wordt beschreven [hier](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) en in de [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="85733-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85733-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="85733-126">Next steps</span></span>
* <span data-ttu-id="85733-127">Lees meer over [beheer van uw DC/OS-containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="85733-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="85733-128">Meer informatie over hoe [de firewall openen](container-service-enable-public-access.md) verstrekt door Azure voor openbare toegang tot uw DC/OS-containers.</span><span class="sxs-lookup"><span data-stu-id="85733-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

