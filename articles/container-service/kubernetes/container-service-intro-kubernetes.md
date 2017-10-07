---
title: aaaIntroduction tooAzure Containerservice voor Kubernetes | Microsoft Docs
description: Azure Container Service voor Kubernetes maakt het eenvoudig toodeploy en beheren van toepassingen op basis van een container in Azure.
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kubernetes, Docker, containers, microservices, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a><span data-ttu-id="52164-104">Inleiding tooAzure Containerservice voor Kubernetes</span><span class="sxs-lookup"><span data-stu-id="52164-104">Introduction tooAzure Container Service for Kubernetes</span></span>
<span data-ttu-id="52164-105">Azure Container Service voor Kubernetes maakt het eenvoudig toocreate, configureren en beheren van een cluster van virtuele machines die vooraf geconfigureerde toorun beperkte toepassingen zijn.</span><span class="sxs-lookup"><span data-stu-id="52164-105">Azure Container Service for Kubernetes makes it simple toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="52164-106">Dit kunt u toouse uw bestaande vaardigheden of tekenen van een grote en groeiende hoofdtekst van de community-expertise, toodeploy en beheren van toepassingen op basis van een container op Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="52164-106">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

<span data-ttu-id="52164-107">U kunt profiteren van Hallo bedrijfsniveau functies van Azure, zonder dat zij de toepassing draagbaarheid via Kubernetes en Docker-afbeeldingsindeling Hallo met behulp van Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="52164-107">By using Azure Container Service, you can take advantage of hello enterprise-grade features of Azure, while still maintaining application portability through Kubernetes and hello Docker image format.</span></span>

## <a name="using-azure-container-service-for-kubernetes"></a><span data-ttu-id="52164-108">Azure Container Service voor Kubernetes gebruiken</span><span class="sxs-lookup"><span data-stu-id="52164-108">Using Azure Container Service for Kubernetes</span></span>
<span data-ttu-id="52164-109">Ons doel met Azure Container Service is een container hostomgeving tooprovide met behulp van open-source hulpprogramma's en -technologieën die tegenwoordig populair onder onze klanten.</span><span class="sxs-lookup"><span data-stu-id="52164-109">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="52164-110">einde toothis, geven we Hallo standaard Kubernetes API-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="52164-110">toothis end, we expose hello standard Kubernetes API endpoints.</span></span> <span data-ttu-id="52164-111">Met behulp van deze standaard eindpunten, kunt u gebruikmaken van alle software die geschikt is voor het praten tooa Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="52164-111">By using these standard endpoints, you can leverage any software that is capable of talking tooa Kubernetes cluster.</span></span> <span data-ttu-id="52164-112">U kunt bijvoorbeeld [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/) of [draft](https://github.com/Azure/draft) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="52164-112">For example, you might choose [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), or [draft](https://github.com/Azure/draft).</span></span>

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a><span data-ttu-id="52164-113">Een Kubernetes-cluster maken met Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="52164-113">Creating a Kubernetes cluster using Azure Container Service</span></span>
<span data-ttu-id="52164-114">toobegin Azure Containerservice met een Azure Container Service-cluster met Hallo implementeren [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) of via de portal hello (zoeken Hallo Marketplace voor **Azure Container Service**).</span><span class="sxs-lookup"><span data-stu-id="52164-114">toobegin using Azure Container Service, deploy an Azure Container Service cluster with hello [Azure CLI 2.0](container-service-kubernetes-walkthrough.md) or via hello portal (search hello Marketplace for **Azure Container Service**).</span></span> <span data-ttu-id="52164-115">Als u een geavanceerde gebruiker die meer controle over hello Azure Resource Manager-sjablonen moet, kunt u open-source Hallo [acs-engine](https://github.com/Azure/acs-engine) project toobuild uw eigen aangepaste Kubernetes cluster en deze implementeren via Hallo `az` CLI.</span><span class="sxs-lookup"><span data-stu-id="52164-115">If you are an advanced user who needs more control over hello Azure Resource Manager templates, you can use hello open source [acs-engine](https://github.com/Azure/acs-engine) project toobuild your own custom Kubernetes cluster and deploy it via hello `az` CLI.</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="52164-116">Kubernetes gebruiken</span><span class="sxs-lookup"><span data-stu-id="52164-116">Using Kubernetes</span></span>
<span data-ttu-id="52164-117">Kubernetes automatiseert het implementeren, schalen en beheren van toepassingen in containers.</span><span class="sxs-lookup"><span data-stu-id="52164-117">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="52164-118">De applicatie bevat een uitgebreide set functies, zoals:</span><span class="sxs-lookup"><span data-stu-id="52164-118">It has a rich set of features including:</span></span>
* <span data-ttu-id="52164-119">Automatische binpacking</span><span class="sxs-lookup"><span data-stu-id="52164-119">Automatic binpacking</span></span>
* <span data-ttu-id="52164-120">Automatisch herstel</span><span class="sxs-lookup"><span data-stu-id="52164-120">Self-healing</span></span>
* <span data-ttu-id="52164-121">Horizontaal schalen</span><span class="sxs-lookup"><span data-stu-id="52164-121">Horizontal scaling</span></span>
* <span data-ttu-id="52164-122">Servicedetectie en taakverdeling</span><span class="sxs-lookup"><span data-stu-id="52164-122">Service discovery and load balancing</span></span>
* <span data-ttu-id="52164-123">Geautomatiseerde implementaties en terugdraaiacties</span><span class="sxs-lookup"><span data-stu-id="52164-123">Automated rollouts and rollbacks</span></span>
* <span data-ttu-id="52164-124">Geheimen- en configuratiebeheer</span><span class="sxs-lookup"><span data-stu-id="52164-124">Secret and configuration management</span></span>
* <span data-ttu-id="52164-125">Opslagindeling</span><span class="sxs-lookup"><span data-stu-id="52164-125">Storage orchestration</span></span>
* <span data-ttu-id="52164-126">Batchuitvoering</span><span class="sxs-lookup"><span data-stu-id="52164-126">Batch execution</span></span>

<span data-ttu-id="52164-127">Architectuurdiagram van Kubernetes geïmplementeerd via Azure Container Service:</span><span class="sxs-lookup"><span data-stu-id="52164-127">Architectural diagram of Kubernetes deployed via Azure Container Service:</span></span>

![Azure Container Service geconfigureerd toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a><span data-ttu-id="52164-129">Video's</span><span class="sxs-lookup"><span data-stu-id="52164-129">Videos</span></span>

<span data-ttu-id="52164-130">Ondersteuning voor Kubernetes in Azure Container Service (Azure Friday, januari 2017):</span><span class="sxs-lookup"><span data-stu-id="52164-130">Kubernetes Support in Azure Container Services (Azure Friday, January 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

<span data-ttu-id="52164-131">Hulpprogramma's voor het ontwikkelen en implementeren van toepassingen in Kubernetes (Azure OpenDev, juni 2017):</span><span class="sxs-lookup"><span data-stu-id="52164-131">Tools for Developing and Deploying Applications on Kubernetes (Azure OpenDev, June 2017):</span></span>

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="52164-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52164-132">Next steps</span></span>

<span data-ttu-id="52164-133">Hallo verkennen [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin vandaag nog met het verkennen van Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="52164-133">Explore hello [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin exploring Azure Container Service today.</span></span>
