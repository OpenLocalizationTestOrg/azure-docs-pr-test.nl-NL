---
title: Monitor Azure DC/OS-cluster - Datadog | Microsoft Docs
description: Een Azure Container Service-cluster met Datadog bewaken. Gebruik de DC/OS-webgebruikersinterface voor het implementeren van de agents Datadog met uw cluster.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Containers, DC/OS Docker Swarm-Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 9dd451f994940d7cc3a59bd7fd08a8f067345e34
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="641fa-105">Een Azure Container Service DC/OS-cluster met Datadog bewaken</span><span class="sxs-lookup"><span data-stu-id="641fa-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="641fa-106">In dit artikel wordt we Datadog agents op alle knooppunten van een agent in uw Azure Container Service-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="641fa-106">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="641fa-107">U moet een account met Datadog voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="641fa-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="641fa-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="641fa-108">Prerequisites</span></span>
<span data-ttu-id="641fa-109">[Implementeer](container-service-deployment.md) en [verbind](../container-service-connect.md) een cluster dat door Azure Container Service is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="641fa-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="641fa-110">Verken de [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="641fa-110">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="641fa-111">Ga naar [http://datadoghq.com](http://datadoghq.com) voor het instellen van een Datadog-account.</span><span class="sxs-lookup"><span data-stu-id="641fa-111">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="641fa-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="641fa-112">Datadog</span></span>
<span data-ttu-id="641fa-113">Datadog is een controleservice die bewakingsgegevens moeten worden verzameld uit uw containers in uw Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="641fa-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="641fa-114">Datadog heeft een Docker-integratie Dashboard waarin u de specifieke metrische gegevens binnen uw containers kunt zien.</span><span class="sxs-lookup"><span data-stu-id="641fa-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="641fa-115">Metrische gegevens die afkomstig zijn van uw containers worden ingedeeld op basis van CPU, geheugen, netwerk en i/o.</span><span class="sxs-lookup"><span data-stu-id="641fa-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="641fa-116">Datadog splitst metrische gegevens in containers en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="641fa-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="641fa-117">Er is een voorbeeld van hoe de gebruikersinterface voor CPU-gebruik eruit hieronder.</span><span class="sxs-lookup"><span data-stu-id="641fa-117">An example of what the UI looks like for CPU usage is below.</span></span>

![Datadog gebruikersinterface](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="641fa-119">Een implementatie met Datadog met Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="641fa-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="641fa-120">Deze stappen wordt beschreven hoe u configureren en implementeren van toepassingen Datadog aan het cluster met Marathon.</span><span class="sxs-lookup"><span data-stu-id="641fa-120">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="641fa-121">Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="641fa-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="641fa-122">Eenmaal in de DC/OS-gebruikersinterface Navigeer naar de 'Universe' die is op de links onder en zoek naar 'Datadog' en klik op 'Installeren'.</span><span class="sxs-lookup"><span data-stu-id="641fa-122">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span></span>

![Datadog pakket binnen de DC/OS-Universe](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="641fa-124">Nu om de configuratie te voltooien, moet u een account Datadog of een gratis proefaccount.</span><span class="sxs-lookup"><span data-stu-id="641fa-124">Now to complete the configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="641fa-125">Nadat u bent aangemeld bij het uiterlijk van de website Datadog naar links en gaat u naar integraties -> vervolgens [API's](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="641fa-125">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API-sleutel](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="641fa-127">Naast uw API-sleutel in de configuratie van de Datadog binnen de DC/OS-Universe invoeren.</span><span class="sxs-lookup"><span data-stu-id="641fa-127">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span></span> 

![Datadog configuratie in de DC/OS-Universe](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="641fa-129">In de bovenstaande configuratie exemplaren zijn ingesteld op 10000000 doet wanneer een nieuw knooppunt wordt toegevoegd aan het cluster Datadog implementeren automatisch een agent naar dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="641fa-129">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span></span> <span data-ttu-id="641fa-130">Dit is een tijdelijke oplossing.</span><span class="sxs-lookup"><span data-stu-id="641fa-130">This is an interim solution.</span></span> <span data-ttu-id="641fa-131">Als u het pakket moet u Ga terug naar de website Datadog en vinden hebt geïnstalleerd '[Dashboards](https://app.datadoghq.com/dash/list). "</span><span class="sxs-lookup"><span data-stu-id="641fa-131">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="641fa-132">Daar ziet u aangepaste en integratie-Dashboards.</span><span class="sxs-lookup"><span data-stu-id="641fa-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="641fa-133">De [Docker-dashboard](https://app.datadoghq.com/screen/integration/docker) hebben alle de container metrische gegevens die u nodig hebt voor het bewaken van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="641fa-133">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span></span> 

