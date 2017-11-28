---
title: aaaMonitor Azure DC/OS-cluster - Datadog | Microsoft Docs
description: Een Azure Container Service-cluster met Datadog bewaken. Hallo DC/OS web UI toodeploy hello Datadog agents tooyour cluster gebruiken.
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
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="3ee89-105">Een Azure Container Service DC/OS-cluster met Datadog bewaken</span><span class="sxs-lookup"><span data-stu-id="3ee89-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="3ee89-106">In dit artikel implementeert we Datadog agents tooall Hallo agent knooppunten in uw Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="3ee89-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="3ee89-107">U moet een account met Datadog voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="3ee89-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3ee89-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3ee89-108">Prerequisites</span></span>
<span data-ttu-id="3ee89-109">[Implementeer](container-service-deployment.md) en [verbind](../container-service-connect.md) een cluster dat door Azure Container Service is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3ee89-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="3ee89-110">Hallo verkennen [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="3ee89-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="3ee89-111">Ga te[http://datadoghq.com](http://datadoghq.com) tooset van een Datadog-account.</span><span class="sxs-lookup"><span data-stu-id="3ee89-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="3ee89-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="3ee89-112">Datadog</span></span>
<span data-ttu-id="3ee89-113">Datadog is een controleservice die bewakingsgegevens moeten worden verzameld uit uw containers in uw Azure Container Service-cluster.</span><span class="sxs-lookup"><span data-stu-id="3ee89-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="3ee89-114">Datadog heeft een Docker-integratie Dashboard waarin u de specifieke metrische gegevens binnen uw containers kunt zien.</span><span class="sxs-lookup"><span data-stu-id="3ee89-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="3ee89-115">Metrische gegevens die afkomstig zijn van uw containers worden ingedeeld op basis van CPU, geheugen, netwerk en i/o.</span><span class="sxs-lookup"><span data-stu-id="3ee89-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="3ee89-116">Datadog splitst metrische gegevens in containers en afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="3ee89-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="3ee89-117">Een voorbeeld van welke Hallo UI lijkt erop dat voor CPU-gebruik hieronder is.</span><span class="sxs-lookup"><span data-stu-id="3ee89-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Datadog gebruikersinterface](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="3ee89-119">Een implementatie met Datadog met Marathon configureren</span><span class="sxs-lookup"><span data-stu-id="3ee89-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="3ee89-120">Deze stappen wordt uitgelegd hoe u tooconfigure en implementeren van Datadog toepassingen tooyour cluster met Marathon.</span><span class="sxs-lookup"><span data-stu-id="3ee89-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="3ee89-121">Toegang tot uw DC/OS-Webgebruikersinterface via [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="3ee89-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="3ee89-122">Eenmaal in DC/OS-Webgebruikersinterface Navigeer Hallo toohello 'Universe' die op Hallo is onderste links en zoek naar 'Datadog' en op 'Installeren'.</span><span class="sxs-lookup"><span data-stu-id="3ee89-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Datadog pakket binnen Hallo DC/OS Universe](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="3ee89-124">Nu toocomplete Hallo configuratie moet u een account Datadog of een gratis proefaccount.</span><span class="sxs-lookup"><span data-stu-id="3ee89-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="3ee89-125">Nadat u bent aangemeld Zoek toohello links in toohello Datadog website en ga vervolgens door tooIntegrations -> [API's](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="3ee89-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API-sleutel](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="3ee89-127">Naast uw API-sleutel in Hallo Datadog configuratie binnen Hallo DC/OS Universe invoeren.</span><span class="sxs-lookup"><span data-stu-id="3ee89-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Configuratie van de Datadog in Hallo DC/OS Universe](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="3ee89-129">In Hallo hierboven configuratie exemplaren too10000000 ingesteld zodat wanneer een nieuw knooppunt wordt toegevoegd toohello cluster Datadog een agent toothat knooppunt automatisch implementeren.</span><span class="sxs-lookup"><span data-stu-id="3ee89-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="3ee89-130">Dit is een tijdelijke oplossing.</span><span class="sxs-lookup"><span data-stu-id="3ee89-130">This is an interim solution.</span></span> <span data-ttu-id="3ee89-131">Zodra u Hallo pakket hebt geïnstalleerd moet u navigeren back toohello Datadog website en vinden '[Dashboards](https://app.datadoghq.com/dash/list). "</span><span class="sxs-lookup"><span data-stu-id="3ee89-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="3ee89-132">Daar ziet u aangepaste en integratie-Dashboards.</span><span class="sxs-lookup"><span data-stu-id="3ee89-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="3ee89-133">Hallo [Docker-dashboard](https://app.datadoghq.com/screen/integration/docker) hebben alle Hallo container metrische gegevens u moet voor het bewaken van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="3ee89-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

